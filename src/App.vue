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
      <v-card 
      color="#262626"
      min-height="505"
      class="wrapper pa-0 rounded-lg border-md border-secondary">
      <div class="cell"
      v-for="(item) in inventoryCells"
      :key="item">
      <div v-if="invetoryItems[item.id]" class="item" @click="openDesc" draggable="true">
        <div class="amount">{{ invetoryItems[item.id].amount }}</div>
      </div>
    
    </div>
      </v-card>
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

<script setup>
let inventoryCells = []
let invetoryItems = [
  {
    id: 1,
    color: 'green',
    amount: 5,
  },
  {
    id: 2,
    color: 'orange',
    amount: 5,
  },
  {
    id: 3,
    color: 'blue',
    amount: 1,
  },
]

for(let i = 0; i < 120; i++){
  inventoryCells = [...inventoryCells, {id: i}]
}

const openDesc = () => {
  console.log('hello');
}
</script>

<style>
body {
  background-color: #1D1D1D;
}

.wrapper {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  width: calc(100% - 250px);
  height: calc(100vh - 110px)
}

.skeleton-footer div {
  height: 36px;
}

.cell {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 105px;
  height: 100px;
  border: 1px solid gray;
}

.item {
  position: relative;
  width: 48px;
  height: 48px;
  background-color: red;
  cursor: pointer;
}
.item::after {
  position: absolute;
  content: '';
  left: 5px;
  bottom: 5px;
  width: 100%;
  height: 100%;
  background-color: inherit;
  opacity: .4;
  -webkit-box-shadow: -2px 4px 8px 5px rgba(34, 60, 80, 0.2);
-moz-box-shadow: -2px 4px 8px 5px rgba(34, 60, 80, 0.2);
box-shadow: -2px 4px 8px 5px rgba(34, 60, 80, 0.2);
backdrop-filter: blur(100px)
}

.amount {
  position: absolute;
  right: -28px;
  bottom: -25px;
  font-size: 10px;
  padding: 2px 4px;
  color: gray;
  border-top: 1px solid gray;
  border-left: 1px solid gray;
  border-radius: 6px 0 0 0;
}

</style>
