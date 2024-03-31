<!-- App.vue -->
<template>
  <div class="container">
    <h1>Random User Data</h1>

    <div class="user-data-container">
      <div v-for="user in userData" :key="user.login.uuid" class="user-data">
        <img :src="user.picture.large" alt="User Image" class="profile-image" />

        <div class="user-details">
          <p>Name: {{ user.name.title }} {{ user.name.first }} {{ user.name.last }}</p>
          <p>Email: {{ user.email }}</p>
          <p>Phone: {{ user.phone }}</p>
          <p>Gender: {{ user.gender }}</p>
          <p>Date of Birth: {{ user.dob.date }}</p>
          <p>Location: {{ user.location.city }}, {{ user.location.country }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',

  data() {
    return {
      userData: [],
    };
  },

  mounted() {
    this.fetchUserData();
  },

  methods: {
    async fetchUserData() {
      try {
        const response = await fetch('https://randomuser.me/api/?results=3');
        const data = await response.json();
        this.userData = data.results;
      } catch (error) {
        console.error('Error fetching user data:', error);
      }
    },
  },
};
</script>

<style>
h1 {
  margin-bottom: 5vh;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  margin-left: 25vw;
  font-family: Arial, sans-serif;
  padding: 2vw;
}

.user-data-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.user-data {
  display: flex;
  align-items: center;
  margin-bottom: 2vh;
  padding-bottom: 2vh;
  border-bottom: 1px solid #ccc;
  width: 100%;
  max-width: 100vw;
}

.profile-image {
  width: 10vw;
  height: 10vw;
  border-radius: 50%;
  object-fit: cover;
  margin-right: 2vw;
}

.user-details {
  text-align: left;
}
</style>