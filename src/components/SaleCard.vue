<template>
  <div :class="$style.container">
    <div :class="['image-box']">
      <img :class="$style.pic" :src="imageLink"/>
    </div>
    <div :class="$style.cardBody">
      <p :class="$style.title">{{title}}</p>
      <div :class="$style.description">
        <p>Ближайшее:
          <span>{{ location }}</span>
        </p>
        <p :class="$style.icon">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
            <path
                d="M12 22a.75.75 0 01-.43-.13C11.14 21.58 1 14.67 1 8.68 1 4.56 3.46 2 7.43 2A6.3 6.3 0 0112 4a6.3 6.3 0 014.57-2A6.57 6.57 0 0123 8.68c0 5.72-10.13 12.88-10.56 13.18A.79.79 0 0112 22zM7.43 3.54c-1.47 0-4.9.5-4.9 5.14S10.09 18.92 12 20.29c3-2.19 9.47-7.72 9.47-11.61a5 5 0 00-4.9-5.14 4.77 4.77 0 00-3.94 2.11A.77.77 0 0112 6a.76.76 0 01-.63-.33 4.84 4.84 0 00-3.94-2.13z"/>
          </svg>
        </p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Props {
  imageLink: string;
  title: string;
  description: string;
  location: string
  mark: number;
  isLiked: boolean;
}

defineProps<Props>()


</script>

<style module>
.container {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  background: #ffffff;
  width: 200px;
  height: 400px;
  overflow: hidden;
  border-radius: 10px;
  border: 1px solid #efefef;
}

.image-box {
  width: 100%;
  height: 50%;
  border-radius: 10px 10px;
}

.icon {
  width: 30px;
  height: 30px;
}

.cardBody {
  display: flex;
  flex-direction: column;
  padding: 0 15px 15px;
  justify-content: space-between;
  flex-grow: 1;
}

.title {
  text-transform: uppercase;
  font-weight: 500;
}

.pic {
  border-radius: 10px 0 0;
  width: 100%;
  height: 200px;
}

.description {
  display: flex;
  justify-content: space-between;
  align-items: center;
  white-space: pre-wrap;
}
.description p {
  margin: 0;
}
</style>
