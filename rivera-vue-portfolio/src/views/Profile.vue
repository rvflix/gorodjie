<template>
  <div class="profile">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
      <button class="go-back" @click="goBack">Go Back to Dashboard</button>
    </header>
    <h1>Welcome to My Profile!</h1> <!-- New welcome message -->
    <img :src="profilePhoto" alt="Profile Photo" class="profile-photo" />
    <div class="details">
      <h2>{{ name }}</h2>
      <p>Age: {{ age }}</p>
      <p>Location: {{ location }}</p>
      <p>Occupation: {{ occupation }}</p>
      <p><strong>Bio:</strong> {{ bio }}</p>
    </div>
    <div class="courses">
      <h3>Courses Enrolled</h3>
      <ul>
        <li v-for="course in courses" :key="course">{{ course }}</li>
      </ul>
    </div>
    <div class="skills">
      <h3>Skills</h3>
      <ul>
        <li v-for="skill in skills" :key="skill">{{ skill }}</li>
      </ul>
    </div>
    <div class="social-links">
      <h3>Connect with Me</h3>
      <a v-for="link in socialLinks" :key="link.name" :href="link.url" target="_blank">{{ link.name }}</a>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import profilePhoto from '@/assets/profile.jpg';

const router = useRouter();

const name = 'Gabriel Rivera';
const age = 22;
const location = 'Manila';
const occupation = 'Student';
const bio = 'A passionate learner with a keen interest in technology and design.';

const courses = [
  'CPE 400 Embedded Systems',
  'CPE 405 Microprocessors',
  'CPE 406 CpE Design 1',
  'CPE 407 Computer Networks Design',
  'CPE 416 Digital Signal Processing and Application',
  'GEC 002 Readings in Philippine History',
  'GEC 007 Science, Technology and Society',
];

const skills = [
  'C++',
  'Vue.js',
  'Python',
  'Problem Solving',
];

const socialLinks = [
  { name: 'Facebook', url: 'https://www.facebook.com/profile.php?id=100006452162071' },
  { name: 'Instagram', url: 'https://www.instagram.com/grbg.gb/' },
];

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
.profile {
  text-align: center;
  padding: 2rem;
  background-color: #101446; /* Dark background color */
  min-height: 100vh; /* Ensure it covers full height */
}

.header {
  display: flex; /* Use flexbox for header layout */
  justify-content: space-between; /* Space between logout and go back buttons */
  align-items: center; /* Center items vertically */
}

h1 {
  font-size: calc(2.5rem); /* Increase size for the welcome message */
  margin-bottom: 20px; /* Add space below the welcome message */
}

.profile-photo {
  width: 250px; /* Adjust size as needed */
  border-radius: 50%; /* Circular profile photo */
  box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.5); /* Shadow effect */
}

.details {
  background-color: rgba(255, 255, 255, 0.1); /* Slightly transparent background */
  border-radius: 10px; /* Rounded corners */
  padding: 1rem; /* Padding around the details */
  margin-top: 1rem; /* Space above details */
}

.details:hover {
  background-color: rgba(255, 255, 255, 0.2); /* Darken background on hover */
}

h2 {
  font-size: calc(3rem); /* Increase size of the name heading by an additional rem */
}

p {
  font-size: 1.5rem; /* Increase size of paragraph text */
}

.courses,
.skills {
   margin-top: 2rem; 
   text-align: left; 
   background-color: rgba(255,255,255,0.1); 
   border-radius:10px; 
   padding:1rem;
}

.courses h3,
.skills h3 {
   font-size:1.5rem;
}

.social-links {
   font-size:1rem;
   margin-top:2rem; 
}

.social-links a {
   font-size:1rem;
   margin:0 10px;
}

.logout-link {
   color: blue; /* Change the color of the logout link to blue */
}

.go-back {
   margin-left:auto; 
   background-color:#2600ff; 
   color:white; 
   border-radius:4px; 
   border:none; 
   padding:.5rem; 
   cursor:pointer; 
}
.go-back:hover {
   background-color:#0056b3; 
}
</style>