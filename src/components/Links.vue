<script setup>
import CopyButton from "./CopyButton.vue";
import CreateLinkButton from "./CreateLinkButton.vue";
const props = defineProps(['urlImage'])
</script>
<template>
    <article>
      <label for="url" class="title">Your Link: </label>
      <article id="url">
        <a
          :href="urlImage"
          target="_blank"
          v-html="urlImage"
        ></a>
        <CopyButton />
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
</style>