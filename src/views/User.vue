<template>
  <v-container fluid>
    <v-layout row>
      <v-flex
        px-3
        py-3
        md3
        v-for="thumbnail in thumbnailList"
        :key="thumbnail.id"
      >
        <v-card @click="gotoVideo(thumbnail.id)">
          <v-img :src="thumbnail.img" height="194"> </v-img>
          <v-card-title>
            {{ thumbnail.title }}
          </v-card-title>
          <v-progress-linear
            :value="thumbnail.completed"
            color="red"
          ></v-progress-linear>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      thumbnailList: [
        {
          id: 1,
          title: "About DIPS",
          img: "https://picsum.photos/id/179/800/800",
          completed: 12,
          rating: 3.2,
          rates: 231
        },
        {
          id: 2,
          title: "DIPS Arena - eHealth solution",
          img: "https://picsum.photos/id/180/800/800",
          completed: 56,
          rating: 2.4,
          rates: 124
        },
        {
          id: 3,
          title: "DIPS SL Team Structure",
          img: "https://picsum.photos/id/191/800/800",
          completed: 100,
          rating: 4.6,
          rates: 6151
        },
        {
          id: 4,
          title: "DIPS SL Team : Short Summary",
          img: "https://picsum.photos/id/182/800/800",
          completed: 87,
          rating: 3.2,
          rates: 231
        },
        {
          id: 5,
          title: "Cross Team Forums",
          img: "https://picsum.photos/id/183/800/800",
          completed: 56,
          rating: 1.2,
          rates: 162
        },
        {
          id: 6,
          title: "Scrum Process",
          img: "https://picsum.photos/id/184/800/800",
          completed: 0,
          rating: 4.0,
          rates: 2131
        },
        {
          id: 7,
          title: "Mobile Development",
          img: "https://picsum.photos/id/185/800/800",
          completed: 66,
          rating: 3.2,
          rates: 231
        },
        {
          id: 8,
          title: "Database Development",
          img: "https://picsum.photos/id/189/800/800",
          completed: 66,
          rating: 3.2,
          rates: 1412
        }
      ]
    };
  },
  methods: {
    gotoVideo(id) {
      console.log(id);
    }
  }
};
</script>

<style scoped>
.v-card--reveal {
  bottom: 0;
  opacity: 0.8;
  position: absolute;
  width: 100%;
}
</style>