<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <h1>{{num}} - {{name | uppercase }}</h1>
    <small>{{url}}</small>
  </div>
</template>

<script>
export default {
    props: {
    num: Number,
    name: String,
    url: String,
    
  }, 
  filters: {
    uppercase: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.toUpperCase()
    }

  }
}
</script>

<style>
</style>