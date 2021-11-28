<template>
  <div id="app">
      <div class="container align-center">
        <!-- Add Field -->
        <div class="row" v-if="isEditing">
           <div class="col-11 mt-3">
              <input type="text" class="form-control shadow" placeholder="Please Write Your TodoList !" v-model="inputModel" @keyup.enter="addToList">
            </div>
            <div class="col-1 mt-3">
              <button type="button" class="btn btn-success shadow" @click="addToList">Add</button>
            </div>
        </div>
        <!-- Update Field -->
        <div class="row" v-else>
           <div class="col-11 mt-3">
              <input type="text" class="form-control shadow" placeholder="Please Write Your Updated List !" v-model="inputModel" @keyup.enter="updateToList">
            </div>
            <div class="col-1 mt-3">
              <button type="button" class="btn btn-warning shadow" @click="updateToList">Update</button>
            </div>
        </div>
        <!-- List Field -->
        <div class="row">
            <div class="col-12 mt-3">
              <ul class="list-group shadow">
                  <li class="list-group-item" v-for="(ourList,index) in ourLists" :key="ourList">
                     <b>{{ index }}.</b>  {{ ourList }} 
                     <button type="button" class="btn btn-danger float-end shadow-sm" style="margin-right:5px;" @click="deleteToList(index)">Delete</button>
                     <button type="button" class="btn btn-warning float-end shadow-sm" style="margin-right:5px;" @click="editToList(index, ourList)">Edit</button>
                  </li>
              </ul>
            </div>
                
          
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      ourLists: [],
      inputModel: "",
      selectedIndex: null,
      isEditing: true
    }
  },
  methods: {
    addToList(){
      if(this.inputModel != ""){
        this.ourLists.push(this.inputModel);
        this.inputModel = "";
      }
    },
    deleteToList(index){
      this.ourLists.splice(index,1);
    },
    editToList(index, ourList){
      this.inputModel = ourList
      this.selectedIndex = index
      this.isEditing = false
    },
    updateToList(){
      this.ourLists.splice(this.selectedIndex,1,this.inputModel)
      this.isEditing = true;
      this.inputModel = ""
    }
  }
}
</script>

<style>
body{
  margin: 0;
  padding: 0;
  background-color: rgba(223, 228, 234,1.0);
}
</style>
