<script setup>
import { ref, defineEmits, } from 'vue'
import { toast } from "vue3-toastify";
import DropSvg from "./DropSvg.vue";
const formElement = ref("");
const emits = defineEmits(['urlImage','vtest','formElement','titleLink'])
const urlImage = ref('');
const isDraging = ref(false);
const vtest = ref(true)
const titleLink = ref('')

function handleInput(e) {
  formElement.value = e.target.files[0];
  emits('formElement', formElement.value)
  if(formElement === undefined){
    toast.error('try another type of image.',{
      autoClose:3000,
      closeButton:true,
    })
    vtest.value = true
    emits('vtest', vtest.value)
  }
  else{
    const reader = new FileReader();
    reader.onload = function(e){
      urlImage.value = e.target.result
      emits('urlImage',urlImage)
      vtest.value = true
      emits('vtest', vtest.value)
      titleLink.value = 'Create your link.'
      emits('titleLink', titleLink.value)
    }
    reader.readAsDataURL(formElement.value)
  }
}

function handleDrag(e) {
  formElement.value = e.dataTransfer.files[0];
  emits('formElement', formElement.value)
  if(formElement.value === undefined){
    toast.error('try another type of image.',{
      autoClose:3000,
      closeButton:true,
    })
    vtest.value = true
    emits('vtest', vtest.value)
  }
  else{
    const reader = new FileReader();
    reader.onload = function(e){
      urlImage.value = e.target.result
      emits('urlImage', urlImage.value)
      vtest.value = true
      emits('vtest', vtest.value)
      titleLink.value = 'Create your link.'
      emits('titleLink', titleLink.value)
    }
    reader.readAsDataURL(formElement.value)
  }
    isDraging.value = false
}

function dragStyle() {
  vtest.value = !vtest.value
  isDraging.value= !isDraging.value
  emits('vtest',vtest.value)
}

</script>
<template>
  <label
    for="imagenInput"
  >
    Drop your Image:
  </label>
    <article 
      class="archive-input" 
      :class="{'draging' : isDraging}"
      @dragenter.prevent="dragStyle"
      @dragleave.prevent="dragStyle"
      @dragover.prevent
      @drop.prevent="handleDrag"
      >
      <DropSvg v-if="!formElement?.name" :isDraging='isDraging'/>
      <span v-else>{{formElement.name}}</span>
    </article>
    <input type="file" @change="handleInput" id="imagenInput" />
</template>
<style scoped>
.drop {
  margin: .8rem 0;
  border-radius: 10px;
  animation-duration: 1s;
  animation-iteration-count: infinite;
  animation-name: moveDrop;
}

@keyframes moveDrop {
  25% {
    margin-top: 1.2rem;
  }
  75% {
    margin-top: .4rem;
  }
}

.archive-input {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content:center;
  width: 50vw;
  height: 20vh;
  color: #fefefe;
  background-color: #00000054;
  border-radius: 10px;
  transition: all ease .2s;
  cursor: pointer;
}
label{
  width:50vw;
  margin-bottom:0.6rem;
  font-weight:bolder;
}
.draging {
  background-color: #00000099;
}
.draging-item {
  fill: #00b52e;
}
input[type="file"] {
  display: none;
}

span {
  font-size: 1.2rem;
  font-weight: bold;
}
@media (max-width:800px){
  .archive-input{
    width:70vw;
    height:15vh;
  }
  label{
    width:70vw;
    margin-bottom:.3rem;
  }
}
</style>