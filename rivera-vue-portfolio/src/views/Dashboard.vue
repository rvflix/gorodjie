<template>
  <header class="header">
    <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
  </header>
  <div class="dashboard">
    <h1>Dashboard</h1>
    <p>Here you can manage and access different sections.</p>

    <div class="navigation">
      <div class="nav-item" @mouseover="setActivePreview('Profile', 'See The Profile Here')" @mouseleave="clearPreview">
        <router-link to="/portfolio/profile" class="nav-link">Profile</router-link>
        <div v-if="activePreview === 'Profile'" class="preview-text">{{ preview }}</div>
      </div>

      <div class="nav-item" @mouseover="setActivePreview('Showcase', 'See All The Projects Here')" @mouseleave="clearPreview">
        <router-link to="/portfolio/showcase" class="nav-link">Portfolio</router-link>
        <div v-if="activePreview === 'Showcase'" class="preview-text">{{ preview }}</div>
      </div>

      <div class="nav-item" @mouseover="setActivePreview('Contact', 'You Can Contact Me Here')" @mouseleave="clearPreview">
        <router-link to="/portfolio/contact" class="nav-link">Contact Me</router-link>
        <div v-if="activePreview === 'Contact'" class="preview-text">{{ preview }}</div>
      </div>

      <div class="nav-item" @mouseover="setActivePreview('Creative', 'See All My Hobbies')" @mouseleave="clearPreview">
        <router-link to="/portfolio/creative" class="nav-link">Creative</router-link>
        <div v-if="activePreview === 'Creative'" class="preview-text">{{ preview }}</div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const preview = ref<string | null>(null); // State for the preview text
const activePreview = ref<string | null>(null); // State for the active preview

// Function to log out
const logout = async () => {
  const confirmed = window.confirm("Are you sure you want to log out?"); // Use window.confirm for clarity
  if (confirmed) {
    await new Promise(resolve => setTimeout(resolve, 2000)); // Simulate loading for 2 seconds
    await router.push('/'); // Redirect to the login page
  }
};

// Function to set active preview text
const setActivePreview = (title: string, description: string) => {
  activePreview.value = title; // Set the active preview title
  preview.value = description; // Set the description
};

// Function to clear preview text
const clearPreview = () => {
  activePreview.value = null; // Clear the active preview
  preview.value = null; // Clear the description
};
</script>

<style scoped>
.dashboard {
  text-align: center;
  padding: 2rem;
  background-color: #101446; /* Dark background color */
  min-height: 100vh; /* Ensure it covers full height */
  display: flex; /* Use flexbox for layout */
  flex-direction: column; /* Stack children vertically */
  align-items: center; /* Center horizontally */
}

h1 {
  font-size: 3rem;
  margin-bottom: 0.5rem; /* Space below the heading */
  color: rgb(192, 192, 204);
}

p {
  font-size: 1.5rem;
  color: rgb(192, 192, 204); 
}

.navigation {
  margin-top: 1rem; /* Space above navigation links */
  display: flex; /* Use flexbox for horizontal layout */
}

.nav-item {
  margin-right: 1rem; /* Space between nav items */
}

.logout-link {
  color: blue; /* Change the color of the logout link to blue */
  text-decoration: none; /* Remove underline */
}

.logout-link:hover {
  text-decoration: underline; /* Optional: underline on hover */
}

.nav-link {
  display: inline-block;
  padding: 0.5rem 1rem;
  background-color: #2600ff; /* Background color for navigation links */
  color: white;
  border-radius: 4px;
  text-decoration: none;
}

.nav-link:hover {
  background-color: #0056b3; /* Darker shade on hover */
}

/* Preview text styles */
.preview-text {
  margin-top: .5rem; /* Space above the preview text */
  font-size: 1rem; /* Adjust font size as needed */
}
</style>