<template>
    <tr @mouseover="showViewProductButton" @mouseleave="hideViewProductButton" style="position:relative">
        <td class="fix proj-name-col">{{details['project_name']}}</td>
        <span v-if="isHovered" class="overlay">
            <ViewProductBtn/>
        </span>
        <td v-for="(columnNumber, index) in columnLength" :key="index">
          <span v-if="columnHeads[index] === 'status'">
            <TableStatusLabel :value="details[columnHeads[index]]"/>
          </span>
          <span v-else>
            {{details[columnHeads[index]]}}
          </span>
        </td>
    </tr>
</template>

<script>
import TableStatusLabel from './TableStatusLabel.vue'
import ViewProductBtn from './ViewProduct.vue';

import '../assets/index.sass'
export default {
  components: { ViewProductBtn, TableStatusLabel },
    props:['details', 'columnLength', 'columnHeads'],
    data:() => ({
        isHovered: false,
    }),
    methods:{
        showViewProductButton(){
            this.isHovered  = true
        },
        hideViewProductButton(){
            this.isHovered  = false
        }
    }
}
</script>

<style lang="sass" scoped>
  .overlay
    position: absolute;
    width: 78%;
    height: 92px;
    overflow-y: scroll;
    text-align: center;

  @media only screen and (max-width: 600px)
    th:first-child
      width: 218px;
      padding: 1.75rem 0.5rem
      border-top-left-radius: 8px

    .fix
      position: relative;    
      width: 218px;
</style>