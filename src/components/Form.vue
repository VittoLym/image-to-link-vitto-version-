<script setup>
import { ref } from "vue";
const KEY = import.meta.env.VITE_API_SECRET;
const ENDPOINT_CLOUD = import.meta.env.VITE_CLOUDINARY_URL;
const IMG_DEFAULT = import.meta.env.VITE_DEFAULT_IMAGE;
const formElement = ref("");
const urlImage = ref(IMG_DEFAULT);

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
}
function copyLink() {
  const urlCopy = document.getElementById('url')
  navigator.clipboard.writeText(urlCopy);
}
</script>
<template>
  <img
    :src="urlImage != '' ? urlImage : IMG_DEFAULT"
    alt="imagen base para link"
  />
  <form @submit="handleSubmit">
    <label for="imagenInput" class='archive-input'>
      Elegir Archivo:
      <span v-html="formElement.name"></span>
    </label>
    <input type="file" @change="handleInput" id="imagenInput" />
    <article >
    <label for='url' class='title'>Tu Link: </label>
      <a
        id='url'
        :href="urlImage"
        target="_blank"
        v-html="urlImage ? urlImage : 'Todavia no ingresa una imagen.'"
      ></a>
      <svg @click='copyLink' width="48px" height="48px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M6 11C6 8.17157 6 6.75736 6.87868 5.87868C7.75736 5 9.17157 5 12 5H15C17.8284 5 19.2426 5 20.1213 5.87868C21 6.75736 21 8.17157 21 11V16C21 18.8284 21 20.2426 20.1213 21.1213C19.2426 22 17.8284 22 15 22H12C9.17157 22 7.75736 22 6.87868 21.1213C6 20.2426 6 18.8284 6 16V11Z" stroke="#1C274C" stroke-width="1.5"></path> <path d="M6 19C4.34315 19 3 17.6569 3 16V10C3 6.22876 3 4.34315 4.17157 3.17157C5.34315 2 7.22876 2 11 2H15C16.6569 2 18 3.34315 18 5" stroke="#1C274C" stroke-width="1.5"></path> </g></svg>
      <button>Create Link</button>
    </article>
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
form{
  display: flex;
  flex-direction: column;
  align-items: center;
  height: max-content;
  width: 50vw;
  margin: 0;
}
.archive-input{
  width: 50vw;
  height: 20vh;
  background-color: #00000054;
  border-radius: 10px;
  color: #fff;
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor:pointer;
}
span{
  font-weight: bold;
  font-size: 1.2rem;
}
input[type='file']{
  display: none;
}
article{
  display:flex;
  width:50vw;
  justify-content:space-between;
  margin: 1rem;
  flex-wrap:wrap;
}
svg{
  position:absolute;
  right:490px;
  bottom:70px;
  cursor:pointer;
  transition: all ease .2s;
}
svg:hover{
  transform:scale(1.1);
}
.title{
  width:50vw;
  margin-bottom:.6rem ;
  font-weight:bolder;
}
a{
  width: 37vw;
  height: 5vh;
  line-height: 5vh;
  background-color: #00000054;
  border-radius: 10px;
  color: #fff;
  overflow: hidden;
  transition: all ease .2s;
  padding: 0.6rem .3rem;
}
a:hover{
  color: #6a2dda;
  text-decoration: underline;
}
</style>
