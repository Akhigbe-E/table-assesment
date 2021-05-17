<template>
  <div style="z-index:1000" class="overlay-container">
    <button class="vp-btn">View Product</button>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="sass" scoped>
  .vp-btn
      border: 2px solid #ACB1B5;
      border-radius: 6px; 
      color: #80868E;
      padding: 12px 36px;
      background: white;
      font-size: 1rem;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      cursor: pointer;
      
  .overlay-container
    position: relative;
    width: 100%;
    height: 92px;
    background: inherit;

  .overlay-container:before
    content: '';
    position: absolute;
    width: 100%;
    z-index: -1;
    height: 92px;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0px;
    background: inherit;
    box-shadow: inset 0 0 0 200px rgba(255,255,255,0.3);
    backdrop-filter: blur(2.5px);
</style>