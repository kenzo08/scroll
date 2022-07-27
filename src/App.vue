<script setup lang="ts">
import {onMounted, ref} from "vue";
import SaleCard from '/src/components/SaleCard.vue'
import axios from "axios";

const sales = ref()
const searchQuery = ref('');
const filter = ref()
let prevScrollpos = window.scrollY;
window.onscroll = function () {
  let currentScrollPos = window.scrollY;
  if (prevScrollpos > currentScrollPos || currentScrollPos <= 0) {
    filter.value.style.top = "70px";
  } else {
   filter.value.style.top = "-140px";
  }
  prevScrollpos = currentScrollPos;
}
onMounted(async () => {
  await axios
      .get(`https://jsonplaceholder.typicode.com/photos?_start=0&_limit=10`)
      .then(response => (sales.value = response.data));
})

</script>

<template>
  <div :class="$style.container">
    <div :class="$style.navbar">
      <input v-model="searchQuery" placeholder="Найти">
      <div ref="filter"  :class="$style.filter">
        <p :class="$style['filter-label']">Подборки</p>
        <p :class="$style['filter-label']">Все категории</p>
        <p :class="$style['filter-label']">Где поесть</p>
      </div>
    </div>

    <div :class="$style.horizontal">
      <div v-for="sale in sales" :key="sale.id">
        <SaleCard :title="sale.title"
                  :imageLink="sale.url"
        />
      </div>
    </div>
    <div :class="$style.horizontal">
      <div v-for="sale in sales" :key="sale.id">
        <SaleCard :title="sale.title"
                  :imageLink="sale.url"
        />
      </div>
    </div>
    <div :class="$style.horizontal">
      <div v-for="sale in sales" :key="sale.id">
        <SaleCard :title="sale.title"
                  :imageLink="sale.url"
        />
      </div>
    </div>
    <div :class="$style.horizontal">
      <div v-for="sale in sales" :key="sale.id">
        <SaleCard :title="sale.title"
                  :imageLink="sale.url"
        />
      </div>
    </div>
  </div>
</template>

<style module>
.container {
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding: 16px;
}

.horizontal::-webkit-scrollbar {
  display: none;
}

.horizontal {
  display: flex;
  gap: 16px;
  width: 100%;
  height: 100%;
  -webkit-overflow-scrolling: touch;
  -ms-overflow-style: none;
  scrollbar-width: none;
  overflow-x: scroll;
}

input {
  background: whitesmoke;
  font-size: 16px;
  height: 30px;
  border-radius: 20px;
  padding: 5px;
}

.navbar {
  position: sticky;
  width: 100%;
  height: 70px;
  margin-bottom: 40px;
  top: 0;
  background: #ffffff;
  z-index: 999;
}

.filter {
  display: flex;
  position: fixed;
  top: 70px;
  gap: 8px;
  width: 100%;
  background: #ffffff;
  transition: top 0.3s
}

.filter-label {
  border: solid 1px lightslategray;
  border-radius: 20px;
  padding: 8px 4px;
  white-space: nowrap;
}

</style>
