<template>
  <div class="home">
    <h2>Home</h2>
    <hr>
    <List  :todoList="todoList"
            @statusControl="statusControl"
            @list-delete="listDelete" 
            @listEdit="listEdit"
            />
    <hr>
    <ListAdd @list-add="listAdd" 
             @listEdit="listEdit2"
    />
    <hr>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'

import List from './List.vue'
import ListAdd from './ListAdd.vue'

export default {
  name: 'Home',
  data() {
    return {
      todoList: [],
    }
  },
  components: {
    List,
    ListAdd
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
