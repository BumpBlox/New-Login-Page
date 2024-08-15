<template>
  <div class="login-container">
    <div class="login-box">
      <h1>Login</h1>
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="username">Username:</label>
          <input type="text" id="username" v-model="username" required />
        </div>
        <div class="form-group">
          <label for="password">Password:</label>
          <input type="password" id="password" v-model="password" required />
        </div>
        <button type="submit" class="login-button">Login</button>
        <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const username = ref('');
const password = ref('');
const errorMessage = ref('');

function submitForm() {
  if (username.value === '' || password.value === '') {
    errorMessage.value = 'Both fields are required!';
    return;
  }
  // Handle form submission logic
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #325487;
}

.login-box {
  background-color: #28426a;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.2);
  text-align: center;
  width: 100%;
  max-width: 400px;
}

h1 {
  font-family: 'Roboto', sans-serif;
  font-weight: 700;
  color: #f7f9fc;
  margin-bottom: 2rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

label {
  font-family: 'Roboto', sans-serif;
  font-weight: 400;
  color: #f7f9fc;
  display: block;
  margin-bottom: 0.5rem;
}

input[type="text"],
input[type="password"] {
  width: 100%;
  padding: 0.75rem;
  border-radius: 4px;
  border: 1px solid #3a3a3a;
  background-color: #222;
  color: #f9f9f9;
  font-family: 'Roboto', sans-serif;
  font-size: 1rem;
}

input[type="text"]::placeholder,
input[type="password"]::placeholder {
  color: #f7f9fc;
}

input[type="text"]:focus,
input[type="password"]:focus {
  outline: none;
  border-color: #f7f9fc;
}

.login-button {
  width: 100%;
  padding: 0.75rem;
  border: none;
  border-radius: 4px;
  background-color: #f7f9fc;
  color: #1c1c1c;
  font-family: 'Roboto', sans-serif;
  font-weight: 700;
  font-size: 1.1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.login-button:hover {
  background-color: #f7f9fc;
}

.error-message {
  margin-top: 1rem;
  color: #ff4c4c;
  font-family: 'Roboto', sans-serif;
  font-weight: 400;
}

@media (max-width: 768px) {
  .login-box {
    padding: 1.5rem;
  }

  h1 {
    font-size: 1.5rem;
    margin-bottom: 1.5rem;
  }
}
</style>
