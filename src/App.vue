<template>
  <div id="app">
    <h1>To Do List</h1>
    <input type='text' v-model='newTask' @keyup.enter='addTask'>
    <button @click='addTask'>Add Task</button>

    <ul>
      <li v-for="item in items" :key="item.id">

        <input type="checkbox" id="checkbox" v-model="item.done">
        <input type='text' v-model='editTask' v-if='editId === item.id' @keyup.enter='update(item)'>
        <span v-else :style="item.done ? 'text-decoration: line-through' : 'initial'">{{item.name}}</span>
        <div id="buttonContainer">
        <button @click="remove(item)" v-if="!editId">&times;</button>
        <button @click="edit(item)" v-if="!editId" class="button">Edit</button>
        <button @click="update(item)" v-if="editId === item.id">Update</button>
        <button @click="cancel" v-if="editId === item.id" class="button">Cancel</button>
        </div>
      </li>
    </ul>

  </div>
</template>


<script>

export default {
  name: 'App',
  data() {
    return {
      newTask : '',
      editTask:'',
      editId:null,

      items: [
        {id: 1, name: 'buy grocery', done: false},
        {id: 2, name: 'feed my fish', done: false},
        {id: 3, name: 'fold clothes', done: true},

             ]
          }
        },
      methods: {

        addTask() {
          this.items.push({
            name: this.newTask,
            done: false
          })
          this.newTask='' 
        },

        edit(item){
          this.editId = item.id,
          this.editTask = item.name
        },

        update(item){
          const index = this.items.indexOf(item)
          this.items[index].name=this.editTask
          this.editId = ''
          this.editTask = ''
        },

        cancel(){
          this.editId = ''
          this.editTask = ''
        },

        remove(item){
          const index = this.items.indexOf(item)
          this.items.splice(index,1)
        },

        toggleTask(){

        }
      },
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;

}

#buttonContainer {
  margin-top: 10px;
  margin-bottom: 10px;
}

.button {
  margin-left: 20px;
}

.input-group--active label {
  text-decoration: line-through;
}
</style>
