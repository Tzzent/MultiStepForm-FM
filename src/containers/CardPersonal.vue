<script setup lang="ts">
import Form1 from "../components/Form1.vue";
</script>

<template>
  <div class="card-container">
    <Form1 />
  </div>
  <div class="footer-container">
    <button>Next Step</button>
  </div>
</template>

<style scoped>
.card-container {
  background-color: #fff;
  border-radius: var(--radius-box);
  padding: 20px;
  margin-top: -80px;
  max-width: 380px;
  box-shadow: 1px 1px 18px 2px rgb(0, 0, 0, 0.3);
}

.footer-container {
  width: 100%;
  display: flex;
  justify-content: end;
  background-color: #fff;
  padding: 10px;
}
.footer-container button {
  border: none;
  border-radius: 8px;
  padding: 15px 20px;
  background-color: #012a58;
  color: #fff;
  font-weight: bold;
}
</style>
