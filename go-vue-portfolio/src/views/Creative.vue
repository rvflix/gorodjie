<template>
  <div class="creative">
    <header class="header">
      <RouterLink to="/" class="logout-link" @click.prevent="logout">Log Out</RouterLink>
      <button class="go-back" @click="goBack">Go Back to Dashboard</button>
    </header>
    <div class="content">
      <h2>My Hobbies</h2>
      <p class="intro-text">Click on any hobby to learn more about it!</p>
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
          <div class="hobby-info">
            <h3>{{ hobby.name }}</h3>
            <p v-if="selectedHobby === index" class="hobby-details">
              {{ hobby.details }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import photography from '@/assets/billiards.jpeg';
import cycling from '@/assets/rides.jpeg';
import traveling from '@/assets/workout.jpeg';
import basketball from '@/assets/basketball.jpg';

// Define hobbies with additional details
const hobbies = [
  { name: 'Billiards', image: photography, details: 'In billiards, it’s not the shot you make, but the one you plan.' },
  { name: 'Rides', image: cycling, details: 'Sometimes, the best therapy is a long ride and a quiet mind.' },
  { name: 'Workout', image: traveling, details: 'The pain you feel today will be the strength you feel tomorrow.' },
  { name: 'Basketball', image: basketball, details: 'The game isn’t over until the final buzzer sounds.' },
];

const router = useRouter();
const selectedHobby = ref<number | null>(null);

const toggleHobby = (index: number) => {
  selectedHobby.value = selectedHobby.value === index ? null : index; // Toggle selection
};

const goBack = () => {
  router.push('/dashboard'); // Navigate to the dashboard
};

const logout = async () => {
  const confirmed = window.confirm("Are you sure you want to log out?");
  if (confirmed) {
    await new Promise(resolve => setTimeout(resolve, 2000)); // Simulate loading
    await router.push('/'); // Redirect to the login page
  }
};
</script>

<style scoped>
.creative {
  text-align: center;
  padding: 2rem;
  background-image: url('@/assets/background.gif'); /* Retain the background GIF */
  background-size: cover;
  background-position: center;
  position: fixed;
  top: 0;
  left: 0;
  min-height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 1rem;
  z-index: 10;
}

h2 {
  color: #ffffff;
  font-size: 3rem;
  margin: 1rem 0;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
}

.intro-text {
  color: #dcdcdc;
  font-size: 1.5rem;
  margin-bottom: 2rem;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}

.hobby-grid {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 1.5rem;
  margin: 0 auto;
}

.hobby-item {
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  padding: 1rem;
  width: 250px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: pointer;
  text-align: center;
}

.hobby-item:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.4);
}

.hobby-image {
  width: 100%;
  height: 150px;
  object-fit: cover;
  border-radius: 8px;
  transition: transform 0.3s ease;
}

.hobby-item:hover .hobby-image {
  transform: scale(1.1);
}

.hobby-info {
  margin-top: 1rem;
}

.hobby-info h3 {
  color: #ffffff;
  font-size: 1.5rem;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}

.hobby-details {
  color: #dcdcdc;
  font-size: 1rem;
  margin-top: 0.5rem;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}

.logout-link,
.go-back {
  background-color: #2600ff;
  color: #ffffff;
  border: none;
  border-radius: 5px;
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.logout-link:hover,
.go-back:hover {
  background-color: #0056b3;
  transform: scale(1.05);
}
</style>
