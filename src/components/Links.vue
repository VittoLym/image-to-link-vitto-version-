<script setup>
import { ref, onUpdated} from "vue";
import CopyButton from "./CopyButton.vue";
import CreateLinkButton from "./CreateLinkButton.vue";
const props = defineProps(['linkImage'])
const isDisabled = ref(false);

onUpdated(() => {
  if(props.linkImage == 'Create your link.'){
    isDisabled.value = true
  }
  else{
    isDisabled.value = false
  }
})
</script>
<template>
    <article>
      <label for="url" class="title">Your Link: </label>
      <article id="url">
        <p v-if="linkImage == 'Creating your link, please wait.'">
          <div class="loader">
            <span class="bar"></span>
            <span class="bar"></span>
            <span class="bar"></span>
          </div>
          {{ linkImage }}
        </p>
        <p v-else-if="linkImage == 'Create your link.'">{{ linkImage }}</p>
        <a
          v-else
          id="link"
          :href="linkImage"
          target="_blank"
          v-html="linkImage"
        ></a>
        <CopyButton :isDisabled="isDisabled"/>
      </article>
      <CreateLinkButton/>
    </article>
</template>
<style scoped>

.title {
  width: 50vw;
  margin-bottom: .6rem;
  font-weight: bolder;
}
#url{
    width:35vw;
    max-width:80%;
    display:flex;
    justify-content:start;
    align-items:start;
}
a {
  overflow: hidden;
  text-overflow:ellipsis;
  height: 5vh;
  width:85%;
  padding: .6rem .3rem;
  color: #fefefe;
  line-height: 5vh;
  border-radius: 10px 0 0 10px;
  transition: all ease .2s;
  background-color:#00000054;
}
a:hover {
  color: #6a2dda;
  text-decoration: underline;
}
p{
  display:flex;
  justify-content:start;
  overflow: hidden;
  text-overflow:ellipsis;
  height: 5vh;
  width:85%;
  padding: .6rem 1rem;
  color: #fefefe;
  line-height: 5vh;
  border-radius: 10px 0 0 10px;
  transition: all ease .2s;
  background-color:#00000054;
  margin:0;
}

.loader {
  display: flex;
  align-items: center;
  width:min-content;
  margin-right: 1rem;
}

.bar {
  display: inline-block;
  width: 3px;
  height: 20px;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 10px;
  animation: scale-up4 1s linear infinite;
}

.bar:nth-child(2) {
  height: 35px;
  margin: 0 5px;
  animation-delay: 0.25s;
}

.bar:nth-child(3) {
  animation-delay: 0.5s;
}

@keyframes scale-up4 {
  20% {
    background-color: #ffff;
    transform: scaleY(1.5);
  }

  40% {
    transform: scaleY(1);
  }
}
</style>