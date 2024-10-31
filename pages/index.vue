<template>
  <div class="login-page">
    <div class="login-container p-5">
      <div class="col-lg-12 p-2">
        <h2 class="text-center login-title">Login</h2>
        <form @submit.prevent="handleLogin">
          <div class="form-group bungkusan">
            <div class="form-group">
              <label for="email">Email:</label>
              <input type="email" v-model="email" required class="m-1" />
            </div>
            <div class="form-group">
              <label for="password">Password:</label>
              <input type="password" v-model="password" required class="m-1" />
            </div>
          </div>
          <button type="submit">Login</button>
        </form>
        <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
      errorMessage: null,
    };
  },
  methods: {
    handleLogin() {
      if (this.email === "admin@smkn4.com" && this.password === "admin12345") {
        alert("Login berhasil!");
        this.$router.push({ name: "home" });
      } else {
        this.errorMessage = "Email atau password salah!";
      }
    },
  },
};
</script>

<style scoped>
/* Background for the entire page */
.login-page {
  background-color: #f0f2f5; /* Light gray background */
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.login-container {
  max-width: 350px;
  margin: 0 auto;
  padding: 2rem;
  background-color: #a6adbe; /* White background for the login box */
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  display: flex;
  align-items: center;
  justify-items: center;
}

.login-title {
  margin-top: -10px; /* Adjust this value to move title higher */
  margin-bottom: 1rem;
}

.form-group {
  margin-bottom: 1rem;
}

.bungkusan {
  border: 1px solid #ddd;
  padding: 1rem;
  border-radius: 8px;
  background-color: #f9f9f9;
}

.error-message {
  color: red;
  font-size: 0.9rem;
}

button {
  padding: 0.5rem 1rem;
  background-color: #626f7e;
  color: rgb(255, 255, 255);
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
