<template>
  <div class="dashboard">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log out</RouterLink>
    </header>

    <div class="content-container">
      <h1>DASHBOARD</h1>

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
  </div>
</template>

<script setup lang="ts">
// Your existing script setup remains unchanged
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const preview = ref<string | null>(null);
const activePreview = ref<string | null>(null);

const logout = async () => {
  const confirmed = window.confirm("Are you sure you want to log out?");
  if (confirmed) {
    await new Promise(resolve => setTimeout(resolve, 2000));
    await router.push('/');
  }
};

const setActivePreview = (title: string, description: string) => {
  activePreview.value = title;
  preview.value = description;
};

const clearPreview = () => {
  activePreview.value = null;
  preview.value = null;
};
</script>

<style scoped>
.dashboard {
  text-align: center;
  padding: 2rem;
  background-image: url('@/assets/background.gif'); 
  background-size: cover; /* Cover the entire area */
  background-position: center; /* Center the image */
  min-height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: fixed;
  top: 0;
  left: 0;
}

.header {
  position: absolute;
  top: 1rem;
  right: 1rem;
}

.logout-link {
  padding: 0.5rem 1rem;
  background-color: rgba(38, 0, 255, 0.8);
  color: #f0f0f0;
  border-radius: 4px;
  text-decoration: none;
  font-weight: bold;
}

.logout-link:hover {
  background-color: rgba(0, 86, 179, 0.9);
}

.content-container {
  max-width: 700px;
  padding: 2rem;
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 8px;
  background-color: rgba(0, 0, 0, 0.7);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
  text-align: center;
}

h1 {
  font-size: 2.5rem;
  color: #e3e3e3;
  text-transform: uppercase;
  margin-bottom: 1rem;
}

.navigation {
  margin-top: 1rem;
  display: flex;
  flex-wrap: wrap; /* Wrap items on smaller screens */
  gap: 1rem;
  justify-content: center;
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 120px; /* Consistent size for all items */
}

.nav-link {
  display: inline-block;
  padding: 0.75rem 1rem;
  background-color: rgba(30, 30, 30, 0.9);
  color: #f0f0f0;
  border-radius: 4px;
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 500;
  text-align: center;
}

.nav-link:hover {
  background-color: rgba(50, 50, 50, 0.9);
  transform: scale(1.05);
  transition: all 0.3s ease;
}

.preview-text {
  margin-top: 0.5rem;
  font-size: 0.85rem;
  color: #e3e3e3;
  text-align: center;
}

@media (max-width: 768px) {
  .content-container {
    padding: 1.5rem;
  }

  h1 {
    font-size: 2rem;
  }

  .nav-link {
    font-size: 0.8rem;
  }
}
</style>
