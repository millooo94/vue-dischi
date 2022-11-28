<template>
  <main>
    <div class="container">
      <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5 g-5">
        <DiskCard
          v-for="album in arrAlbums"
          :key="album.title"
          :album="album"
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
    axios.get(this.albumApi)
      .then((axiosResponse) => {
        this.arrAlbums = axiosResponse.data.response;
      });
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

</style>
