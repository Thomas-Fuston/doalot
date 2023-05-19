<script>
  export default {
    props: {
      error: {
        type: String,
        default: ''
      }
    }
  }
</script>

<template>
  <div class="Error-wrapper">
    <div class="Error">
      {{ error }}
    </div>
  </div>
</template>

<style>
  .Error-wrapper {
    position: fixed;
    top: 20px;
  }
  .Error {
    padding: 20px;
    color: white;
    background: #e13314;
    box-shadow: 3px 3px 5px rgba(0,0,0,0.1);
    border: 1px solid #1f2d3d;
    width: 400px;
    text-align: center;
  }
</style>
