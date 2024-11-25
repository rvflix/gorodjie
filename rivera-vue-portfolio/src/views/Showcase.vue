<template>
  <div class="showcase">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
      <button class="go-back" @click="goBack">Go Back to Dashboard</button>
    </header>
    <h2>Portfolio Showcase</h2>
    <div class="projects">
      <div class="project-card" v-for="project in projects" :key="project.title">
        <img :src="project.image" alt="" />
        <h3>{{ project.title }}</h3>
        <p>{{ project.description }}</p>
        <a :href="project.link" target="_blank">View Project</a>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

const projects = ref([
  {
    title: 'Project One',
    description: 'Description of project one.',
    image: 'path/to/project-one-image.jpg', // Replace with actual image path
    link: 'https://drive.google.com/file/d/1Z3RKd3MxTPb098voyZGnzgnWJgtFUt9j/view?usp=drive_link'
  },
  {
    title: 'Project Two',
    description: 'Description of project two.',
    image: 'path/to/project-two-image.jpg', // Replace with actual image path
    link: 'https://drive.google.com/file/d/1YAqTNMzQl0Mm4tfjO_4N1zKbkoobvgCq/view?usp=drive_link'
  },
  {
    title: 'Project Three', // Replace with actual title
    description: 'Your New Project Description', // Replace with actual description
    image: 'path/to/your-new-project-image.jpg', // Replace with actual image path
    link: 'https://drive.google.com/file/d/1cdoNkyeAeuDZmFy7Xpz74kqaMGrYCqkg/view?usp=drive_link' // Replace with actual link
  },
]);

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
h2 {
  color: rgb(178, 178, 187);
}

.project-card h3,
.project-card p {
  color: rgb(178, 178, 187); /* Match the color of h2 */
}

.showcase {
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

.projects {
  display: flex;
  flex-wrap: wrap;
}

.project-card {
  border: 1px solid #ccc;
  border-radius: 8px;
  margin: 10px;
  padding: 10px;
  width: calc(33% - 20px); /* Adjust width as needed */
}

.project-card img {
   width:100%; /* Responsive image */
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