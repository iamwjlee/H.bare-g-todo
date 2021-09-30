<template>
    <div>
        <div class="card" :class="flippedStyles"  @click="selectCard(0)" >
            <div  class="card-face front">
                1234
            </div>
            <div  class="card-face back">
                back
            </div>

        </div>
        <div class="card" @click="selectCard(1)" >
            <div v-if="visible[1]"  class="card-face front">
                1234</div>
            <div v-else class="card-face back">
                5678</div>

        </div>

    </div>

</template>

<script>
// vue.js transition 
// transition-group 
// https://ngio.co.kr/5542
// vue.js 컴포넌트간 전환
// vue.js 리스트 전환 리스트의 진입-진출-전환
// 비틀거리는 목록 전환
export default {
    name: 'Test',
    //props: 
    //emits:
    data() {
        return {
            visible: [false,false ],
        }
    },
    methods: {
        selectCard(index) {
           
            this.visible[index]=!this.visible[index]
             console.log('clicked ' + 'index=' +index +' visible='+this.visible[index] )
            
        }
    },
    computed: {
        flippedStyles() {
            console.log('flipped='+ this.visible[0])
            return this.visible[0]===true ? 'is-flipped':''
        }

    }

}
</script>

<style scoped>

.card {
    border: 5px solid #ccc;
    display: block;
    position: relative;
    width: 100px;
    height: 100px;
    margin: 10px;

    transition: transform 0.7s;
    transform-style: preserve-3d;


}
.card.is-flipped {
    transform: rotateY(180deg);

}
.card-face {
    width: 100%;
    height: 100%;
    position: absolute;  /* ?? */
   /*  -webkit-backface-visibility: hidden; */
     backface-visibility: hidden;  
}
.card-face.front {
    /* background-color: red; */
    background-image: url('/images/card-bg.png');
    color: white;
         transform: rotateY(180deg);    

     /*  */

}
.card-face.back {
    background-image: url('/images/card-bg-empty.png');

    color: white;
 
}
.shuffle-card-move {
    transition: transform 0.8s ease-in;
}
</style>