<script setup>
import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';
const props = defineProps(['isDisabled'])
function copyLink(e) {
  e.preventDefault();
  const urlCopy = document.getElementById("link");
  if(urlCopy != null && props.isDisabled === false){
    navigator.clipboard.writeText(urlCopy.text);
    toast.success('was copied successfully',{
      autoClose:500,
    });
  }
  else{
    toast.warning('Please create link first',{
      autoClose:500,
    })
  }
}
</script>
<template>
    <button :class="{'isDisabled': props.isDisabled}" class="copy" @click="copyLink" >
  <span>
    <svg xml:space="preserve" style="enable-background:new 0 0 512 512" viewBox="0 0 6.35 6.35"  xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" xmlns="http://www.w3.org/2000/svg" class="clipboard">
      <g>
        <path fill="currentColor" d="M2.43.265c-.3 0-.548.236-.573.53h-.328a.74.74 0 0 0-.735.734v3.822a.74.74 0 0 0 .735.734H4.82a.74.74 0 0 0 .735-.734V1.529a.74.74 0 0 0-.735-.735h-.328a.58.58 0 0 0-.573-.53zm0 .529h1.49c.032 0 .049.017.049.049v.431c0 .032-.017.049-.049.049H2.43c-.032 0-.05-.017-.05-.049V.843c0-.032.018-.05.05-.05zm-.901.53h.328c.026.292.274.528.573.528h1.49a.58.58 0 0 0 .573-.529h.328a.2.2 0 0 1 .206.206v3.822a.2.2 0 0 1-.206.205H1.53a.2.2 0 0 1-.206-.205V1.529a.2.2 0 0 1 .206-.206z"></path>
      </g>
    </svg>
    <svg v-if="!props.isDisabled" xml:space="preserve" style="enable-background:new 0 0 512 512" viewBox="0 0 24 24"  xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" xmlns="http://www.w3.org/2000/svg" class="checkmark">
      <g>
        <path data-original="#000000" fill="currentColor" d="M9.707 19.121a.997.997 0 0 1-1.414 0l-5.646-5.647a1.5 1.5 0 0 1 0-2.121l.707-.707a1.5 1.5 0 0 1 2.121 0L9 14.171l9.525-9.525a1.5 1.5 0 0 1 2.121 0l.707.707a1.5 1.5 0 0 1 0 2.121z"></path>
      </g>
    </svg>
    <svg  v-else xml:space="preserve" style="enable-background:new 0 0 512 512" viewBox="0 0 6.35 6.35"  xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" xmlns="http://www.w3.org/2000/svg" class="checkmark">
      <g>
        <path fill="currentColor" d="M2.43.265c-.3 0-.548.236-.573.53h-.328a.74.74 0 0 0-.735.734v3.822a.74.74 0 0 0 .735.734H4.82a.74.74 0 0 0 .735-.734V1.529a.74.74 0 0 0-.735-.735h-.328a.58.58 0 0 0-.573-.53zm0 .529h1.49c.032 0 .049.017.049.049v.431c0 .032-.017.049-.049.049H2.43c-.032 0-.05-.017-.05-.049V.843c0-.032.018-.05.05-.05zm-.901.53h.328c.026.292.274.528.573.528h1.49a.58.58 0 0 0 .573-.529h.328a.2.2 0 0 1 .206.206v3.822a.2.2 0 0 1-.206.205H1.53a.2.2 0 0 1-.206-.205V1.529a.2.2 0 0 1 .206-.206z"></path>
      </g>
    </svg>
  </span>
</button>
</template>
<style scoped>
/* tooltip settings 👇 */

.copy {
  /* button */
  --button-hover-bg: #00000099;
  --button-text-color: #CCCCCC;
  --button-hover-text-color: #8bb9fe;
  --button-border-radius: 0;
  --button-diameter: 7.8vh;
  --button-outline-width: 1px;
  --button-outline-color: rgb(141, 141, 141);
  /* tooltip */
  --tooltip-bg: #f4f3f3;
  --toolptip-border-radius: 0;
  --tooltip-font-family: Menlo, Roboto Mono, monospace;
  /* 👆 this field should not be empty */
  --tooltip-font-size: 12px;
  /* 👆 this field should not be empty */
  --tootip-text-color: rgb(50, 50, 50);
  --tooltip-padding-x: 7px;
  --tooltip-padding-y: 7px;
  --tooltip-offset: 8px;
  /* --tooltip-transition-duration: 0.3s; */
  /* 👆 if you need a transition, 
  just remove the comment,
  but I didn't like the transition :| */
}
.copy {
  background-color:#00000056;
  box-sizing: content-box;
  border-radius:0 10px 10px 0;
  width: 6vw;
  height: 5vh;
  color: var(--button-text-color);
  border: none;
  cursor: pointer;
  display:flex;
  outline: none;
  padding: .6rem .3rem;
}
.isDisabled{
  background-color :#c0c0c056;
  box-sizing: content-box;
  border-radius:0 10px 10px 0;
  width: 6vw;
  height: 5vh;
  color: var(--button-text-color);
  border: none;
  cursor: pointer;
  display:flex;
  outline: none;
  padding: .6rem .3rem;
  cursor:not-allowed;
}
.copy span{
  height:100%;
  width:100%;
  display:flex;
  align-items:center;
  justify-content:center;
}
.copy svg {
  height:25px;
  width:25px;
}

.checkmark {
  display: none;
}

/* actions */

.copy:hover 
.copy:focus:not(:focus-visible) {
  opacity: 1;
  visibility: visible;
}

.copy:focus:not(:focus-visible) .clipboard {
  display: none;
}

.copy:focus:not(:focus-visible) .checkmark {
  display: block;
}

.copy:hover {
  background-color: var(--button-hover-bg);
}

.copy:active {
  outline: var(--button-outline-width) solid var(--button-outline-color);
}

.copy:hover svg {
  color: var(--button-hover-text-color);
}
.isDisabled:hover{
  background-color :#c0c0c056;
}

</style>