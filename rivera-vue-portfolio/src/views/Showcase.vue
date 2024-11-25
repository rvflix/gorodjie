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
      alt: 'Project One',
      class: 'projectone'
    },
    link: 'https://drive.google.com/file/d/1Z3RKd3MxTPb098voyZGnzgnWJgtFUt9j/view?usp=drive_link'
  },
  {
    title: 'EatEasy',
    description: 'A COMPUTERIZED WEB-BASED ORDERING SYSTEM WITH CHAT-BOT CUSTOMER SERVICE FOR RESTAURANT AMARI’S',
    img: {
      src: projecttwo,
      alt: 'Project Two',
      class: 'projecttwo'
    },
    link: 'https://drive.google.com/file/d/1YAqTNMzQl0Mm4tfjO_4N1zKbkoobvgCq/view?usp=drive_link'
  },
  {
    title: 'Manic Beauty mobile application',
    description: 'A mobile application using Android Studio with Java for both the frontend and backend, providing a comprehensive platform that includes user access, admin access, and super admin access.',
    img: {
      src: projectthree,
      alt: 'Project Three',
      class: 'projectthree'
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
h2 {
  color: rgb(178, 178, 187);
}

.project-card h3,
.project-card p {
  color: rgb(178, 178, 187);
}

.project-title {
  font-weight: bold; /* Make project titles bold */
}

.showcase {
  text-align: center;
  padding: 2rem;
  background-color: #101446;
  min-height: 100vh;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.projects {
  display: flex;
  flex-wrap: wrap;
}

.project-card {
  border: 1px solid #ccc;
  border-radius: 8px;
  margin: 10px;
  padding: 10px;
  width: calc(33% - 20px);
}

.project-card img {
   width:100%; /* Ensure images take full width of the card */
   height:150px; /* Set a fixed height for uniformity */
   object-fit: cover; /* Crop images to fit within the specified dimensions */
}

.logout-link {
   color: blue;
}
.go-back {
   margin-left: auto;
   background-color: #2600ff;
   color: white;
   border-radius: 4px;
   border: none;
   padding:.5rem;
   cursor:pointer;
}
.go-back:hover {
   background-color:#0056b3; 
}
</style>