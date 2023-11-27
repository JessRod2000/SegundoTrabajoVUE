<script setup>

</script>

<template>
  <div class="home">
    <section class="welcome-section">
      <img src="@/assets/administracion.png" alt="Welcome Image" class="welcome-image" />
      <div class="welcome-content">
        <h1 class="welcome-title">Welcome to User Management</h1>
      </div>
    </section>

    <!-- Resto de tu contenido -->
  </div>
</template>

<style>
.home {
  max-width: 80%;
  margin: 0 auto;
  padding: 20px;
}

.welcome-section {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 30px;
}

.welcome-image {
  max-height: 400px;
  border-radius: 8px;
  margin-bottom: 20px;
}

.welcome-content {
  text-align: center;
  max-width: 80%;
  margin: 50px 30px;
  padding: 20px;
  border-radius: 10px;
  background-color: #f8f8f8;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.welcome-title {
  font-size: 5em;
  margin-bottom: 10px;
  color: #333;
}

h1 {
  font-size: 2.5em;
  margin-bottom: 10px;
}

p {
  font-size: 1.2em;
  color: #666;
}
</style>
