<template>
<div>
    <h2>{{titleListAdd}}</h2>
    <textarea name="" id="" cols="60" rows="10" v-model="memo" ></textarea> <br>
    memo : {{memo}}
    <br>
    <button @click="listAdd" >List ADD </button>
    <button @click="listEdit" >List EDIT </button>

</div>
</template>

<script>
export default {
    name: 'ListAdd',
    props: ['titleListAdd'],
    emits: ['list-add','listEdit'],
    data() {
        return {
            memo: '',
            index: ''

        }
    },
    created() {
        this.emitter.on('e-msg',this.eventfunction)
    },
    methods: {
        eventfunction(d) {
            this.memo=d.memo
            this.index=d.index
            
        },
        listAdd() {
            if(!this.memo) return
            console.log('click')
            this.$emit('list-add',this.memo)
            this.memo=''
        },
        listEdit() {
            this.$emit('listEdit',{memo: this.memo,index: this.index })
        }
    }

}
</script>