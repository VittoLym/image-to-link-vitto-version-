<script setup>
import { ref } from "vue";
import Links from "./Links.vue";
import LoaderUI from "./LoaderUI.vue";
import DropFile from "./DropFile.vue";
const IMG_DEFAULT = import.meta.env.VITE_DEFAULT_IMAGE;
const urlImage = ref(IMG_DEFAULT)
const vtest = ref(true)
const formElement = ref('')
const KEY = import.meta.env.VITE_API_SECRET;
const ENDPOINT_CLOUD = import.meta.env.VITE_CLOUDINARY_URL;

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

function eraseDrop(e){
  console.log(e)
}
</script>
<template>
  <img
    v-if="vtest"
    :src="urlImage"
    alt="Default image"
  />
  <LoaderUI v-else/>
  <form @submit="handleSubmit">
    <DropFile @urlImage=" urlImage = $event" @vtest="vtest = $event" @formElement="formElement = $event"/>
    <Links :urlImage="urlImage"/>
  </form>
</template>
<style scoped>
img {
  width: 50vw;
  height: 34vh;
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
article {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  width: 50vw;
  margin: 1rem;
}
</style>
