<template>
    <div class="login-background">
      <div class="login-container">
        <h2>Welcome to Login Page</h2>
        <form @submit.prevent="handleLogin">
          <div class="form-group">
            <label for="username">Username:</label>
            <input type="text" id="username" v-model="username" required />
          </div>
          <div class="form-group">
            <label for="password">Password:</label>
            <input type="password" id="password" v-model="password" required />
          </div>
          <button type="submit" :disabled="isLoading">Login</button>
          <!-- Loading indicator -->
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
  const isLoading = ref(false); // Loading state
  const router = useRouter();
  
  const handleLogin = async () => {
      const validUsername = 'admin123'; // Updated username
      const validPassword = 'admin';      // Updated password
  
      if (username.value === validUsername && password.value === validPassword) {
          isLoading.value = true; // Set loading state to true
          await new Promise(resolve => setTimeout(resolve, 2000)); // Simulate loading for 2 seconds
          alert('Login successful!'); // Alert for successful login
          await router.push('/dashboard'); // Redirect to Dashboard.vue upon successful login
      } else {
          alert('Invalid credentials, please try again.'); // Alert for invalid credentials
      }
  };
  </script>
  
  <style scoped>
  .login-background {
      background-image: url('@/assets/background.gif');
      background-size: cover; /* Cover the entire area */
      background-position: center; /* Center the image */
      height: 100vh; /* Full viewport height */
      width: 100vw; /* Full viewport width */
      display: flex; /* Flexbox for centering */
      align-items: center; /* Center vertically */
      justify-content: center; /* Center horizontally */
  }
  
  .login-container {
      max-width: 400px; /* Limit container width */
      padding: 2rem; /* Padding around the container */
      border: 1px solid #d3d3d3; /* Border around container */
      border-radius: 8px; /* Rounded corners */
      box-shadow: 0 2px 10px rgba(0,0,0,0.1); /* Shadow effect */
      background-color: rgba(185, 182, 182, 0.8); /* Semi-transparent background */
  }
  
  h2 {
      text-align: center; /* Center heading text */
  }
  
  .form-group {
      margin-bottom: 1rem; /* Space between form groups */
  }
  
  label {
      display: block; /* Block display for labels */
      margin-bottom:.5rem; /* Space below labels */
  }
  
  input {
      width: 100%; /* Full width inputs */
      padding:.5rem; /* Padding inside inputs */
      border:1px solid #ccc; /* Border around inputs */
      border-radius:4px; /* Rounded corners for inputs */
  }
  
  button {
      width:100%; /* Full width button */
      padding:.5rem; /* Padding inside button */
      background-color:#020496; /* Button background color */
      color:white; /* White text color for button */
      border:none; /* No border for button */
      border-radius:4px; /* Rounded corners for button */
  }
  
  button:hover {
     background-color:#0056b3; /* Darker shade on hover */
  }
  
  .loading-indicator {
     text-align: center;
     margin-top: 10px;
     color: white;
  }
  </style>