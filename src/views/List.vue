<template>
 <h2>{{titleList}}</h2>

 <div class="list-1">

     <div >
        <div class="container"   :key="index" 
                v-for="(list,index) in visibleTodoList" 
                :class="{'done':list.status==='done'}" >
        
            <div >
                <p>{{list.memo}} </p> 
            </div>
            
            <div>
                <button @click="$emit('statusControl',index,'done') " >DONE</button>
                <button @click="$emit('statusControl',index,'created' )" >BACK</button>
                <button @click="listEdit(list.memo,index)" > EDIT</button>
                <button @click="$emit('list-delete',index)">DEL</button>

            </div>

        </div>



     </div>
    <br>
    <div>
        <button v-if="showPreviousLink()" @click="updatePage(currnetPage-1)" > prev </button>
        {{currnetPage+1}} of {{totalPages()}}
        <button v-if="showNextLink()" @click="updatePage(currnetPage+1)" > next </button>

    </div>

 </div>
</template>

<script>
export default {
    name: 'List',
    props: ['todoList','titleList'],
    emits: ['list-delete','statusControl','listEdit'],
    beforeMount: function(){
        console.log('beforeMount in List')
        this.updateVisibleTodos();
    },
    data() {
        return {
            currnetPage: 0,
            pageSize: 3,
            visibleTodoList: []

        }
    },

    methods: {
        totalPages() {
            return  Math.ceil(this.todoList.length / this.pageSize)
        },
        showPreviousLink() {
            return this.currnetPage==0 ? false : true
        },
        showNextLink() {
            return this.currnetPage ==(this.totalPages()-1) ? false : true
        },
        listEdit(memo,index) {
            this.$emit('listEdit',memo,index)

        },
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

    }
    
}
</script>

<style scoped>
    .list-1 {
        
        height: 300px;
    }
    .container
    {
        display: flex;
        justify-content:  space-between;
        align-content: center;

    }    

    .done {
        background-color: #00000020;
        /* background-color: rgba(0,0,0,0.1); */
    }
    .done p {
        text-decoration: line-through;
        color: #00000050;
       /*  color: rgba(0,0,0,0.5); */
    }

</style>