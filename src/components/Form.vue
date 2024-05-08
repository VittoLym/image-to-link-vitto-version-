<script setup>
import DropSvg from "./DropSvg.vue";
import { ref } from "vue";
import Links from "./Links.vue";
import { toast } from "vue3-toastify";
const KEY = import.meta.env.VITE_API_SECRET;
const ENDPOINT_CLOUD = import.meta.env.VITE_CLOUDINARY_URL;
const IMG_DEFAULT = import.meta.env.VITE_DEFAULT_IMAGE;
const formElement = ref("");
const urlImage = ref(IMG_DEFAULT);
const isDraging = ref(false);

async function handleSubmit(e) {
  e.preventDefault();
  const formData = new FormData();
  try {
    if (formElement.value == "") {
      urlImage.value = "";
    } else {
      formData.append("file", formElement.value);
      formData.append("upload_preset", "bye1zwq8");
      formData.append("api_key", KEY);
      const response = await fetch(ENDPOINT_CLOUD, {
        method: "POST",
        body: formData,
      });
      const data = await response.json();
      urlImage.value = data.secure_url;
    }
  } catch (e) {
    console.log(e);
  }
}

function handleInput(e) {
  formElement.value = e.target.files[0];
  if(formElement === undefined){
    toast.error('try another type of image.',{
      autoClose:3000,
      closeButton:true,
    })
  }
  else{
    const reader = new FileReader();
    reader.onload = function(e){
      urlImage.value = e.target.result
    }
    reader.readAsDataURL(formElement.value)
  }
}
function handleDrag(e) {
  formElement.value = e.dataTransfer.files[0];
  if(formElement.value === undefined){
    toast.error('try another type of image.',{
      autoClose:3000,
      closeButton:true,
    })
  }
  else{
    const reader = new FileReader();
    reader.onload = function(e){
      urlImage.value = e.target.result
    }
    reader.readAsDataURL(formElement.value)
  }
    isDraging.value = false
}
function dragStyle() {
  isDraging.value= !isDraging.value
}
</script>
<template>
  <img
    :src="urlImage != '' ? urlImage : IMG_DEFAULT"
    alt="Default image"
  />
  <form @submit="handleSubmit">
    <label
      for="imagenInput"
      class="archive-input"
      :class="{'draging' : isDraging}"
      @dragenter.prevent="dragStyle"
      @dragleave.prevent="dragStyle"
      @dragover.prevent
      @drop.prevent="handleDrag"
    >
      Drop your Image:
      <DropSvg v-if="!formElement?.name" :isDraging='isDraging'/>
      <span v-html="formElement?.name"></span>
    </label>
    <input type="file" @change="handleInput" id="imagenInput" />
    <Links :urlImage="urlImage"/>
  </form>
</template>
<style scoped>
img {
  width: 50vw;
  max-height: 40vh;
  margin: 1rem;
  margin-top: 0;
  border-radius: 10px;
}
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 50vw;
  height: max-content;
  margin: 0;
}
.archive-input {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 50vw;
  height: 20vh;
  color: #fefefe;
  background-color: #00000054;
  border-radius: 10px;
  transition: all ease .2s;
  cursor: pointer;
}
.draging {
  background-color: #00000068;
}
.draging-item {
  fill: #00b52e;
}
span {
  font-size: 1.2rem;
  font-weight: bold;
}
input[type="file"] {
  display: none;
}
article {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  width: 50vw;
  margin: 1rem;
}
.copy {
  height:7.6vh;
  position: absolute;
  right: 485px;
  bottom: 68px;
  transition: all ease .2s;
  cursor: pointer;
  padding:.2rem;
  background-color:#00000000;
  border-radius:0 10px 10px 0;
}
.copy:hover {
  background-color:#00000066;
}
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
</style>
