<template>
  <v-overlay :absolute="true" :value="overlay">
    <v-card class="elevation-16 mx-auto" width="300">
      <v-card-title class="headline" primary-title>
        Rate This Video
      </v-card-title>
      <v-card-text>
        <v-textarea
          class="subtitle-1"
          outlined
          label="Write a comment"
          :auto-grow="false"
          no-resize
          maxlength="200"
          v-model="comment"
        ></v-textarea>

        <div class="text-center mt-2">
          <v-rating
            v-model="rating"
            color="yellow darken-3"
            background-color="grey darken-1"
            empty-icon="$ratingFull"
            hover
          ></v-rating>
        </div>
      </v-card-text>
      <v-divider></v-divider>
      <v-card-actions class="justify-space-between">
        <v-btn text @click="submit('close')">No Thanks</v-btn>
        <v-btn color="primary" text @click="submit('submit')">
          Rate Now
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-overlay>
</template>

<script>
export default {
  props: ["overlay", "ratingObj"],
  data: () => ({
    rating: 0,
    comment: null
  }),
  methods: {
    submit(option) {
      let rating = this.rating;
      let comment = this.comment;
      this.$emit("submit", { option, rating, comment });
    }
  },
  mounted() {
    if (this.ratingObj) {
      this.rating = this.ratingObj.rating;
      this.comment = this.ratingObj.comment;
    }
  }
};
</script>
