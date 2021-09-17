<template>
 <h2>List</h2>
<div :key="index" v-for="(list,index) in todoList" 
    :class="{'done':list.status==='done'}"        
>
   <p>{{list.memo}} </p> 
   <button @click="$emit('statusControl',index,'done') " >DONE</button>
   <button @click="$emit('statusControl',index,'created' )" >BACK</button>
   <button @click="listEdit(list.memo,index)" > EDIT</button>
   <button @click="$emit('list-delete',index)">DEL</button>

</div>
</template>

<script>
export default {
    name: 'List',
    props: ['todoList'],
    emits: ['list-delete','statusControl','listEdit'],
    methods: {
        listEdit(memo,index) {
            this.$emit('listEdit',memo,index)

        }
    }
    
}
</script>

<style scoped>

    .done {
        background-color: rgba(0,0,0,0.1);
    }
    .done p {
        text-decoration: line-through;
        color: rgba(0,0,0,0.5);
    }

</style>