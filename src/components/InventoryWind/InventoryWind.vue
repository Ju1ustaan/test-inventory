<template>
    <v-card 
    color="#262626" 
    min-height="505" 
    class="wrapper pa-0 rounded-lg border-md border-secondary">
        <v-layout 
        v-for="(cell) in inventoryCells" 
        class="cell" 
        :key="cell.id" 
        @drop="onDrop($event, cell.id)"
        @dragover.prevent @dragenter.prevent>
            <div 
            v-for="item in items.filter(x => x.categoryId === cell.id)" 
            :key="item.id" 
            class="item"
            draggable="true" 
            @click.stop="drawer = !drawer"        
            @dragstart="onDragStart($event, item)"
            :style="{ backgroundColor: item.color }" >
                <div class="amount">{{ item.amount }}</div>
            </div>
            <v-navigation-drawer :width="500" v-model="drawer" class="drawer" location="right">
                <v-card>
                    <v-toolbar class="drawer__topbar">
                        <v-spacer></v-spacer>
                        <v-btn>X</v-btn>
                    </v-toolbar>
                </v-card>

            </v-navigation-drawer>
        </v-layout>
    </v-card>
</template>

<script>
import { ref } from 'vue';

export default {
    name: 'InventoryWind',
    setup() {
        const inventoryCells = ref([]);
        const drawer = ref(false);
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

        for (let i = 0; i < 120; i++) {
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

        return { items, inventoryCells, onDragStart, onDrop, drawer };
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

.item {
    position: relative;
    width: 48px;
    height: 48px;
    cursor: pointer;
}


.cell {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 105px;
    height: 100px;
    border: 1px solid gray;
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
    backdrop-filter: blur(10px)
}

.drawer__topbar {
    background-color: transparent!important;
}
</style>