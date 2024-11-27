<template>
  <div class="profile">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
      <button class="go-back" @click="goBack">Go Back to Dashboard</button>
    </header>
    <h2>Welcome to My Profile!</h2> <!-- Welcome message -->
    <div class="content-container"> <!-- New container for content -->
      <div class="profile-photo-container">
        <img :src="profilePhoto" alt="Profile Photo" class="profile-photo" />
      </div>
      <div class="info-box">
        <div class="details">
          <h3>{{ name }}</h3>
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
      </div>
      <div class="social-links">
        <h3>Connect with Me</h3>
        <a v-for="link in socialLinks" :key="link.name" :href="link.url" target="_blank">{{ link.name }}</a>
      </div>
    </div> <!-- End of content-container -->
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
  const confirmed = window.confirm("Are you sure you want to log out?");
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
  background-image: url('@/assets/background.gif'); /* Background GIF */
  background-size: cover; /* Cover the entire area */
  background-position: center; /* Center the image */
  min-height: 100vh; /* Ensure it covers full height */
  width: 100vw; /* Full width */
  display: flex; /* Use flexbox for layout */
  flex-direction: column; /* Stack children vertically */
  align-items: center; /* Center horizontally */
  justify-content: center; /* Center vertically */
  position: fixed; /* Fixed positioning to cover entire screen */
  top: 0; /* Align to top */
  left: 0; /* Align to left */
}

h2 {
   color: rgb(229,229,231);
   font-size: calc(3rem); /* Increase size of the welcome heading */
   margin-bottom: calc(20px);
}

.profile-photo-container {
   margin-bottom: calc(20px); /* Space below profile photo */
}

.profile-photo {
   width: 250px; /* Adjust size as needed */
   border-radius: 50%; /* Circular profile photo */
   box-shadow: 0px 4px 15px rgba(0,0,0,0.5); /* Shadow effect */
}

.info-box {
   display: flex; /* Use flexbox for layout of info sections */
   justify-content: space-between; /* Space between columns */
   width: auto; 
   max-width:800px; /* Set a maximum width for uniformity */
   background-color: rgba(255,255,255,0.1); /* Slightly transparent background */
   border-radius:10px; /* Rounded corners */
   padding:20px; /* Padding around the info box */
}

.details,
.courses,
.skills {
   flex-basis: calc(33% - 20px); /* Each section takes up one-third of the space minus margin */
   margin-right: calc(10px); /* Space between columns */
}

.details:hover,
.courses:hover,
.skills:hover {
   background-color: rgba(255,255,255,0.2); /* Darken background on hover for all containers */
}

h3 {
   color: rgb(229,229,231);
   font-size: calc(1.5rem); /* Increase size of section headings */
}

p {
   font-size: calc(1.5rem); /* Increase size of paragraph text */
}

.social-links {
   font-size: calc(1rem);
   margin-top: calc(2rem); 
}

.social-links a {
   color: rgb(229,229,231);
   font-size: calc(1rem);
   margin-right: calc(10px);
}
.social-links a:hover {
    text-decoration: underline; /* Underline on hover for social links */
}

.logout-link{
  background-color: #2600ff; 
   color: white; 
   border-radius: 4px; 
   border: none; 
   padding: .5rem .75rem; 
   cursor: pointer; 
   display: inline-block; /* Ensure it behaves like a block element */
   text-align: center; /* Center text within the link */
   text-decoration: none; /* Remove underline from link */
   font-size: 1rem; /* Set a consistent font size */
   line-height: 1.5; /* Set a consistent line height */
   margin-right:1500px ;
}
.go-back {
   background-color: #2600ff; 
   color: white; 
   border-radius: 4px; 
   border: none; 
   padding: .5rem .75rem; 
   cursor: pointer; 
   display: inline-block; /* Ensure it behaves like a block element */
   text-align: center; /* Center text within the link */
   text-decoration: none; /* Remove underline from link */
   font-size: 1rem; /* Set a consistent font size */
   line-height: 1.5; /* Set a consistent line height */
   margin-left:0px ;
}

.header {
  display: flex; /* Use flexbox for header layout */
  justify-content: space-between; /* Space between logout and go back buttons */
  align-items: center; /* Center items vertically */
  padding: .5rem; /* Add padding for better spacing */
  
}
</style>