<template>
    <span style="position:relative">      
        <span @click="toggleOptionsVisibility" class="head-with-icon">
            <span>{{title}}</span>
            <span><img src="../assets/sortDown.png" alt="sort"></span>
        </span>
        <div v-if="isOptionsVisible" class="dropdown-items">
            <div
                class="dropdown-item"
                v-for="(option, i) of filters"
                :key="i"
                @click="
                    selected = option;
                    isOptionsVisible = false;
                    $emit('selectOption', option);
                "
            >
                {{ option }}
            </div>
        </div>
    </span>
</template>

<script>
export default {
    props:['title', 'filters'],
    data:()=>({
        isOptionsVisible: false,
        selected: ''
    }),
    methods:{
        toggleOptionsVisibility(){
            this.isOptionsVisible = !this.isOptionsVisible
        }
    }
}
</script>

<style lang="sass">
  .head-with-icon
    display: flex;
    align-items: center;
    cursor: pointer;
    img
      display: inherit;
      margin-left: 32px;
      width: 16px

  .dropdown
    &-items
        position: absolute;
        width: max-content;
        min-width: 150px;
        border-radius: 8px;
        color: #52606B
        background: white;
        z-index: 1000;
        margin-top: 10px;
        padding: 5px 0px;
        box-shadow: 0.2rem 0.1rem 0.4em rgba(0, 0, 0, 0.1)

    &-item
        padding: 8px 32px 8px 16px
        font-weight: 100;
        cursor: pointer;

    &-item:hover
        background: #F6FAFD
</style>