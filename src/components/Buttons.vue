<script setup lang="ts">
import { ref } from "vue";
import Button from "./Button.vue";
import PopUpForm from "./PopUpForm.vue";

const isPopupOpen = ref(false);
</script>

<template>
  <div class="rating-btns">
    <a href="https://www.google.com" target="_blank">
      <Button btnTitle="Переглянути" />
    </a>
    <Button btnTitle="Написати" class="btn-gradient" @click="isPopupOpen = true" />
  </div>

  <PopUpForm :isOpen="isPopupOpen" @close="isPopupOpen = false" />
</template>

<style scoped>
.btn-gradient {
  color: white;
  background: linear-gradient(90deg, rgb(60, 185, 160), rgb(23, 134, 172));
  background-size: 150% 150%;
  animation: gradient-animation 2s ease infinite;
  margin-left: 10px;
}

@keyframes gradient-animation {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.btn-gradient:hover {
  background: rgb(54, 168, 160);
}

.rating-btns {
  display: flex;
}

.rating-btns a {
  text-decoration: none;
}
@media(max-width: 576px){
 .rating-btns{
  flex-direction: column;
  width: 100%;
  margin-top: 20px;
 }
 .btn-main.btn-gradient{
    margin: 10px 0 0 0;
   }
}
</style>
