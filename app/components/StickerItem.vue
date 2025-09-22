<template>
  <div class="sticker">
    <div
        class="sticker__mini"
        @mouseenter="openSticker"
        @mouseleave="closeSticker"
    >
      <div class="stack">
        <img
            v-for="(cat, i) in [...cats].reverse()"
            :key="i"
            :src="cat"
            :alt="'cat ' + i"
            class="stack__img"
            :style="{ zIndex: i, top: i * 52 + 'px' }"
        />
      </div>
      <span class="sticker__arrow"><img src="/icons/iconArrow.svg" alt="arrow"/></span>
    </div>

    <div
        class="sticker__content"
        :class="{ 'sticker__content--open': isHover }"
        @mouseenter="openSticker"
        @mouseleave="closeSticker"
    >
      <div class="sticker__inner">
        <h4 class="sticker__title">Консультация эксперта</h4>
        <div class="sticker__images">
          <div class="stack-horizontal">
            <img
                v-for="(cat, i) in cats"
                :key="i"
                :src="cat"
                :alt="'cat ' + i"
                class="stack-horizontal__img"
                :style="{ '--i': i }"
            />
          </div>
        </div>
        <button class="sticker__btn">Получить консультацию</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const isHover = ref(false)
let hoverTimeout: number | null = null

function openSticker() {
  if (hoverTimeout) {
    clearTimeout(hoverTimeout)
    hoverTimeout = null
  }
  isHover.value = true
}

function closeSticker() {
  hoverTimeout = window.setTimeout(() => {
    isHover.value = false
    hoverTimeout = null
  }, 200)
}

const cats = ref<string[]>([])

onMounted(async () => {
    const promises = Array.from({ length: 3 }, async () => {
      const res = await fetch('https://cataas.com/cat?json=true')
      const data = await res.json()
      return data.url.startsWith('http') ? data.url : `https://cataas.com${data.url}`
    })
    cats.value = await Promise.all(promises)
})
</script>

<style scoped lang="scss">
.sticker {
  position: fixed;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;

  &__mini {
    position: relative;
    padding: 10px;
    background: #F4F6F9;
    box-shadow: 0 2px 6px rgba(0,0,0,0.15);
    display: flex;
    flex-direction: column;
    align-items: center;
    cursor: pointer;
    height: 266px;
    justify-content: center;
    border-radius: 14px 0 0 14px;

    .stack {
      position: relative;
      width: 50px;
      height: 180px;
      margin-bottom: 6px;
      left: -18%;
    }

    .stack__img {
      position: absolute;
      width: 64px;
      height: 64px;
      border-radius: 16px;
      left: 0;
      border: 3px solid #F4F6F9;
    }

    .sticker__arrow {
      margin-top: 20px;
    }
  }

  &__content {
    position: absolute;
    right: 80px;
    top: 50%;
    transform: translateY(-50%) scale(0.8);
    opacity: 0;
    background: #F4F6F9;
    padding: 24px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.15);
    width: 220px;
    transition: all 0.3s ease;
    pointer-events: none;
    min-height: 240px;
    border-radius: 8px 0 0 8px;

    &--open {
      opacity: 1;
      transform: translateY(-50%) scale(1);
      pointer-events: auto;
    }

    .sticker__inner {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 24px;
    }

    .sticker__images {
      position: relative;
      height: 50px;
      left: -40%;

      .stack-horizontal {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        height: 50px;

        .stack-horizontal__img {
          position: absolute;
          width: 64px;
          height: 64px;
          border-radius: 16px;
          border: 3px solid #F4F6F9;
          left: calc(var(--i) * 54px);
          z-index: calc(var(--i) + 1);
        }
      }
    }

    .sticker__btn {
      height: 50px;
      font-family: 'Exo 2', sans-serif;
      font-weight: 500;
      font-size: 16px;
      width: 100%;
      margin-top: 12px;
      background: #FFFFFF;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
    }

    .sticker__title {
      font-family: 'Exo 2', sans-serif;
      font-weight: 600;
      font-size: 23px;
      text-align: center;
      margin-bottom: 12px;
      margin-top: 0;
    }
  }
}
</style>
