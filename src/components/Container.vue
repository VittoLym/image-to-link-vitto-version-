<script setup>
import Form from './Form.vue'
</script>
<template>
    <div class="container">
        <h3><span class="image">Image</span> to <span>Link</span> </h3>
        <Form></Form>
    </div>
</template>
<style scoped>
.container{
  border: 7px solid #20101060;
  border-radius: 15px;
  background-color: #00000028;
  height: 90vh;
  width: 60vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: start;
  margin: .5rem 0;
  padding:1rem 0;
}
h3{
  font-size:2rem;
  margin:0;
  color:#000;
}
.image{
  color:#662299;
}
span{
  color:green;
}

</style>