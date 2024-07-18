<template>
    <div 
    v-for="item in $props.items.filter(x => x.categoryId === $props.cell.id)" 
    :key="item.id" class="item"
    draggable="true" @click="openDetail(item)" 
    @dragstart="onDragStart($event, item)"
    :style="{ backgroundColor: item.color }">
        <div class="amount">{{ item.amount }}</div>
    </div>
    <v-navigation-drawer 
    :width="326" 
    v-model="drawer" 
    class="drawer pa-5" 
    location="right">
        <div 
        class="detail__img" 
        :style="{ backgroundColor: detailItem.color }"></div>
        <v-divider 
        class="my-5" 
        color="#4D4D4D" 
        :thickness="3"></v-divider>
        <v-skeleton-loader 
        color="transparent" 
        type="article, paragraph">
        </v-skeleton-loader>
        <v-divider 
        class="my-5" 
        color="#4D4D4D" 
        :thickness="3"></v-divider>
        <v-btn 
        v-if="!decrement" 
        color="#FA7272" 
        width="100%" 
        @click.stop="decrement = true">Удалить предмет</v-btn>
        <v-btn 
        v-else 
        color="#FA7272"
        width="100%">Удалить</v-btn>
    </v-navigation-drawer>
</template>
<script>
import { ref } from 'vue';
export default {
    name: 'InvetoryDetail',
    props: {
        items: Array,
        cell: Object,
        onDragStart: Function,
    },
    setup() {
        let drawer = ref(false);
        let decrement = ref(false);
        let detailItem = ref({})

        const openDetail = (item) => {
            drawer.value = !drawer.value
            detailItem.value = item
        }

        return { decrement, drawer, openDetail, detailItem }
    }
}
</script>
<style scoped>
.item {
    position: relative;
    width: 48px;
    height: 48px;
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

.drawer {
    position: absolute !important;
    background-color: rgba(29, 29, 29, 0.1);
    backdrop-filter: blur(5px)
}

.drawer__topbar {
    background-color: transparent !important;
}

.detail__img {
    margin: 20px auto 0;
    width: 115px;
    height: 115px;
    position: relative;
}

.detail__img::after {
    position: absolute;
    content: '';
    left: 15px;
    bottom: 15px;
    width: 100%;
    height: 100%;
    background-color: inherit;
    opacity: .4;
    -webkit-box-shadow: -2px 4px 8px 5px rgba(34, 60, 80, 0.2);
    -moz-box-shadow: -2px 4px 8px 5px rgba(34, 60, 80, 0.2);
    box-shadow: -2px 4px 8px 5px rgba(34, 60, 80, 0.2);
    backdrop-filter: blur(100px)
}
</style>