<template>
  <div class="app">
    <div class="container">
      <div class="table-top">
        <div>{{tableData.length}} Projects</div>
        <div class="table-top-right">
          <div>
            {{tableMeta.from}} - {{tableMeta.to}} of {{tableMeta.total}}
          </div>
          <div style="display: flex; justify-self: end; align-items: center">
            <span>
              Display Map
            </span>
            <label class="switch">
              <input type="checkbox">
              <span class="slider round"></span>
            </label>
          </div>
        </div>
      </div>
      <Table :tableData="tableData" :tableFilters="tableFilters"/>
    </div>
  </div>
</template>

<script>
import Table from './components/Table.vue'
export default {
  data:() => ({
    tableData: [],
    tableFilters:{},
    tableMeta:{}
  }),
  components: { Table },
  async created(){
    const {data, filters, meta} = await (await fetch('https://244b8df3-7491-4cfd-a48b-267f19446372.mock.pstmn.io/')).json();
    this.tableData = data
    this.tableFilters = filters
    this.tableMeta = meta
  }
}
</script>

<style lang="sass" scoped>
  .app
    background: #F5F9FC;
    padding: 50px 0;
  .table-top
    display: grid;
    grid-row-gap: 24px; 
    margin-bottom: 32px;
    grid-template-columns: auto auto;
    &-right
      display: grid;
      grid-template-columns: auto auto;

  .container
    font-family: arial, sans-serif;
    margin: 0px auto;
    width: 98%;

  .switch 
    position: relative;
    display: inline-block;
    width: 60px;
    margin-left: 8px

  .switch input 
    opacity: 0;
    width: 0;
    height: 0;

  .slider
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    height: 13px;
    width: 32px;
    background-color: #5D6B7A;
    transition: .4s;


  .slider:before
    position: absolute;
    content: "";
    height: 18px;
    width: 18px;
    top: -3px;
    left: 0px;
    border: 1px solid whitesmoke;
    bottom: 4px;
    background-color: white;
    transition: .4s;

  input:checked + .slider
    background-color: #ccc;

  input:focus + .slider
    box-shadow: 0 0 1px #ccc;

  input:checked + .slider:before
    transform: translateX(13px);

  .slider.round 
    border-radius: 34px;

  .slider.round:before
    border-radius: 50%;

</style>