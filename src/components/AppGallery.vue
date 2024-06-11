<template>
  <v-app>
  <v-row>
    <v-col
      v-for="n in 9"
      :key="n"
      class="d-flex child-flex justify-center"
      cols="4"
      
    >
    <v-hover v-slot="{ isHovering, props }" >
      
      <v-img v-bind="props"
        :lazy-src="`https://picsum.photos/10/6?image=${n * 5 + 10}`"
        :src="`https://picsum.photos/500/300?image=${n * 5 + 10}`"
        aspect-ratio="1"
        
        cover
      >
        <template v-slot:placeholder>
          <v-row
            align="center"
            class="fill-height ma-0"
            justify="center"
          >
            <v-progress-circular
              color="grey-lighten-5"
              indeterminate
            ></v-progress-circular>
          </v-row>
        </template>
        <v-overlay
        :model-value="isHovering"
        class="align-center justify-center"
        contained
        v-for="post in posts" :key="post.id"
      >
      
        <v-btn variant="flat"><h5> {{ post.id }}</h5><p style="max-width: fit-content">{{ post.value }}</p></v-btn>
      </v-overlay>
        
      </v-img>
    
    </v-hover>
      
    </v-col>
    
  </v-row>
</v-app>
</template>

<script>

import axios from 'axios'


  export default{
    data() {
      return {
        posts: []
      }
    },
    mounted() {
      axios.get('https://api.chucknorris.io/jokes/random')
        .then(response => this.posts = response.data)
    },
  }
</script>


