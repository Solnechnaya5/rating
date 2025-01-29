<script setup lang="ts">
import { ref } from "vue";

defineProps<{ isOpen: boolean }>();
const emit = defineEmits(["close"]);

const name = ref("");
const email = ref("");
const message = ref("");
const errors = ref<{ name?: string; email?: string; message?: string }>({});

const validateForm = () => {
  errors.value = {};

  if (!name.value.trim()) {
    errors.value.name = "Введіть ваше ім'я";
  }

  if (!email.value.trim()) {
    errors.value.email = "Введіть вашу електронну пошту";
  } else if (!/\S+@\S+\.\S+/.test(email.value)) {
    errors.value.email = "Невірний формат електронної пошти";
  }

  if (!message.value.trim()) {
    errors.value.message = "Введіть повідомлення";
  }

  return Object.keys(errors.value).length === 0;
};

const submitForm = () => {
  if (validateForm()) {
    console.log("Форма відправлена", {
      name: name.value,
      email: email.value,
      message: message.value,
    });

    name.value = "";
    email.value = "";
    message.value = "";
    errors.value = {};
    emit("close");
  }
};
</script>

<template>
  <div v-if="isOpen" class="pop-up">
    <span class="close-btn" @click="emit('close')">X</span>
    <form @submit.prevent="submitForm" class="contact-form">
      <div class="form-group">
        <input v-model="name" type="text" placeholder="Повне ім'я" />
        <span v-if="errors.name" class="error-msg">{{ errors.name }}</span>
      </div>

      <div class="form-group">
        <input v-model="email" type="email" placeholder="Контактний email" />
        <span v-if="errors.email" class="error-msg">{{ errors.email }}</span>
      </div>

      <div class="form-group">
        <textarea v-model="message" placeholder="Повідомлення..."></textarea>
        <span v-if="errors.message" class="error-msg">{{
          errors.message
        }}</span>
      </div>

      <button type="submit" class="submit-btn">Відправити</button>
    </form>
  </div>
</template>

<style scoped>
.pop-up {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  padding: 20px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.3);
  border-radius: 8px;
  z-index: 1000;
  width: 600px;
}

.close-btn {
  cursor: pointer;
  color:#2fa087;
  font-size: 20px;
  font-weight: bold;
  position: absolute;
  top: 10px;
  right: 15px;
}
.close-btn:hover{
    color: rgb(190, 10, 10);
}

.contact-form {
  display: flex;
  flex-direction: column;
}
.form-group {
  margin: 10px 0;
}
.contact-form input,
.contact-form textarea {
  width: 100%;
  padding: 10px;
  margin-bottom: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.error-msg {
  color: rgb(190, 10, 10);
  font-size: 12px;
  margin-top: -8px;
}

.submit-btn {
  background: #3cb9a0;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
}

.submit-btn:hover {
  background: #2fa087;
}
@media (max-width: 1024px){
  .pop-up {
    top: 30%;
  }
}
@media (max-width: 566px) {
  .pop-up {
    width: 280px;
    top: 30%;
  }
  
}
</style>
