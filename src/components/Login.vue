<template>
    <div class="login-container">
        <div class="card p-4 login-card">
            <h2 class="mb-3 text-center"> Login </h2>

            <form @submit.prevent="login">
                <div class="mb-3">
                    <label for="password" class="form-label"> <strong>Password</strong> </label>
                    <input type="password" id="password" class="form-control" required v-model="password" />
                </div>

                <button type="submit" class="btn btn-primary w-100"> Login </button>
            </form>

            <p v-if="error" class="mt-3 text-danger text-center"> {{error}}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "LoginPage",
    data() {
        return {
            password: 'cardinals',
            error: ''
        };
    },

    methods: {
        login() {
            if (this.password === 'cardinals') {
                this.error = '';
                this.$emit('login-success');
            } else {
                this.error = 'Incorrect password. Please try again.';
            }
        }
    }
}
</script>

<style>

.login-container {
  width: 100%;
  min-height: 60vh;
  display: grid;         
  place-items: center;      
  padding: 1rem;
}


.login-card {
  max-width: 400px;
  width: 100%;
  border-radius: 0.5rem;
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);
}


.login-card h2 {
  font-size: 1.5rem;
}
</style>