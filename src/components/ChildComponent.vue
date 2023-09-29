
<template>
    <h1>Message:{{ message }}</h1>
    <h1>Message:{{ number }}</h1>
    <hr />
  
</template>

<script>
export default {
  props:{
    message:{
      type:String,
      default:'aslam'
    },
    number:{
      type:Number,
      default:0
    }
  }
}
</script>

