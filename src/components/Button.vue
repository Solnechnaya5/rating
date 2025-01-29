<template>
    <button class="btn-main">{{ btnTitle }}</button>
</template>

<script setup lang="ts">
defineProps<{
  btnTitle?: string
}>()
</script>
<style >
.btn-main{
    display: flex;
    justify-content: center;
align-items: center;
gap: 10;

font-family: 'Formular';
font-size: 14px;
font-weight: 500;
line-height: 22px;
text-align: center;
padding: 10px 20px 10px 20px;
box-sizing: border-box;
border-radius: 8px;
background: linear-gradient(90.00deg, rgb(230, 247, 245),rgb(248, 252, 252) 100%);

}
.btn-main:hover{
color: rgb(255, 255, 255);
background: rgb(54, 168, 160);
}
@media(max-width: 576px){
   .btn-main{
    width: 100%;
   }
   
  }
</style>