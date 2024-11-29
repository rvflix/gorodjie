<template>
  <div class="login-background">
    <div class="login-container">
      <h2>Welcome to Login Page</h2>
      <form @submit.prevent="handleLogin">
        <div class="form-group">
          <label for="username">Username:</label>
          <input 
            type="text" 
            id="username" 
            v-model="username" 
            required 
            placeholder="Enter your username" 
          />
        </div>
        <div class="form-group">
          <label for="password">Password:</label>
          <input 
            type="password" 
            id="password" 
            v-model="password" 
            required 
            placeholder="Enter your password" 
          />
        </div>
        <button type="submit" :disabled="isLoading">Login</button>
        <div v-if="isLoading" class="loading-indicator">Loading...</div>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const username = ref('');
const password = ref('');
const isLoading = ref(false);
const router = useRouter();

const handleLogin = async () => {
  const validUsername = 'gorodjie@gmail.com';
  const validPassword = 'rvflix08';

  if (username.value === validUsername && password.value === validPassword) {
    isLoading.value = true;
    await new Promise(resolve => setTimeout(resolve, 2000));
    alert('Login Successful!');
    await router.push('/dashboard');
  } else {
    alert('Invalid credentials, please try again.');
  }
};
</script>

<style scoped>
.login-background {
  background-image: url('@/assets/background.gif');
  background-size: cover;
  background-position: center;
  height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  top: 0;
  left: 0;
  backdrop-filter: blur(4px); /* Add a slight blur for a modern look */
}

.login-container {
  max-width: 400px;
  padding: 2rem;
  border: 1px solid #a3d5ff;
  border-radius: 10px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
  background-color: rgba(30, 30, 30, 0.85); /* Darker and more transparent */
  transition: transform 0.3s, box-shadow 0.3s; /* Smooth transitions */
}

.login-container:hover {
  transform: scale(1.03); /* Slight zoom on hover */
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.6); /* Enhance shadow on hover */
}

h2 {
  font-family: 'Impact', Haettenschweiler, 'Arial Narrow Bold', sans-serif;
  text-align: center;
  color: #83a0ff;
  font-size: 1.8rem;
  margin-bottom: 1rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: bold;
  color: #ffffff;
  font-size: 0.9rem;
}

input {
  width: 100%;
  padding: 0.6rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
  transition: border-color 0.3s;
}

input:focus {
  border-color: #83a0ff;
  outline: none;
  box-shadow: 0 0 5px rgba(131, 160, 255, 0.5); /* Focus glow */
}

button {
  width: 100%;
  padding: 0.8rem;
  background-color: #020496;
  color: #fff;
  border: none;
  border-radius: 5px;
  font-size: 1rem;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s;
}

button:hover {
  background-color: #0056b3;
  transform: scale(1.02);
}

button:disabled {
  background-color: #aaa;
  cursor: not-allowed;
}

.loading-indicator {
  text-align: center;
  margin-top: 10px;
  color: #fff;
  font-size: 0.9rem;
  animation: pulse 1s infinite;
}

@keyframes pulse {
  0%, 100% {
    opacity: 0.6;
  }
  50% {
    opacity: 1;
  }
}

@media (max-width: 768px) {
  .login-container {
    padding: 1.5rem;
  }

  h2 {
    font-size: 1.5rem;
  }

  button {
    font-size: 0.9rem;
  }
}
</style>
