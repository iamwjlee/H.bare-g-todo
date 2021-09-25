<template>
  <div class="about">
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



export default {
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
</style>


