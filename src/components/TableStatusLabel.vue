<template>
  <span :class="labelColour">{{value}}</span>
</template>

<script>
export default {
    props:['value'],
    computed:{
        labelColour(){
            return 'amber-label'
        }
    }
}
</script>

<style lang="sass">
    .amber-label
        color: #926820;
        background-color: #FCE2AB;
        padding: 4px 8px;
        border-radius: 3px;
</style>