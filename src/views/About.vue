<template>
  <div class="about">

    <section class="game-board">
      <Card 
        v-for="(card,index) in cardList" 
        :key="`card-${index}`" 
        :visible="card.visible"
        @select-card="flipCard"
        :position="card.position"
        :matched="card.matched"
        :value="card.value" />
    </section>
    <button @click="shuffleCards" >Shuffle Cards</button>
    <button @click="restartGame" >Restart Game</button>
    <h2> {{userSelection}}  </h2>
    <h2> {{status}}  </h2>
    <p>remainingPairs: {{remainingPairs}} </p>

    <br>


    <button @click="darkMode=!darkMode">Clik me</button>
    <div class="textbox" :class="{'dark':darkMode}" >
      This is an about page

      How you can use the dynamic style and class attributes in vue js. 
      I explain to you step by step these important key features, 
      class and style binding with v-bind:class and v-bind:style in vue js. 
      After this tutorial, you understand how you can use dynamic styling in your template. Enjoy watching.
      You like this video? 
      <br>
      See the next one: https://youtu.be/co38qQzgDFM
      <br>
      https://codepen.io/tutsplus/pen/XejpWb

    </div>
    <hr>
    <button @click="test1" > get Object.keys </button> <br>
    <button> Test2 </button> <br> <br>

      <div class="sort-orders">
        <a v-for="(sortKey,index) in Object.keys(orderedListOptions)" :key="index" 
            @click="sortOder=sortKey"
            :class="{active: sortOder==sortKey}"
        >
          {{sortKey}}
        </a>

      </div>

     <ul>
       <li v-for="(item,index) in sort(sortOder)" :key="index" >
         {{item}}
       </li>

     </ul>


  </div>
</template>

<script>
import _ from 'lodash'
import {ref,watch,computed} from 'vue'
import Card from './Card'
export default {
  name: 'About',
  components: {
    Card,
  },
  setup() {
    // const cardList= [] 
    const cardList=ref([])
    const userSelection=ref([])
    //const status= ref('')
    const status=computed(()=>{
      if(remainingPairs.value==0) return 'Player wins!'
      else return `Remaining Pairs: ${remainingPairs.value}`

    })
    const remainingPairs=computed(()=>{
      const remainingCards=cardList.value.filter(card=>card.matched===false).length
      return remainingCards/2

    })
    const shuffleCards = ()=>{
      cardList.value=_.shuffle(cardList.value)

    }
    const restartGame=()=>{
      shuffleCards()
      cardList.value=cardList.value.map((card,index)=>{
        return {
          ...card,
          matched: false,
          visible: false,
          position: index,
        }
      })

    }

    const cardItems = [1,2,3,4,5,6,7,8]
    cardItems.forEach(item=>{
      cardList.value.push({
          value: item,
          visible: false,
          position: null,
          matched: false

      })  
      cardList.value.push({
          value: item,
          visible: false,
          position: null,
          matched: false

      })  
      
    })

    cardList.value=cardList.value.map((card,index)=>{
      return {
        ...card,
        position: index
      }
    })

    // for(let i=0;i<16;i++) cardList.value.push({
    //     value: 8,
    //     visible: false,
    //     position: i,
    //     matched: false

    // })
    const flipCard=(payload)=>{
      cardList.value[payload.position].visible=true

      if(userSelection.value[0]) {
        //
        if( userSelection.value[0].position===payload.position  &&
             userSelection.value[0].faceValue ===   payload.faceValue) {
          return
        } 
        else {
          userSelection.value[1]=payload
        }
      }
      else {
        userSelection.value[0]=payload
      }
    }
    watch(userSelection, (currentValue)=>{
      console.log(currentValue)
      if(currentValue.length===2) {
        const cardOne=currentValue[0]
        const cardTwo=currentValue[1]

        if(cardOne.faceValue===cardTwo.faceValue) {
          //status.value='Matched!'
          cardList.value[cardOne.position].matched=true
          cardList.value[cardTwo.position].matched=true
        }
        else {

          //status.value='Mismatch'
          setTimeout(()=>{
          cardList.value[cardOne.position].visible=false
          cardList.value[cardTwo.position].visible=false
          },2000)

        }

        //console.log("That's it!")
        userSelection.value.length=0
      }
    },{deep:true})
    
    return {
      cardList,
      flipCard,
      userSelection,
      status,
      //remainingPairs
      shuffleCards,
      restartGame,
    }
  },
  data() {
    return {
      darkMode:false,
      list: [
      "Michael Gary Scott",
        "Dwight Schrute",
        "Jim Halpert",
        "Pam Beesly-Halpert",
        "Darryl Philbin",
        "Erin Hannon",
        "Andy Bernard",
        "Phyllis Lapin-Vance",
        "Stanley Hudson",

      ],
      sortOder: "A-Z",
    }
  },
  computed: {
    orderedListOptions() {
      return {
        "Popularity" : () =>{
          return  this.list
        },
        "A-Z" : ()=>{
          return this.list.slice().sort()
        },
        "Z-A" : ()=>{
          return this.list.slice().sort().reverse()
        }

      }
    },

  },
  methods: {
  

    sort(sortOder) {
      return this.orderedListOptions[sortOder]()
    },
    test1() {
      console.log('test1')
      console.log(Object.keys(this.orderedListOptions))

    }

  }
}
</script>


<style scoped>
  body {
    margin: 0;
    padding: 0;
  }
  .textbox {
    width: calc(100%-40px);
    background-color: #fff;
    color: #222;
  }

 .dark {
    background-color: #222;
    color: #fff;
  }
  .sort-orders a{
    background: #999;
    padding: 10px 10px;
    margin: 1px 10px 0 0;
    cursor: pointer;


  }
  .sort-orders a.active {
    background: #49b293;
  }


  .game-board {
    display: grid;
    grid-template-columns: 100px 100px 100px 100px;
    grid-template-rows: 100px 100px 100px 100px;
    column-gap: 30px;
    row-gap: 30px;
    justify-content: center;
  }
</style>


