<script>
 export default {
   props: {
     label: {
       type: String,
       default: ''
     },
     modelValue: {
       type: [String, Number],
       default: ''
     },
     error: {
       type: String,
       default: ''
     }
   }
 }
</script>

<template>
  <label :for="label">{{ label }}</label>
    <input
    v-bind="$attrs"
    placeholder="start here..."
    :id="label"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  >
</template>

<style>
label {
  display: block;
  text-align: left;
}

[type="text"]{
  font-size: 16px;
  padding: 10px;
  width: 100%;
  margin: 5px 0 15px;
}

[type="text"]:focus{
  border: 2px solid #7e5bef;
  outline: none;
}
</style>
