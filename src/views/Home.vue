<template>
  <div class="home">
    <h2>Home</h2>
    <header>
      <div> 
        <p>button block test</p>
      </div>
      <div>
        <Button @click="updatePage(1)" text="buttonTest1" color="gray" />
        <Button @click="updatePage(0)" text="buttonTest2" color="yellow" />
   
  
      </div>
    </header>
    <hr>
    <List  
        titleList="List"
        :todoList="todoList"
        @statusControl="statusControl"
        @list-delete="listDelete" 
        @listEdit="listEdit" />
    <hr>
    <ListAdd 
        titleListAdd="ListAdd"
        @list-add="listAdd" 
        @listEdit="listEdit2" />
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
        {memo: '2222222'},
        {memo: '33333'},
        {memo: '4444444'},
        {memo: '555555'},
        {memo: '6666666'},
        {memo: '7777777'}

      ],
      currnetPage: 0,
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
    console.log('beforeMount')
    this.updateVisibleTodos();
  },
  methods: {

    updatePage(pageNumber) {
      this.currnetPage=pageNumber
      console.log(pageNumber)
      this.updateVisibleTodos();
    },
    updateVisibleTodos() {

      this.visibleTodoList = this.todoList.slice(this.currnetPage*this.pageSize,
        (this.currnetPage*this.pageSize) + this.pageSize )

      //if no visible page to back page
      if(this.visibleTodoList.length== 0 && this.currnetPage > 0) {
        console.log('last')
        this.updatePage(this.currnetPage-1)
      }

      for(let i=0;i<this.visibleTodoList.length;i++)
      console.log(this.visibleTodoList[i])

    },
    listAdd(memo) {
      console.log(memo)
      this.todoList.push( {memo: memo,status: 'created'})
      //this.updateVisibleTodos()

    },
    listDelete(index) {
      console.log('delete')
      this.todoList.splice(index,1) 
    },
    statusControl(index,status) {
      this.todoList[index].status=status
    },
    listEdit(memo,index) {
      const aa={
        memo: memo,
        index:index
      }
      this.emitter.emit('e-msg',aa)

    },
    listEdit2(memo) {
      this.todoList[memo.index].memo=memo.memo

    }
  }
}
</script>


<style scoped>
header {
  display: flex;
  justify-content:  space-between;
  align-content: center;
  margin-bottom: 1px;
  justify-items: center;
}
.btn {
  border-radius: 2px;
  border: none;
  font-size: 15px;
}

</style>