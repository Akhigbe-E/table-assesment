<template>
   <tr class="empty-products" >
        <td :colspan="lengthOfColumns" rowspan="2">No Products</td>
    </tr>
</template>

<script>
export default {
    props:['lengthOfColumns']
}
</script>

<style lang="sass">
  .empty-products
    text-align: center;
    td
        font-size: 48px;
        padding-top: 40px;

</style>