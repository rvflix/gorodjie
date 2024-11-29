<template>
  <div class="contact">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
      <button class="go-back" @click="goBack">Go Back to Dashboard</button>
    </header>
    <h2>To Contact Me, Kindly Leave A Message.</h2>
    <p>This message will be directed to my email.</p>
    <form @submit.prevent="handleSubmit" class="contact-form">
      <div class="form-group row">
        <div class="input-group">
          <label for="name">Name:</label>
          <input type="text" id="name" v-model="name" required />
        </div>
        <div class="input-group">
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="email" required />
        </div>
      </div>
      <div class="form-group">
        <label for="message">Message:</label>
        <textarea id="message" v-model="message" required></textarea>
      </div>
      <button type="submit">Send Message</button>
    </form>

    <!-- Social Links Section -->
    <div class="social-links">
      <h3>Connect with Me</h3>
      <a v-for="link in socialLinks" :key="link.name" :href="link.url" target="_blank">{{ link.name }}</a>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import emailjs from '@emailjs/browser';

// Initialize EmailJS with your public key
emailjs.init('Pww8VkAF4sdB3pjv_'); // Replace with your actual public key

const router = useRouter();

const name = ref('');
const email = ref('');
const message = ref('');

// Function to handle form submission
const handleSubmit = () => {
  const templateParams = {
    user_name: name.value,
    user_email: email.value,
    message: `From: ${name.value} (${email.value})\n\nMessage:\n${message.value}`,
  };

  // Send the email using EmailJS
  emailjs.send('service_wyb9rab', 'template_j2w7ljc', templateParams)
    .then((response) => {
      alert('Message sent successfully!');
      // Clear the form fields
      name.value = '';
      email.value = '';
      message.value = '';
    }, (error) => {
      alert('Failed to send message, please try again.');
      console.error('EmailJS Error:', error);
    });
};

// Social links data
const socialLinks = [
  { name: 'Facebook', url: 'https://www.facebook.com/rodjieven.f.go' },
  { name: 'Instagram', url: 'https://www.instagram.com/rv_flrsgo/profilecard/?igsh=Y3lpMXg1Y3QzZGMz' },
];

// Function to navigate back to the dashboard
const goBack = () => {
  router.push('/dashboard'); // Navigate to the dashboard
};

// Function to log out
const logout = async () => {
  const confirmed = window.confirm("Are you sure you want to log out?"); // Use window.confirm for clarity
  if (confirmed) {
    await new Promise(resolve => setTimeout(resolve, 2000)); // Simulate loading for 2 seconds
    await router.push('/'); // Redirect to the login page
  }
};
</script>

<style scoped>
.contact {
  text-align: center;
  padding: 1rem;
  
  /* Fullscreen settings */
  background-image: url('@/assets/background.gif'); /* Background GIF */
  background-size: cover; /* Cover the entire area */
  background-position: center; /* Center the image */
  position: fixed; /* Fixed positioning to cover entire screen */
  top: 0; /* Align to top */
  left: 0; /* Align to left */

  width: 100vw; /* Full width */
  height: 100vh; /* Full height */
  
  display: flex; /* Use flexbox for layout */
  flex-direction: column; /* Stack children vertically */
  justify-content: flex-start; /* Start content at the top */
  align-items: center; /* Center content horizontally */
  
  overflow-y: auto; /* Enable vertical scrolling */
  overflow-x: hidden; /* Disable horizontal scrolling */
  scroll-behavior: smooth; /* Smooth scrolling effect */
}

.header {
  display: flex; /* Use flexbox for header layout */
  justify-content: space-between; /* Space between logout and go back buttons */
  align-items: center; /* Center items vertically */
  width: 100%; /* Ensure header spans the full width */
  padding: 1rem;
  z-index: 10;
  background-color: rgba(48, 48, 48, 0.8); /* Add a background to the header for better readability */
  position: sticky; /* Make header stick to the top when scrolling */
  top: 0; /* Align to the top of the viewport */
}

h2 {
  color: rgb(229, 229, 231);
  font-size: 2rem; /* Slightly reduced font size */
  background-color: rgba(48, 48, 48, 0.7); /* Semi-transparent background */
  padding: 1rem;
  border-radius: 8px; /* Rounded corners */
  margin-top: 1rem;
  max-width: 80%; /* Make the heading text more compact */
}

p {
  color: rgb(229, 229, 231);
  background-color: rgba(48, 48, 48, 0.7);
  font-size: 1.2rem; /* Slightly reduced font size */
  padding: 0.75rem;
  border-radius: 8px;
  margin-top: 0.5rem;
  max-width: 80%;
}

.contact-form {
  background-color: rgba(48, 48, 48, 0.7); /* Slightly transparent background for form area */
  color: rgb(229, 229, 231); /* Set color for text */
  padding: 1.5rem;
  border-radius: 10px;
  margin-top: 2rem;
  max-width: 500px; /* Reduced width for better fitting */
  width: 100%;
  box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.5); /* Shadow effect for depth */
}

.form-group {
  margin-bottom: 12px; /* Reduced space between form fields */
}

.row {
  display: flex; /* Use flexbox for row layout */
  justify-content: space-between; /* Space between input groups */
  flex-wrap: wrap; /* Allow wrapping of input groups */
}

.input-group {
  flex: 1; /* Allow input groups to grow equally */
  margin-right: 8px; /* Space between input groups */
}

.input-group:last-child {
  margin-right: 0; /* Remove margin from last input group */
}

input, textarea {
  width: 100%; /* Full width */
  padding: 0.75rem;
  border-radius: 5px;
  border: 1px solid #ccc; /* Add border to input fields */
  background-color: rgba(255, 255, 255, 0.9); /* Light background color */
  font-size: 1.2rem; /* Larger text for better readability */
  margin-bottom: 12px; /* Space between input fields */
}

textarea {
  height: 120px; /* Reduced height for the textarea */
  resize: vertical; /* Allow resizing of textarea */
}

button {
  background-color: #2600ff;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 0.75rem 1.5rem;
  font-size: 1.2rem;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
  margin-top: 1rem;
}

button:hover {
  background-color: #0056b3; /* Darken the button color on hover */
  transform: scale(1.05); /* Slight zoom effect on hover */
}

button:focus {
  outline: none;
  box-shadow: 0 0 0 4px rgba(0, 123, 255, 0.5); /* Outline effect when focused */
}

.social-links {
  margin-top: 1rem; /* Space above social links */
  display: flex; /* Arrange links horizontally */
  justify-content: center; /* Center links */
  gap: 15px; /* Space between links */
}

.social-links h3 {
  font-size: 1.2rem; /* Font size for social links title */
  color: rgb(229, 229, 231);
}

.social-links a {
  margin: 0;
  color: rgb(229, 229, 231); /* Color for social links */
  font-size: 1.2rem; /* Font size for links */
  text-decoration: none;
  transition: color 0.3s ease;
}

.social-links a:hover {
  color: #2600ff; /* Color change on hover */
}

.logout-link,
.go-back {
  background-color: #2600ff;
  color: white;
  border-radius: 5px;
  border: none;
  padding: 0.75rem 1.5rem;
  font-size: 1.2rem;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.logout-link:hover,
.go-back:hover {
  background-color: #0056b3;
  transform: scale(1.05); /* Slight zoom effect on hover */
}

.logout-link:focus,
.go-back:focus {
  outline: none;
  box-shadow: 0 0 0 4px rgba(0, 123, 255, 0.5); /* Outline effect when focused */
}
</style>
