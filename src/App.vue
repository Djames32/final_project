<template>
  <div id="app" class="app-layout">
    <div class="header">
      <h1 class="text-center"> Final Project </h1>
    </div>

    <div class="main">
    <Login v-if="!isLoggedIn" @login-success="loginSuccess" />

    <Home v-else :items="items" :loading="isLoading" :error="error"/>
    </div>
  </div>
</template>

<script>
import Login from './components/Login.vue'
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Login,
    Home
  },

  data() {
    return {
      isLoggedIn: false,
      items: [],
      isLoading: false,
      error: ''
    }
  },

  methods: {
    async loginSuccess() {
      this.isLoggedIn = true;
      this.error = '';
      await this.fetchData();
    },

    async fetchData() {
      this.isLoading = true;
      this.error = '';

      try {
        const res = await fetch('https://cis255.vercel.app/api', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({ password: 'cardinals' })
      });

      if(!res.ok) {
        throw new Error(`Error: ${res.status} ${res.statusText}`);
      }

      const data = await res.json();
      console.log('API Log:', data);

      this.items = Array.isArray(data.books) ? data.books : [];

      this.error = '';
    } catch (err) {
      console.error(err);
      this.error = `Failed to fetch data: ${err.message}`;
      this.items = [];
    } finally {
      this.isLoading = false;
    }
  }
}
}
</script>

<style>
.app-layout {
  min-height: 100vh;
  display: grid;
  grid-template-rows: auto 1fr;
  background-color: #f2f4f7;
  color: #212529;
}

.header {
  background-color: #ffffff;
  padding: 1.5rem 1rem 0.75rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.header h1 {
  margin: 0;
  font-size: 2rem;
  font-weight: 700;
}



.main {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding: 1rem;
}
</style>
