<template>
    <tbody>
        <tr
        v-for="index in 10"
        :key="index"
        >
            <td class="fix proj-name-col">
                <div
                class="loader-item"
                :style="`width: ${Math.floor(Math.random() * 51) + 50}%;`"
                />
            </td>

            <td
                v-for="(head, index) in lengthOfColumns"
                :key="index"
            >
                <div
                class="loader-item"
                :style="`width: ${Math.floor(Math.random() * 51) + 50}%;`"
                />
            </td>
        </tr>
    </tbody>
</template>

<script>
import '../assets/index.sass'
export default {
    props:['lengthOfColumns']
}
</script>

<style lang="sass" scoped>
  tr .small-width
    width: 190px

  .loader-item
    background: #80808014;
    height: 20px;
    border-radius: 8px;
</style>
