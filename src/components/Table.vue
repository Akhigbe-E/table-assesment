<template>
  <div class="outer">
    <div class="inner">
      <table>
        <tr>
          <th class="fix">Project Name</th>
          <th v-for="(head, index) in columnHeads" :class="hasSmallWidth(head)? 'small-width':''" :key="index">
            <TableHeadWithIcon v-if="head === 'status'" title="Status" @selectOption="setStatusToView" :filters="tableFilters[head]"/>
            <span v-else>
              {{head | createName}}
            </span>
          </th>
        </tr>
        <TableLoader v-if="!tableData.length" :lengthOfColumns="lengthOfColumns"/>
        <EmptyTable v-else-if="tableData.length && !dataToDisplay.length" :lengthOfColumns="lengthOfColumns"/>
        <TableRow v-else v-for="(details, index) in dataToDisplay" :details="details" :columnLength="lengthOfColumns" :columnHeads="columnHeads" :key="index"/>
      </table>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'
import TableRow from './TableRow.vue'
import TableHeadWithIcon from './TableHeadWithIcon.vue'
import EmptyTable from './EmptyTable.vue'
import TableLoader from './TableLoader.vue'

import '../assets/index.sass'
export default {
  components: { TableRow, TableHeadWithIcon, EmptyTable, TableLoader },
  props: ['tableData', 'tableFilters'],
  data:()=>({
    statusToView: 'Under construction',
    displayedColumnHeads: ['developer', 'main_contractor', 'state', 'status', 'sector', 'lga', 'region']
  }),
  computed:{
    columnHeads(){
      return [...this.displayedColumnHeads]
    },
    dataToDisplay(){
      return this.filterDataByStatus(this.statusToView)
    },
    lengthOfColumns(){
      return Object.values(this.columnHeads).length
    }
  },
  filters:{
    createName(name){
      return _.startCase(name)
    }
  },
  methods:{
    selectPreferedColumns(columnName){
      if(this.displayedColumnHeads.includes(columnName)){
        const columnIndex = this.displayedColumnHeads.indexOf(columnName);
        this.displayedColumnHeads.splice(columnIndex, 1)
      }else{
        this.displayedColumnHeads.push(columnName)
      }
    },
    hasSmallWidth(columnName){
      return columnName === 'state' || columnName === 'status'
    },
    filterDataByStatus(statusToView){
      return this.tableData.filter(el => el.status === statusToView)
    },
    setStatusToView(status = 'On hold'){
      this.statusToView = status
    }
  },
}
</script>

<style lang="sass" scoped>
  table
    table-layout: fixed;
    width: 100%;
    border-radius: 5px
    border-collapse: separate;
    background-color: transparent;
    border-spacing: 0;
    color: #52606B;

  th
    background-color: #293A4A;
    color: #fff;

  tr .small-width
    width: 190px

  .table-header
    display: grid;
  
  th:first-child
    width: 218px;
    margin-left: -250px
    padding: 1.75rem 1rem
    border-top-left-radius: 8px;
    box-shadow: 6px 0px 5px -2px #273847;

  .outer 
    position: relative;
    border-radius: 5px
    overflow-x: scroll;
    overflow-y: hidden;
    box-shadow: 0.2rem 0.1rem 0.4em rgba(0, 0, 0, 0.2)

  .inner
    border-top-right-radius: 8px
    overflow-x: scroll;
    margin-left: 250px
    z-index: 0;
    min-height: 275px;

  @media only screen and (max-width: 600px)
    th:first-child
      width: 250px;
      margin-left: -250px
      padding: 1.75rem 0.5rem
      border-top-left-radius: 8px

    .fix
      position: relative;    
      width: 250px;

    .inner
      margin-left: 0px;
    
    .outer 
      width: unset; 
      border-radius: 5px
</style>
