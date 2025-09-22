<template>
  <div class="sticker-page">
    <h1>Страница со стикером</h1>
    <div class="blocks">
      <div v-for="i in 25" :key="i" class="block">
        Блок {{ i }}
      </div>
    </div>
    <StickerItem />
  </div>
</template>

<script setup lang="ts">
import StickerItem from "../components/StickerItem.vue";
</script>

<style scoped>
.sticker-page {
  padding: 50px;
  font-family: 'Exo 2', sans-serif;
  background-color: #f0f2f5;
}
.sticker-page h1 {
  margin-bottom: 20px;
  color: #333;
}
.blocks {
  display: flex;
  flex-direction: column;
  gap: 16px;

}
.block {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.1);
  text-align: center;
  color: #555;
}
</style>
