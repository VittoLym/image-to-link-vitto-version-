<script setup>
  import { ref } from 'vue'
  const KEY = import.meta.env.VITE_API_SECRET
  const ENDPOINT_CLOUD = import.meta.env.VITE_CLOUDINARY_URL
  const IMG_DEFAULT= import.meta.env.VITE_DEFAULT_IMAGE
  const formElement = ref('')
  const urlImage = ref(IMG_DEFAULT)

  async function handleSubmit(e){
    e.preventDefault();
    const formData = new FormData(); 
    try{
      if(formElement.value == '' ){
        urlImage.value = '' 
      }
      else{
        formData.append('file', formElement.value)
        formData.append("upload_preset", "bye1zwq8")
        formData.append('api_key', KEY)
        const response = await fetch(ENDPOINT_CLOUD,{method: 'POST', body:formData,})
        const data = await response.json()
        urlImage.value = data.secure_url
      }
    }
    catch(e){
      console.log(e)
    } 
  }
  function handleInput(e) {
    formElement.value = e.target.files[0]
    console.log(formElement.value)
  }
</script>

<template>
  <div>
    <h3>Imagen a Link</h3>
    <img :src="urlImage" alt="">
    <form @submit="handleSubmit">
      <label for="imagenInput"> Elegir Archivo: 
        <span v-html="formElement.name"></span>
      </label>
      <a :href="urlImage" target="_blank" v-html="urlImage ? urlImage : 'Todavia no genera una imagen.'"></a>
      <input type="file" @change="handleInput" id="imagenInput">
      <button>Create Link</button>
    </form>
  </div>
</template>
.
<style scoped>
div{/* 
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center; */
  border: 10px solid #20101060;
  border-radius: 10px;
  background-color: #00000028;
  height: 100vh;
  width: max-content;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  margin: 1rem 0;
}
div:hover{
  filter: blur(0);
}
a{
  width: 30vw;
  height: 5vh;
  line-height: 5vh;
  background-color: #00000054;
  border-radius: 10px;
  color: #fff;
  overflow: hidden;
  transition: all ease .2s;
  padding: 0 .3rem;
}
a:hover{
  color: #6a2dda;
  text-decoration: underline;
}
img{
  width: 30vw;
  max-height: 40vh;
  margin: 2rem 1rem;
  margin-top:0;
  border-radius: 10px;
}
form{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  height: 40vh;
  width: max-content;
  margin: 1rem 0;
}
label{
  width: 30vw;
  height: 20vh;
  background-color: #00000054;
  border-radius: 10px;
  color: #fff;
  display: flex;
  flex-direction: column;
  align-items: center;
}
span{
  font-weight: bold;
  font-size: 1.2rem;
}
input[type='file']{
  display: none;
}
h2{
  width: 60vw;
  overflow: hidden;
}
</style>
