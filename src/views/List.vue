<template>
 

 <div class="list-1">
<h2>{{titleList}}</h2>
     <div >
        
        <div class="container"   :key="index" 
                v-for="(list,index) in visibleTodoList" 
                :class="{'done':list.status==='done'}" >
        
            <div class="item">
                <p>{{list.memo}} </p> 
            </div>
            
            <div class="item2">
                <button @click="$emit('statusControl',index,'done') " >DONE</button>
                <button @click="$emit('statusControl',index,'created' )" >BACK</button>
                <button @click="listEdit(list.memo,index)" > EDIT</button>
                <button @click="$emit('list-delete',index)">DEL</button>

            </div>

        </div>



     </div>
    <br>
    <div>
        <!-- <button v-if="showPreviousLink()" @click="updatePage(currentPage-1)" > prev </button> -->
        <button v-if="showPreviousLink()" @click="$emit('prevLink')" > prev </button>
        {{currentPage+1}} of {{totalPages}}
        <button @click="$emit('nextLink')" > next </button>

    </div>

 </div>
</template>

<script>
export default {
    name: 'List',
    props: ['visibleTodoList','titleList','pageSize','currentPage','totalPages'],
    emits: ['list-delete','statusControl','listEdit','nextLink','prevLink'],
    data() {
        return {
        }
    },
    methods: {
        showPreviousLink() {
            return this.currentPage==0 ? false : true
        },
        showNextLink() {

            return this.currentPage ==(this.totalPages-1) ? false : true

        },
        listEdit(memo,index) {
            this.$emit('listEdit',memo,index)

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
        justify-content: space-between;
        align-items: center;
        background-color: beige;
        padding: 4px 4px;
        margin-bottom: 5px;
    }    
    .item {
        font-size: 13px;
        padding: 1px 1px;
    }
    .item2 button{
        font-size: 12px;
        padding:1px 10px;
        margin-right: 3px;
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