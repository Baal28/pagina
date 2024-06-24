<template>
  <v-app>
    <v-row>
      <v-col
        v-for="item in posts"
        :key="item.id"
        class="d-flex child-flex justify-center"
        cols="4"
      >
        <v-hover v-slot="{ isHovering, props }">
          <v-img
            v-bind="props"
            :lazy-src="`https://picsum.photos/10/6?image=${item.id * 5 + 10}`"
            :src="`https://picsum.photos/500/300?image=${item.id * 5 + 10}`"
            aspect-ratio="1"
            cover
          >
            <template v-slot:placeholder>
              <v-row align="center" class="fill-height ma-0" justify="center">
                <v-progress-circular
                  color="grey-lighten-5"
                  indeterminate
                ></v-progress-circular>
              </v-row>
            </template>

            <v-overlay
              :model-value="isHovering"
              class="align-center justify-center blur-on-hover"
              contained
              style="background-color: black"
            >
              {{ item.joke }}
            </v-overlay>
          </v-img>
        </v-hover>
      </v-col>
    </v-row>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    async getJoke() {
      const result = await axios.get("https://api.chucknorris.io/jokes/random");
      return result.data.value;
    },
    async buildObject() {
      const totalImages = 9;
      for (let index = 0; index < totalImages; index++) {
        const obj = {};
        obj.id = index + 1;
        obj.joke = await this.getJoke();
        this.posts.push(obj);
      }
    },
  },
  mounted() {
    this.buildObject();
  },
};
</script>
