<template>
  <div class="showcase">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
      <button class="go-back" @click="goBack">Go Back to Dashboard</button>
    </header>
    <h2>Portfolio Showcase</h2>
    <div class="projects">
      <div class="project-card" v-for="project in projects" :key="project.title">
        <img :src="project.img.src" :alt="project.img.alt" />
        <h3 class="project-title">{{ project.title }}</h3>
        <p>{{ project.description }}</p>
        <a :href="project.link" target="_blank">View Project</a>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import projectone from '@/assets/projectone.jpg';
import projecttwo from '@/assets/projecttwo.jpg';
import projectthree from '@/assets/projectthree.jpg';

const router = useRouter();

const projects = ref([
  {
    title: 'PORKIFY',
    description: 'Exploring Farmer Perspectives: Essential Features for an Advanced Farmer Monitoring System',
    img: {
      src: projectone,
      alt: 'Project One'
    },
    link: 'https://drive.google.com/file/d/1Z3RKd3MxTPb098voyZGnzgnWJgtFUt9j/view?usp=drive_link'
  },
  {
    title: 'EatEasy',
    description: 'A COMPUTERIZED WEB-BASED ORDERING SYSTEM WITH CHAT-BOT CUSTOMER SERVICE FOR RESTAURANT AMARI’S',
    img: {
      src: projecttwo,
      alt: 'Project Two'
    },
    link: 'https://drive.google.com/file/d/1YAqTNMzQl0Mm4tfjO_4N1zKbkoobvgCq/view?usp=drive_link'
  },
  {
    title: 'Manic Beauty mobile application',
    description: 'A mobile application using Android Studio with Java for both the frontend and backend, providing a comprehensive platform that includes user access, admin access, and super admin access.',
    img: {
      src: projectthree,
      alt: 'Project Three'
    },
    link: 'https://drive.google.com/file/d/1cdoNkyeAeuDZmFy7Xpz74kqaMGrYCqkg/view?usp=drive_link'
  },
]);

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
.showcase {
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
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: rgba(255, 255, 255, 0); /* Lighten header background */
  padding: .5rem; /* Add padding for better spacing */
  
}

h2 {
  color: rgb(229, 229, 231);
  font-size: 3rem; /* Increase font size for the heading */
}

p {
   color: rgb(229, 229, 231);
   
   font-size: calc(1.5rem); /* Increase size of paragraph text */
}

h3 {
   color: rgb(229, 229, 231);
   font-size: calc(1.5rem); /* Increase size of paragraph text */
}

a {
   color: rgb(229, 229, 231);
   font-size: calc(1.5rem); /* Increase size of paragraph text */
   margin-top: .5rem; /* Add some space above the link */
   display:inline-block; /* Ensure it behaves like a block element for better spacing */
}

.projects {
   display: flex;
   justify-content: center; /* Center the project cards horizontally */
   flex-wrap: wrap; /* Allow wrapping of project cards */
}

.project-card {
   background-color: #121c77;
   border: 1px solid #ccc;
   border-radius: 8px;
   margin: calc(10px); /* Space between cards */
   padding: calc(10px); 
   width: calc(30% - 20px); /* Adjust width for three cards per row with margin */
}

.project-card img {
   width:100%; /* Ensure images take full width of the card */
   height:auto; /* Maintain aspect ratio */
   max-height:300px; /* Set a fixed height for uniformity */
   object-fit: cover; /* Crop images to fit within the specified dimensions */
   border-radius:8px; /* Rounded corners for images */
}

.project-card h3,
.project-card p {
   color: rgb(178,178,187);
}

.project-title {
   font-weight:bold; /* Make project titles bold */
}

.logout-link,
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
}

.header {
  display: flex; /* Use flexbox for header layout */
  justify-content: space-between; /* Space between logout and go back buttons */
  align-items: center; /* Center items vertically */
  padding: .5rem; /* Add padding for better spacing */
}
</style>