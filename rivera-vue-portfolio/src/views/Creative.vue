<template>
  <div class="creative">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
      <button class="go-back" @click="goBack">Go Back to Dashboard</button>
    </header>
    <h2>My Hobbies</h2>
    <p1>Click on any hobby to learn more!</p1>
    <div class="hobby-grid">
      <div 
        class="hobby-item" 
        v-for="(hobby, index) in hobbies" 
        :key="index" 
        @click="toggleHobby(index)"
      >
        <img 
          :src="hobby.image" 
          :alt="hobby.name" 
          class="hobby-image" 
          :class="{ 'active': selectedHobby === index }" 
        />
        <p2>{{ hobby.name }}</p2>
        <!-- Show details if this hobby is selected -->
        <div v-if="selectedHobby === index" class="hobby-details">
          <p3>{{ hobby.details }}</p3>
        </div>
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

// Define hobbies with additional details
const hobbies = [
  { name: 'Photography', image: photography, details: 'Capturing moments through the lens.' },
  { name: 'Cycling', image: cycling, details: 'Exploring nature on two wheels.' },
  { name: 'Traveling', image: traveling, details: 'Discovering new cultures and places.' },
  { name: 'Basketball', image: basketball, details: 'Playing and watching my favorite sport.' },
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
.creative {
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

p1 {
  color: rgb(229, 229, 231);
  background-color: rgba(48, 48, 48, 0.781);
  font-size: calc(1.5rem); /* Increase size of paragraph text */
  
}
p2 {
  color: rgb(229, 229, 231);
  font-size: calc(1.5rem); /* Increase size of paragraph text */
}

p3 {
  color: rgb(229, 229, 231);
  font-size: calc(1.5rem); /* Increase size of paragraph text */
}


.hobby-grid {
  display: flex;
  justify-content: center; /* Center the hobby items horizontally */
  flex-wrap: wrap; /* Allow wrapping of hobby items */
}

.hobby-item {
  background-color: rgba(255,255,255,0.1); /* Slightly transparent background for hobby items */
  border-radius: 10px; /* Rounded corners */
  padding: .5rem; /* Padding inside each item */
  margin: calc(10px); /* Space between items */
  
  display: flex; /* Use flexbox for centering content */
  flex-direction: column; /* Stack image and text vertically */
  align-items: center; /* Center items horizontally */
  
  cursor: pointer; /* Pointer cursor on hover */
}

.hobby-image {
  width:100%; /* Ensure images take full width of the card */
   height:auto; /* Maintain aspect ratio */
   max-height:300px; /* Set a fixed height for uniformity */
   object-fit: cover; /* Crop images to fit within the specified dimensions */
   border-radius:8px; /* Rounded corners for images */
}

.hobby-item:hover .hobby-image {
   transform: scale(1.2); /* Scale up on hover for effect */
}

.hobby-details {
   margin-top: .5rem;
   color: rgb(178,178,187); /* Set color for details text */
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