<template>
  <div class="home">
    <h2>Home</h2>
    <header>
      <div> 
        <p>buttonVue test</p>
      </div>
      <div >
        <Button @click="testButton1" text="buttonTest1" color="gray" />
        <Button @click="testButton2" text="buttonTest2" color="yellow" />
        <Button @click="testButton3" text="buttonTest3" color="yellow" />
   
  
      </div>
    </header>
    <hr>
    <List  
        :totalPages="totalPages()"
        :pageSize="pageSize"
        :currentPage="currentPage"
        titleList="List"
        :visibleTodoList="visibleTodoList"
        @nextLink="updatePage(currentPage+1)"
        @prevLink="updatePage(currentPage-1)"
        @statusControl="statusControl"
        @list-delete="listDelete" 
        @listEdit="listEdit" />
    <hr>
    <ListAdd 
        titleListAdd="ListAdd"
        @list-add="listAdd" 
        @listEdit="listAddEdit" />
    <hr>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
//pagenation ??
//https://techblog.woowahan.com/2672/


import List from './List.vue'
import ListAdd from './ListAdd.vue'
import Button from './Button.vue'

export default {
  name: 'Home',
  data() {
    return {
      todoList: [
        {memo: '111111'},
        {memo: '222222'},
        {memo: '333333'},
        {memo: '444444'},
        {memo: '555555'},
        {memo: '666666'},
        {memo: '777777'}

      ],
      currentPage: 0,
      pageSize: 3,
      visibleTodoList: []

    }
  },
  components: {
    List,
    ListAdd,
    Button
    //HelloWorld
  },
  beforeMount: function(){
    console.log('beforeMount in Home')
    this.updateVisibleTodos();
  },
  methods: {

    saveFile: function() {
      const data=JSON.stringify(this.todoList)
      window.localStorage.setItem('myTodo',data)
      console.log(JSON.parse(window.localStorage.getItem('myTodo')))

    },
    testButton1() {
      console.log(JSON.parse(window.localStorage.getItem('myTodo')))
      //updatePage(0)
    },
    testButton2() {
      for(let i=0;i<this.todoList.length;i++)
        console.log(this.todoList[i])
      this.saveFile()

    },
    testButton3() {
      this.pageSize=10
      this.updateVisibleTodos();
    },
    totalPages() {
        return   Math.ceil(this.todoList.length / this.pageSize)
    },


    updatePage(pageNumber) {
      this.currentPage=pageNumber
      console.log(pageNumber)
      this.updateVisibleTodos();
    },
    updateVisibleTodos() {
      
      this.visibleTodoList = this.todoList.slice(this.currentPage*this.pageSize,
        (this.currentPage*this.pageSize) + this.pageSize )

      //if no visible page to back page
      if(this.visibleTodoList.length== 0 && this.currentPage > 0) {
        console.log('last')
        this.updatePage(this.currentPage-1)
      }
      console.log(this.currentPage)
      console.log(this.pageSize)

      console.log(this.visibleTodoList.length)

      for(let i=0;i<this.visibleTodoList.length;i++)
        console.log(this.visibleTodoList[i])

    },
    listAdd(memo) {
      console.log(memo)
      this.todoList.push( {memo: memo,status: 'created'})
      this.updateVisibleTodos()

    },
    listDelete(index) {
      console.log('delete')
      this.todoList.splice(index,1) 
      this.updateVisibleTodos()
    },
    statusControl(index,status) {
      console.log(index,status,this.currentPage)
      this.visibleTodoList[index].status=status
      this.todoList[this.currentPage*this.pageSize+index].status=status
      this.updateVisibleTodos()

    },
    listEdit(memo,index) {
      const aa={
        memo: memo,
        index:index
      }
      this.emitter.emit('e-msg',aa)

    },
    listAddEdit(memo) {
      this.visibleTodoList[memo.index].memo=memo.memo
      this.todoList[this.currentPage*this.pageSize+memo.index].memo=memo.memo

      //this.todoList[memo.index].memo=memo.memo

    }
  }
}
</script>


<style scoped>
header {
  display: flex;
  justify-content:  space-between;
  align-items: center;
  margin-bottom: 1px;
  justify-items: center;
}
.btn {
  border-radius: 2px;
  border: none;
  font-size: 15px;
}

header button {
  margin-right: 5px;
}


</style>