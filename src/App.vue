<template>
  <div id="app">
    <div class="container">
      <div class="header">
        <div class="title">To-Do Application</div>
        <div class="add-todo">
          <img @click="toggleModal"  src="./assets/Groupadd-btn.svg" alt="Adding Task to ToDo">
          <AddToDo class="form-modal" @myTaskEdit="myTaskEdit" @close="toggleModal" :show="show" :editObjc="editedObj" @myTask="addTask"/>
        </div>
      </div>
      <div class="main">
        <li v-for="(task, index) in myData" :key="index">
          <div class="check">
            <input type="checkbox">
          </div>
          <div class="content">
            <div class="obj">
              <p>{{task.conObj}}</p>
              </div>
            <div class="date-month">
              <p>{{task.myDate}}/{{task.myMonth +1}}</p>
            </div>
            <div class="time">
              <p>Time: {{task.myHours}}:{{task.myMinutes}}</p>
            </div>
          </div>
          <div  @click="editTask(index)" class="edit"><p>Edit</p></div>
          <div @click="deleteTask(index)" class="delete"><p>Delete</p></div>
        </li>
      </div>
    </div>
  </div>
</template>

<script>

import AddToDo from "./components/AddToDo.vue"

export default {
  name: 'App',
  components: {
    AddToDo,
  },
  data() {
    return {
      isEdit: false,
      editIndex: null,
      time: "",
      date: new Date(),
      show: false,
      myData: [],
      editedObj: null,
      editEmitIndex: null,
    }
  },
  methods: {
    addTask(obj) {
      this.myData.push({conObj: obj.content, myDate: this.date.getDate(), myMonth: this.date.getMonth(), myHours: this.date.getHours(), myMinutes: this.date.getMinutes()});
      this.show = true;
      console.log(this.date.getDate(), this.date.getHours(), this.date.getMinutes());
    },

    editTask(index) {
      console.log(index, this.myData)
      this.show = !this.show;
      this.editIndex = index;
      this.isEdit = true;
      this.editedObj = this.myData[index].conObj;      
    },

    myTaskEdit(obj) {
      console.log(obj);

      this.myData[this.editIndex].conObj = obj.content;
      console.log(this.myData[this.editIndex])
      console.log(this.editedObj)
    },

    deleteTask(index){
      this.myData.splice(index, 1);
    },

    toggleModal() {
      this.show = !this.show;
      console.log(this.show);
    }
  }
}
</script>

<style>
#app {
  width: 60%;
  margin-left: auto;
  margin-right: auto;
}


.container{
  display: flex;
  flex-direction: column;
}

.header{
  width: 100%;
  height: 50px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.add-todo img{
  display: flex;
  align-items: center;
}

.main{
  display: flex;
  flex-direction: column;
}

li{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
}

.content{
  display: flex;
  column-gap: 5px;
  row-gap: 5px;
  grid-column-start: 2;
  grid-column-end: 3;
}

.check{
  display: flex;
  align-items: center;
}

.form-modal{
  top: 0;
  left: 0;
}

</style>
