<template>
<div class="container">
<div 
  class="drop-zone" 
  @drop="onDrop($event, 1)"
  @dragenter.prevent
  @dragover.prevent
  >
<div v-for="item in getList(1)" :key="item.id" class="drag-el" draggable="true" @dragstart="startDrag($event, item)">
  <img src="./assets/icon.png">
  {{ item.title }}
</div>
</div> 
<div 
  class="drop-zone" 
  @drop="onDrop($event, 2)"
  @dragenter.prevent
  @dragover.prevent
  >
<div v-for="item in getList(2)" :key="item.id" class="drag-el" draggable="true" @dragstart="startDrag($event, item)">
  <img src="./assets/icon.png">
  {{ item.title }}
</div>
</div> 
<div 
  class="drop-zone" 
  @drop="onDrop($event, 3)"
  @dragenter.prevent
  @dragover.prevent
  >
<div v-for="item in getList(3)" :key="item.id" class="drag-el" draggable="true" @dragstart="startDrag($event, item)">
  <img src="./assets/icon.png">
  {{ item.title }}
</div>
</div> 
<div 
  class="drop-zone" 
  @drop="onDrop($event, 4)"
  @dragenter.prevent
  @dragover.prevent
  >
<div v-for="item in getList(4)" :key="item.id" class="drag-el" draggable="true" @dragstart="startDrag($event, item)">
  <img src="./assets/icon.png">
  {{ item.title }}
</div>
</div> 
<div 
  class="drop-zone" 
  @drop="onDrop($event, 5)"
  @dragenter.prevent
  @dragover.prevent
  >
<div v-for="item in getList(5)" :key="item.id" class="drag-el" draggable="true" @dragstart="startDrag($event, item)">
  <img src="./assets/icon.png">
  {{ item.title }}
</div>
</div> 
<div 
  class="drop-zone" 
  @drop="onDrop($event, 6)"
  @dragenter.prevent
  @dragover.prevent
  >
<div v-for="item in getList(6)" :key="item.id" class="drag-el" draggable="true" @dragstart="startDrag($event, item)">
  <img src="./assets/icon.png">
  {{ item.title }}
</div>
</div> 
</div>
</template>

<script>
import {ref} from 'vue'

export default {
  setup () {
    const items = ref([
      {id:0, title: 'Item 1', list: 1},
      {id:1, title: 'Item 2', list: 2},
      {id:2, title: 'Item 3', list: 3},
      {id:3, title: 'Item 4', list: 4},
      {id:4, title: 'Item 5', list: 5},
      {id:5, title: 'Item 6', list: 6},
    ])
    
    const getList = (list) => {
      return items.value.filter((item)=> item.list == list)
    }
    const startDrag = (event, item) => {
      event.dataTransfer.dropEffect = 'move'
      event.dataTransfer.effectAllowed = 'move'
      event.dataTransfer.setData('itemID', item.id)
      event.dataTransfer.setData('listID', item.list)
    }
   
    const onDrop = (event, list) => {
      const dropZoneItem = items.value.find((item) => item.list == list)
      const itemID = event.dataTransfer.getData('itemID')
      const item = items.value.find((item) => item.id == itemID)
      dropZoneItem.list = item.list
      item.list = list 
    }
    return {
      getList, 
      startDrag, 
      onDrop
    }
  }
}

</script>

<style>
@media only screen and (min-width: 1000px) {
  .container {
   display: grid;
   grid-template-columns: repeat(6, 1fr);
   margin-bottom: 1000px;
  }
}
@media only screen and (max-width: 999px) {
  .container {
   display: grid;
   grid-template-columns: repeat(4, 1fr);
   margin-bottom: 1000px;
  }
}
@media (max-width: 500px) {
  .container {
   display: grid;
   grid-template-columns: repeat(2, 1fr);
   margin-bottom: 1000px;
  }
}
.drop-zone {
  margin: 50px auto;
}
img {
  height: 80px;
  width: 80px;
  margin-bottom: 10px;
}
.drag-el {
  display: flex;
  flex-direction: column;
  padding: 5px;
  margin: 5px;
  text-align: center;
  color: white;
}
</style>
