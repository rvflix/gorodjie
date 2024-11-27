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
emailjs.init('GDOWu0bw1EUepiPZZ'); // Replace with your actual public key

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
  emailjs.send('grbg.gab', 'template_erv7jsq', templateParams)
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
  { name: 'Facebook', url: 'https://www.facebook.com/profile.php?id=100006452162071' },
  { name: 'Instagram', url: 'https://www.instagram.com/grbg.gb/' },
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
  padding: 2rem;
  
  /* Fullscreen settings */
  background-image: url('@/assets/background.gif'); /* Background GIF */
  background-size: cover; /* Cover the entire area */
  background-position: center; /* Center the image */
  position: fixed; /* Fixed positioning to cover entire screen */
    top: 0; /* Align to top */
    left: 0; /* Align to left */
  min-height: 100vh; /* Ensure it covers full height */
  width: 100vw; /* Full width */
  
  display: flex; /* Use flexbox for layout */
  flex-direction: column; /* Stack children vertically */
}

.header {
  display: flex; /* Use flexbox for header layout */
  justify-content: space-between; /* Space between logout and go back buttons */
  align-items: center; /* Center items vertically */
  padding: .5rem; /* Add padding for better spacing */
}

h2 {
  color:rgb(229, 229, 231);
  font-size: 3rem; /* Increase font size for the heading */
  background-color: rgba(48, 48, 48, 0.781);
  
}

p {
  color: rgb(229, 229, 231);
  background-color: rgba(48, 48, 48, 0.781);
  font-size: calc(1.5rem); /* Increase size of paragraph text */
}

.contact-form {
   color: rgb(229, 229, 231); /* Set color for paragraph text */
   background-color: rgba(48, 48, 48, 0.781); /* Slightly transparent background for form area */
   border-radius:10px; /* Rounded corners */
   padding:2rem; /* Padding inside the form area */
   margin-top: calc(20px); /* Space above the form area */
   height: 400px;
   width: 700px; 
   max-width:700px; /* Set a maximum width for consistency */
   box-shadow: 0px 4px 15px rgba(0,0,0,0.5); /* Shadow effect for depth */

   align-self: center; /* Center the form horizontally within contact container */
}

.form-group {
   margin-bottom: 15px;
}

.row {
   display: flex; /* Use flexbox for row layout */
   justify-content: space-between; /* Space between input groups */
}

.input-group {
   flex: 1; /* Allow input groups to grow equally */
   margin-right: 10px; /* Space between input groups */
}

.input-group:last-child {
   margin-right: 0; /* Remove margin from last input group */
}

input, textarea {
   width: calc(100% - 10px); /* Full width minus padding */
   border-radius:4px; /* Rounded corners for inputs and textarea */
   border:none; /* No border style */
   padding:.5rem; /* Padding inside inputs and textarea */
}

textarea {
   height: 150px; /* Increased height for message box */
}

button {
   margin-top: 1rem; /* Space above the button */
   background-color:#2600ff; 
   color:white;
   border:none;
   border-radius:4px;
   padding:.5rem .75rem;
   cursor:pointer;
}
button:hover {
   background-color:#0056b3; 
}

.social-links {
   margin-top: 2rem; /* Space above social links */
}

.social-links a {
   margin: 0 10px;
}

.logout-link,
.go-back {
   background-color:#2600ff; 
   color:white; 
   border-radius:4px; 
   border:none; 
   padding:.5rem .75rem; 
   cursor:pointer; 
}
.logout-link:hover,
.go-back:hover {
   background-color:#0056b3; 
}
</style>