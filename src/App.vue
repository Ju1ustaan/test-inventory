<template>
  <v-container>
    <v-row>
      <v-card 
      color="#262626" 
      width="236"
      class="px-4 py-5 rounded-lg border-md border-secondary">
        <img 
        width="100%" 
        src="./assets/images/Img.png" />
        <v-skeleton-loader 
        color="#262626" 
        type="article, paragraph">
        </v-skeleton-loader>
      </v-card>
      <v-spacer></v-spacer>
      <InventoryWind/>
    </v-row>
    <v-row>
        <v-card 
        class="d-flex mt-3 rounded-lg border-md border-secondary" 
        color="#262626" 
        width="100%">
          <v-skeleton-loader 
          width="100%" 
          class="skeleton-footer" 
          color="#262626" 
          type="heading"></v-skeleton-loader>
        <v-spacer></v-spacer>
        <v-btn 
        color="#262626" 
        elevation="0">X</v-btn>
        </v-card>
    </v-row>
  </v-container>
</template>

<script>
import { defineComponent } from 'vue';
import InventoryWind from './components/InventoryWind/InventoryWind.vue'

export default defineComponent({
  name: 'App',
  components: {
    InventoryWind
  }
})
</script>

<style>
body {
  background-color: #1D1D1D;
}

.skeleton-footer div {
  height: 36px;
}
</style>
