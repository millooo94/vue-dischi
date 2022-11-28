<template>
  <main>
    <div class="container">
      <div
        v-if="arrAlbums"
        class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5 g-5"
      >
        <DiskCard
          v-for="album in arrAlbums"
          :key="album.title"
          :album="album"
        />
      </div>
      <div
        v-else
        class="loader-container"
      >
        <span
          class="loader"
        />
      </div>
    </div>
  </main>
</template>

<script>
import axios from 'axios';
import DiskCard from '@/components/DiskCard.vue';

export default {
  name: 'MainPage',
  components: {
    DiskCard,
  },
  data() {
    return {
      arrAlbums: null,
      albumApi: 'https://flynn.boolean.careers/exercises/api/array/music',
    };
  },
  created() {
    setTimeout(() => {
      axios.get(this.albumApi)
        .then((axiosResponse) => {
          this.arrAlbums = axiosResponse.data.response;
        });
    }, 6000);
  },
};
</script>

<style lang="scss" scoped>
main {
  background-color: #1e2d3b;
}
.container {
  padding: 4rem;
}
.loader-container {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.loader {
    width: 80px;
    height: 80px;
    border: 5px solid #FFF;
    border-bottom-color: transparent;
    border-radius: 50%;
    display: inline-block;
    box-sizing: border-box;
    animation: rotation 1s linear infinite;
    }

    @keyframes rotation {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
    }

</style>
