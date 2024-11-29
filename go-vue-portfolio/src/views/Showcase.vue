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
    title: 'Primos Beach Resort',
    description: ' MCWEB: Mobile Compliant Web-based System on Booking for Primos Beach Resort',
    img: {
      src: projectone,
      alt: 'Project One'
    },
    link: 'https://drive.google.com/drive/folders/1K_18Jw4j71RQcoKsmNtzyfz6evhjDNJx?usp=sharing'
  },
  {
    title: 'PetBook',
    description: 'DATABASE MANAGEMENT SYSTEM PET ADOPTION SYSTEM',
    img: {
      src: projecttwo,
      alt: 'Project Two'
    },
    link: 'https://drive.google.com/file/d/1Zx5tbjkKwdolvjPL-6we-LhdLeCyzB9R/view?usp=sharing'
  },
  {
    title: 'SNB',
    description: 'The SnB is a mobile application that utilizes barcode and QR code scanning to improve grocery shopping experience.',
    img: {
      src: projectthree,
      alt: 'Project Three'
    },
    link: 'https://drive.google.com/drive/folders/1KwghTSV1eGqwNf4AF4w4PeCqFdbm5LW_?usp=sharing'
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
  padding: 1rem;
  background-image: url('@/assets/background.gif'); /* Background GIF */
  background-size: cover; /* Cover the entire area */
  background-position: center; /* Center the image */
  position: fixed; /* Fixed positioning to cover entire screen */
  top: 0; /* Align to top */
  left: 0; /* Align to left */
  height: 100vh; /* Full viewport height */
  width: 100vw; /* Full width */
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  overflow: auto; /* Allow scrolling for large content */
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: rgba(255, 255, 255, 0); /* Transparent header */
  padding: 1rem;
}

h2 {
  color: rgb(229, 229, 231);
  font-size: 2rem; /* Adjust font size to fit better */
  margin-bottom: 2rem; /* Add space between title and projects */
}

p {
  color: rgb(229, 229, 231);
  font-size: 1.1rem; /* Slightly larger text */
  margin-bottom: 1rem;
}

h3 {
  color: rgb(229, 229, 231);
  font-size: 1.3rem; /* Increase font size for project title */
}

a {
  color: rgb(229, 229, 231);
  font-size: 1.1rem; /* Slightly larger font for links */
  margin-top: 0.5rem;
  display: inline-block;
  text-decoration: underline;
}

.projects {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly; /* Spread project cards across the screen */
  margin-top: 2rem;
}

.project-card {
  background-color: #121c77;
  border-radius: 8px;
  margin: 1rem;
  padding: 1rem;
  width: 250px; /* Fixed card width for uniformity */
  text-align: left;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.project-card:hover {
  transform: scale(1.05); /* Slight zoom effect on hover */
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3); /* Add shadow on hover */
}

.project-card img {
  width: 100%;
  height: 200px;
  object-fit: cover; /* Crop image to fit within fixed height */
  border-radius: 8px;
}

.project-title {
  font-weight: bold;
  color: rgb(178, 178, 187);
  margin-top: 1rem;
}

.logout-link,
.go-back {
  background-color: #2600ff;
  color: white;
  border-radius: 4px;
  border: none;
  padding: 0.5rem 1rem;
  cursor: pointer;
  font-size: 1rem;
  line-height: 1.5;
  margin: 0 10px;
}

.logout-link:hover,
.go-back:hover {
  background-color: #1f00cc; /* Darker shade on hover */
}
</style>
