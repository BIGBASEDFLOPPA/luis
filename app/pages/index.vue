<template>
  <div class="main">
    <h1>Главная страница</h1>
    <NuxtLink to="/sticker" class="btn-link">Перейти на страницу со стикером</NuxtLink>
  </div>
</template>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 100px;
}
.btn-link {
  margin-top: 20px;
  padding: 10px 20px;
  background: #1565C0;
  color: #fff;
  border-radius: 6px;
  text-decoration: none;
  box-shadow: 0 5px 15px 0 rgba(21, 101, 192, 0.7);
  transition: 0.3s;
}

.btn-link:hover {
  background: #1E88E5;
  transform: translateY(-3px);
  box-shadow: 0 10px 30px 0 rgba(30, 136, 229, 0.9);
}
</style>
<script setup lang="ts">

</script>