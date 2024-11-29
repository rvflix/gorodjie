<template>
  <div class="profile">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
      <button class="go-back" @click="goBack">Go Back to Dashboard</button>
    </header>
    <h2>Welcome to My Profile</h2> <!-- Welcome message -->
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

const name = 'Rodjie Ven F. Go';
const age = 24;
const location = 'Tondo, Manila';
const occupation = 'Student';
const bio = 'Computer engineering student passionate about technology and innovation.';

const courses = [
  'CPE 400 Embedded Systems',
  'CPE 405 Microprocessors',
  'CPE 406 CpE Design 1',
  'CPE 407 Computer Networks Design',
];

const skills = [
  'C++',
  'Java',
  'Python',
  'HTML'
];

const socialLinks = [
  { name: 'Facebook', url: 'https://www.facebook.com/rodjieven.f.go' },
  { name: 'Instagram', url: 'https://www.instagram.com/rv_flrsgo' },
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
  padding: 1rem;
  background-image: url('@/assets/background.gif'); /* Background GIF */
  background-size: cover; /* Cover the entire area */
  background-position: center; /* Center the image */
  height: 100vh; /* Set height to fill the screen */
  width: 100vw; /* Full width */
  display: flex; /* Use flexbox for layout */
  flex-direction: column; /* Stack children vertically */
  align-items: center; /* Center horizontally */
  justify-content: space-around; /* Spread content evenly across the screen */
  position: fixed; /* Fixed positioning for the entire screen */
  top: 0; /* Align to top */
  left: 0; /* Align to left */
  overflow: hidden; /* Prevent scrolling */
}

.header {
  display: flex; /* Use flexbox for header layout */
  justify-content: space-between; /* Space between logout and go back buttons */
  align-items: center; /* Center items vertically */
  width: 100%; /* Full width of the screen */
  padding: 0.5rem 1rem; /* Add padding */
  position: absolute; /* Place it at the top */
  top: 0; /* Stick to the top */
  z-index: 10; /* Ensure it's above other content */
}

h2 {
  font-family: Georgia, 'Times New Roman', Times, serif;
  color: rgb(6, 201, 236);
  font-size: 2rem; /* Adjust font size for fitting */
  margin: 0.5rem 0; /* Reduce margin */
}

.profile-photo-container {
  margin: 0.5rem 0; /* Reduce spacing around the profile photo */
}

.profile-photo {
  width: 150px; /* Smaller size to save space */
  height: 150px; /* Match height with width */
  border-radius: 50%; /* Circular profile photo */
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.5); /* Shadow effect */
}

.info-box {
  display: flex; /* Use flexbox for layout of info sections */
  flex-wrap: wrap; /* Allow items to wrap to the next row if needed */
  justify-content: center; /* Center all content */
  width: 100%; /* Full width */
  max-width: 900px; /* Limit max width */
  padding: 1rem; /* Add padding inside */
  background-color: rgba(255, 255, 255, 0.1); /* Slightly transparent background */
  border-radius: 10px; /* Rounded corners */
}

.details,
.courses,
.skills {
  flex-basis: 30%; /* Each section takes up 30% of the row */
  margin: 0.5rem; /* Add some space between sections */
  text-align: left; /* Align text to the left for readability */
  color:aliceblue;
}

.details p,
.courses ul,
.skills ul {
  font-size: 0.9rem; /* Smaller font size to fit everything */
  margin: 0.2rem 0; /* Reduce space between items */
  color:aliceblue;
}

.social-links {
  font-size: 0.9rem; /* Reduce font size */
  margin-top: 0.5rem; /* Smaller margin at the top */
  color:aliceblue
}

.social-links a {
  margin-right: 0.5rem; /* Reduce spacing between links */
  color: rgb(105, 208, 252);
}

.logout-link,
.go-back {
  font-family: Georgia, 'Times New Roman', Times, serif;
  font-size: 0.8rem; /* Smaller font size for buttons */
  padding: 0.3rem 0.5rem; /* Adjust button padding */
}



.header {
  display: flex; /* Use flexbox for header layout */
  justify-content: space-between; /* Space between logout and go back buttons */
  align-items: center; /* Center items vertically */
  padding: .5rem; /* Add padding for better spacing */
  
}
</style>