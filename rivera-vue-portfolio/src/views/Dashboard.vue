<template>
  <div class="dashboard">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
    </header>
    
    <div class="content-container"> <!-- New container for content -->
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
    </div> <!-- End of content-container -->
  </div>
</template>

<script setup lang="ts">
// Your existing script setup remains unchanged
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

.header {
  position: absolute; /* Positioning the header absolutely */
  top: 1rem; /* Distance from the top */
  right: 1rem; /* Distance from the right */
}

.logout-link {
  padding: 0.5rem 1rem; /* Padding inside the link */
  background-color: rgba(38,0,255,0.8); /* Background color for the logout link */
  color: rgb(240,240,240); /* Light text color for logout link */
  border-radius: 4px; /* Rounded corners for link */
  text-decoration: none; /* Remove underline */
}

.logout-link:hover {
  background-color: rgba(0,86,179,0.8); /* Darker shade on hover with transparency */
}

.content-container { 
    max-width: 700px; /* Limit container width */
    max-height: 300px;
    padding: 2rem; /* Padding around the container */
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 1px solid #d3d3d3; /* Border around container */
    border-radius: 8px; /* Rounded corners */
    box-shadow: 0 2px 10px rgba(94, 94, 94, 0.3); /* Shadow effect for depth */
    background-color: rgba(92, 92, 92, 0.9); /* Darker semi-transparent background */

}

h1 {
  font-size: 3rem;
  margin-bottom: 0.5rem; /* Space below the heading */
  color: rgb(220, 220, 220); /* Lighter text color for heading */
}

p {
  font-size: 1.5rem;
  color: rgb(220, 220, 220); /* Lighter text color for paragraph */
}

.navigation {
  margin-top: 1rem; /* Space above navigation links */
  display: flex; /* Use flexbox for horizontal layout */
}

.nav-item {
   margin-right: .5rem; /* Adjust space between nav items as needed */ 
}

.nav-link {
   display: inline-block;
   padding: .5rem .75rem;
   background-color: rgba(30,30,30,0.9); 
   color: rgb(240,240,240); 
   border-radius:4px; 
}

.nav-link:hover {
   background-color: rgba(50,50,50,0.9); 
}

/* Preview text styles */
.preview-text {
   margin-top: .5rem; 
   font-size: .9rem; 
   color: rgb(240,240,240); 
}
</style>