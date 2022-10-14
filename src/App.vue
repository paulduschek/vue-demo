<template>
  <div id="app">
    <h1>Example</h1>
    <form @submit..prevent="addNew">
      <label>Enter new subject:</label><br />
      <input v-model="newSubject" /><br />
      <button>Add subject</button>
      <hr>
    </form>

    <ul>
      <li v-for="item in subjectArr">
        {{ item.content }}
        <!-- <button @submit..prevent="deleteItem">Delete </button> -->
        <button @click="deleteItem(item)">Delete </button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';
export default {
  setup(){
    const newSubject = ref('');
    const subjectArr = ref([]);
    let id = 0;

    function addNew(){
      console.log('addNew...');
      subjectArr.value.push({
        content: newSubject.value,
        iid: id
      });
      id++;
    }

    function deleteItem(item){
      for (let i = 0; i < subjectArr.value.length; i++) {
        if (subjectArr.value[i].iid == item.iid) {
          subjectArr.value.splice(i, 1);
          return;
        }
      }
    }
    
      return {
        newSubject,
        subjectArr,
        addNew,
        deleteItem,
      };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
