<template>
  <div class="home">
    <h2>Home</h2>
    <header>
      <p>button block test</p>
      <!-- send button name, color -->
      <Button text="buttonTest1" color="gray" />
<!--       <Button text="buttonTest2" color="yellow" />
 -->    
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
      todoList: [],
    }
  },
  components: {
    List,
    ListAdd,
    Button
    //HelloWorld
  },
  methods: {
    listAdd(memo) {
      console.log(memo)
      this.todoList.push( {memo: memo,status: 'created'})

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
}
.btn {
  display: inline-block;
  border-radius: 2px;
  border: none;
  font-size: 15px;
}

</style>