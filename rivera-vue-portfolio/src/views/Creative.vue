<template>
  <div class="creative">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
      <button class="go-back" @click="goBack">Go Back to Dashboard</button>
    </header>
    <h2>My Hobbies</h2>
    <div class="hobby-grid">
      <div class="hobby-item" v-for="(hobby, index) in hobbies" :key="index" @click="toggleHobby(index)">
        <img :src="hobby.image" alt="hobby.name" class="hobby-image" :class="{ 'active': selectedHobby === index }" />
        <p>{{ hobby.name }}</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import photography from '@/assets/photography.jpg';
import cycling from '@/assets/cycling.jpg';
import traveling from '@/assets/traveling.jpg';
import basketball from '@/assets/basketball.jpg';

// Define hobbies
const hobbies = [
  { name: 'Photography', image: photography },
  { name: 'Cycling', image: cycling },
  { name: 'Traveling', image: traveling },
  { name: 'Basketball', image: basketball },
];

const router = useRouter();
const selectedHobby = ref<number | null>(null);

const toggleHobby = (index: number) => {
  selectedHobby.value = selectedHobby.value === index ? null : index; // Toggle selection
};

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
  font-size: 3rem; /* Increase size of the name heading by an additional rem */
}

.creative {
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

.hobby-grid {
  display: grid; /* Use CSS Grid for layout */
  grid-template-columns: repeat(2, 1fr); /* Create two columns */
  gap: 1rem; /* Space between grid items */
}

.hobby-item {
  background-color: #321cb3; /* Match background color with Go Back button */
  border-radius: 8px; /* Rounded corners */
  padding: 1rem; /* Padding inside each item */
  display: flex; /* Use flexbox for centering content */
  flex-direction: column; /* Stack image and text vertically */
  align-items: center; /* Center items horizontally */
  cursor: pointer; /* Pointer cursor on hover */
}

.hobby-image {
  width: 200px; /* Fixed width for uniformity */
  height: 200px; /* Fixed height for uniformity */
  border-radius: 10%; /* Make it circular */
  box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.5); /* Shadow effect */
  object-fit: cover; /* Ensure aspect ratio is maintained without distortion */
  transition: transform 0.5s ease; /* Smooth transition for scaling effect */
}
.hobby-image {
  background-color: rgba(255, 255, 255, 0.1); /* Slightly transparent background */
  border-radius: 10px; /* Rounded corners */
  padding: 1rem; /* Padding around the details */
  margin-top: 1rem; /* Space above details */
}

.hobby-image:hover {
  background-color: rgba(255, 255, 255, 0.2); /* Darken background on hover */
}
.hobby-image.active {
  transform: scale(2); /* Scale up when active/toggled */
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
  padding: 0.5rem 1rem; /* Padding for button */
}

.go-back:hover {
  background-color: #0056b3; /* Darker shade on hover */
}
</style>