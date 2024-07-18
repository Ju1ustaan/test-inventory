<template>
    <v-card 
    color="#262626" 
    min-height="505" 
    class="wrapper pa-0 rounded-lg border-md border-secondary">
        <v-layout 
        v-for="cell in inventoryCells" 
        class="cell" 
        :key="cell.id" 
        @drop="onDrop($event, cell.id)"
        @dragover.prevent @dragenter.prevent>
            <InventoryDetail :items="items" :cell="cell" :onDragStart="onDragStart"/>
        </v-layout>
    </v-card>
</template>

<script>
import { ref } from 'vue';
import InventoryDetail from './InventoryDetail.vue'

export default {
    name: 'InventoryWind',
    components: {
        InventoryDetail,
    },
    setup() {
        const inventoryCells = ref([]);
        const items = ref([
            {
                id: 1,
                color: 'green',
                amount: 5,
                categoryId: 0
            },
            {
                id: 2,
                color: 'orange',
                amount: 5,
                categoryId: 1
            },
            {
                id: 6,
                color: 'blue',
                amount: 1,
                categoryId: 2
            },
        ]);

        for (let i = 0; i < 100; i++) {
            inventoryCells.value.push({ id: i });
        }

        function onDragStart(e, item) {
            e.dataTransfer.dropEffect = 'move';
            e.dataTransfer.effectAllowed = 'move';
            e.dataTransfer.setData('itemId', item.id.toString());
        }

        function onDrop(e, categoryId) {
            const itemId = parseInt(e.dataTransfer.getData('itemId'));
            items.value = items.value.map(x => {
                if (x.id === itemId) {
                    x.categoryId = categoryId;
                }
                return x;
            });
        }

        return { items, inventoryCells, onDragStart, onDrop };
    }
}
</script>

<style scoped>
.wrapper {
    position: relative;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    width: calc(100% - 250px);
    height: calc(100vh - 110px)
}

.cell {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 105px;
    height: 100px;
    border: 1px solid gray;
}


</style>