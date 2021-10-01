<template>
    <div>
        <button @click="show=!show" >Toggle Render</button>
        <transition name="fade" >
            <p v-if="show" >hello </p>
        </transition>
        <hr>
        <p>
        <button @click="doAdd" >Add</button>
        <button @click="current=1" >Total</button>
        <button @click="current=n" v-for="n in [3,5]" :key="n" > multiple by {{n}} </button>


        </p>

        <transition-group  tag="ul" class="list"
            @before-enter="beforeEnter"
            @after-enter="afterEnter"
            @enter-cancelled="afterEnter"
        
        >
            <li v-for="(item,index) in filteredList"
                :key="item"
                :data-index="index"
                class="item"
                @click="doRemove(item)"


            >
            {{item}}
            </li>

        </transition-group>
    
    </div>

</template>

<script>
export default {
    name: 'Demo',
    data() {
        return {
            current: 1,
            list: [1,2,3,4,5,6,7,8,9,10],
            addEnter: false,
            show: true,

        }
    },
    computed: {
        filteredList() {
            return this.list.filter(el=>el%this.current ===0)
        }
    },
    props: [],
    methods: {
        doRemove(item) {
            this.list.splice(this.list.indexOf(item),1)
        },
        doAdd() {
            this.addEnter=true
            const newNumber=Math.max.apply(null,this.list)+1
            const index=Math.floor(Math.random()*(this.list.length+1))
            this.list.splice(index,0,newNumber)

        },
        //
        // transition은  css의 변화를 동적으로 변환해 준다 
        //
        beforeEnter(el){ //트랜지션을 시작할때 apply index*100ms delay
            this.$nextTick(()=>{
                if(!this.addEnter) {
                    el.style.transitionDelay=100*parseInt(el.dataset.index,10)+'ms'
                }
                else {
                    this.addEnter=false
                }
            })
            //el.style.transitionDelay=300*parseInt(el.dataset.index,10)+'ms'
        }
        ,
        afterEnter(el) { //finish transition or cencel, remove delay  
            el.style.transitionDelay=''
        }
    },

}
</script>

<style scoped>

/*transition style   
    요소의 추가,삭제,변경시 발생
    진입하는 순가 enter
    v-enter
    v-enter-active
    v-enter-to

    v-leave
    v-leave-active
    v-leave-to

    vue transiton tag 
    1. transition
    2. transition-group

*/
.fade-enter-active,
.fade-leave-active
{
    transition: all  .8s;
}

.fade-enter-from, 
.fade-leave-to {
    transform: translateX(50px);
    opacity: 0;
}


.v-enter-active, 
.v-leave-active,
.v-move {
    transition:  opacity 1s , transform 1s;
}
.v-leave-active {
    position: absolute;
}
.v-enter {
    opacity: 1;
    transform:  translateY(-20px);
}
.v-leave-to {
    opacity: 0;
    transform: translateY(20px);
}


button {
    padding: 10px 10px 10px 10px;
    margin-left: 10px;
}
.list {
    width: 360px;
    padding: 0px 0px 0px 0px;
    background-color: #777;
}
.item {
    display: inline-flex;
    justify-content: center;
    align-items: center;
    background: #f5f5f5;
    width: 40px;
    height: 40px;
    margin: 4px;  
    padding: 10px 10px 10px 10px; 
}


</style>