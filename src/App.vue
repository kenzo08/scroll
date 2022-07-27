<script setup lang="ts">
import {onMounted, ref} from "vue";
import SaleCard from '/src/components/SaleCard.vue'
import axios from "axios";

const sales = ref()
const searchQuery = ref('');
const filter = ref()
const horizontal = ref()

const filterArr = ref([
  'Подборки',
  'Все категории',
  'Где поесть',
  'Покупки',
  'Здоровье',
])
let prevScrollpos = window.scrollY;
window.onscroll = function () {
  let currentScrollPos = window.scrollY;
  if (currentScrollPos > 70) {
    filter.value.style.top = "0";
  } else if (currentScrollPos <= 0) {
    filter.value.style.top = "70px";
  } else {
   filter.value.style.top = "-140px";
  }
  prevScrollpos = currentScrollPos;
}

const onEnter = (e: any) => {
  console.log(1)
}

let pos = { top: 0, left: 0, x: 0, y: 0 };

const mouseMoveHandler = function (e: any) {
  // How far the mouse has been moved
  const dx = e.clientX - pos.x;
  const dy = e.clientY - pos.y;

  // Scroll the element
  horizontal.value.scrollTop = pos.top - dy;
  horizontal.value.scrollLeft = pos.left - dx;
};

const mouseDownHandler = function (e: any) {
  pos = {
    // The current scroll
    left: horizontal.value.scrollLeft,
    top: horizontal.value.scrollTop,
    // Get the current mouse position
    x: e.clientX,
    y: e.clientY,
  };

  document.addEventListener('mousemove', mouseMoveHandler);
};


onMounted(async () => {
  horizontal.value.addEventListener('mouseenter', onEnter)
  await axios
      .get(`https://jsonplaceholder.typicode.com/photos?_start=0&_limit=10`)
      .then(response => (sales.value = response.data));
})

</script>

<template>
  <div :class="$style.container">
    <div :class="$style.navbar">
      <div :class="$style.searchBar">
        <input v-model="searchQuery" placeholder="Найти" :class="$style.btn">
      </div>

      <div ref="filter"  :class="$style.filter">
        <p v-for="(item, index) in filterArr" :key="index" :class="$style['filter-label','btn']">{{item}}</p>
      </div>
    </div>

    <div :class="$style.horizontalWrapper">
      <div ref="horizontal" :class="$style.horizontal" draggable="true">
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
  </div>
</template>

<style module>
.container {
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding: 16px;
  width: 100%;
}

.horizontalWrapper {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 80px;
  width: 100%;
}

.horizontal::-webkit-scrollbar, .filter::-webkit-scrollbar {
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
  overflow-x: auto;
}

.navbar {
  background-color: #fff;
}

.searchBar {
  position: sticky;
  width: 100%;
  height: 35px;
  top: 0;
  background: #ffffff;
  z-index: 999;
}

.filter {
  display: flex;
  position: fixed;
  top: 70px;
  gap: 8px;
  background: #ffffff;
  width: calc(100% - 25px);
  overflow-x: scroll;
  white-space: nowrap;
}

.filter-label {
  border: solid 1px lightslategray;
  border-radius: 20px;
  padding: 8px 4px;
  white-space: nowrap;
}

.btn {
  background: whitesmoke;
  font-size: 16px;
  border-radius: 10px;
  padding: 10px 15px;
  border: 1px solid #ccc;
}

@media (max-width: 640px) {
  .btn {
    width: 100%;
  }
}

</style>
