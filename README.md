# Vue Project with Popup Form and Validation

## 📌 Опис проєкту
Цей проєкт створений на Vue 3 з використанням Composition API та `script setup`. Він містить компоненти кнопок та модального вікна (поп-ап), яке містить контактну форму з валідацією.

## 🚀 Функціонал
- Дві кнопки: одна веде на Google, друга відкриває поп-ап.
- Поп-ап із контактною формою.
- Валідація форми (перевірка на порожні поля, коректність email).
- Закриття поп-апу при натисканні на кнопку закриття або після успішного відправлення форми.
- Дані для рейтингу та відгуків тягнуться з **MockAPI** і змінюються при перезавантаженні.
- Зірки фарбуються відповідно до рейтингу (1 рейтинг = 1 зірка, 2 рейтинг = 2 зірки і т.д.).

## 📂 Структура проєкту
```
📁 src/
 ├── components/
 │   ├── Button.vue
 │   ├── Buttons.vue
 │   ├── PopUpForm.vue
 │   ├── ShowRating.vue
 ├── App.vue
 ├── main.ts
```

## 🛠 Технології
- Vue 3 (Composition API, `<script setup>`)
- TypeScript
- HTML / CSS / SCSS (Scoped styles)
- Vite
- MockAPI (для отримання даних рейтингу та відгуків)

## 📦 Встановлення та запуск
```bash
# Клонування репозиторію
git clone https://github.com/your-repo/vue-popup-project.git

# Перехід до папки проєкту
cd vue-popup-project

# Встановлення залежностей
npm install

# Запуск локального сервера
npm run dev
```

## 📝 Використання
### 🔹 Додавання поп-апу
```vue
<Popup :isOpen="isPopupOpen" @close="isPopupOpen = false" />
```

### 🔹 Відкриття поп-апу по кліку на кнопку
```vue
<Button btnTitle="Написати" @click="isPopupOpen = true" />
```
