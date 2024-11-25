<template>
  <div class="contact">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
      <button class="go-back" @click="goBack">Go Back to Dashboard</button>
    </header>
    <h2>To Contact Me, Kindly Leave A Message.</h2>
    <form @submit.prevent="handleSubmit">
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
  background-color: #101446; /* Dark background color */
  min-height: 100vh; /* Ensure it covers full height */
}

.header {
  display: flex; /* Use flexbox for header layouat */
  justify-content: space-between; /* Space between logout and go back buttons */
  align-items: center; /* Center items vertically */
}

h2 {
  font-size: 2rem; /* Increase font size for the heading */
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
}

textarea {
  height: 150px; /* Increased height for message box */
}

button {
  margin-top: 1rem; /* Space above the button */
}

.social-links {
  margin-top: 2rem; /* Space above social links */
}

.social-links a {
  margin: 0 10px;
}

.logout-link {
  color: blue; /* Change the color of the logout link to blue */
}
.go-back {
   margin-left: auto; /* Pushes the Go Back button to the right */
   background-color: #2600ff; /* Background color for Go Back button */
   color: white; /* Text color for Go Back button */
   border-radius: 4px; /* Rounded corners */
   border: none; /* No border */
   padding: .5rem; /* Padding for button */
   cursor:pointer; /* Pointer cursor on hover */
}
.go-back:hover {
   background-color:#0056b3; /* Darker shade on hover */
}
</style>