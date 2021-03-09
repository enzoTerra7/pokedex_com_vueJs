<template>
  <div>
  
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="currentImg" @click="changeImg">
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{num}} - {{name | upperFirstCase}}</p>
            <div id="containerBtn">
              <p :class="pokemon.type" id="btn">{{pokemon.type}}</p>
              <p v-if="pokemon.secondType.length > 0" :class="pokemon.secondType" id="btn">{{pokemon.secondType}}</p>
            </div>
          </div>
        </div>

        <div class="content">
        </div>
      </div>
    </div>

  </div>
</template>

<script>
// ======= Libs ========
import axios from 'axios'

export default {
  data(){
    return{
      isFront: true,
      currentImg: '',
      pokemon: {
        secondType: '',
        type: '',
        back: '',
        front: '',
      }
    }
  },
  props: {
    num: Number,
    name: String,
    url: String
  },
  filters: {
    upperFirstCase: function(value){
      let newName = value[0].toUpperCase() + value.slice(1)
      
      return newName
    }
  },
  created: function() {
    axios.get(this.url).then(answer =>{
      this.pokemon.type = answer.data.types[0].type.name
      this.pokemon.back = answer.data.sprites.back_default
      this.pokemon.front = answer.data.sprites.front_default
      this.currentImg = this.pokemon.front
      this.pokemon.secondType = answer.data.types[1].type.name
    })
  },
  methods: {
    changeImg: function (){
      if(this.isFront == true){
        this.isFront = false
        this.currentImg = this.pokemon.back
      } else if(this.isFront == false) {
        this.isFront = true
        this.currentImg = this.pokemon.front
      }
    }
  }
}
</script>

<style>
  #containerBtn{
    display: flex;
    width: 100%;

    justify-content: space-evenly;
    align-items: center;
  }
  #btn{
    width: 45%;
    box-sizing: border-box;
    padding: .3rem 0 .5rem 0;
    border-radius: 25px;
    margin: 0 auto;
    text-align: center;
  }
  .water{
    background: rgb(101, 166, 223);
    color: white
  }
  .fire{
    background: rgb(206, 57, 57);
    color: white
  }
  .grass{
    background:rgb(47, 255, 57);
    color: white
  }
  .bug{
    background: rgb(2, 95, 2);
    color: white
  }
  .normal{
    background: rgb(241, 241, 186);
    color: rgb(122, 122, 122);
  }
  .electric{
    background: rgb(234, 255, 41);
    color: rgb(112, 112, 112)
  }
  .bug{
    background: rgb(2, 95, 2);
    color: white
  }
  .poison{
    background: rgb(102, 0, 102);
    color: white
  }
  .ground{
    background: rgb(196, 148, 28);
    color: white
  }
  .fairy{
    background: pink;
    color: white
  }
  .fighting{
    background: firebrick;
    color: white
  }
  .psychic{
    background: palevioletred;
    color: white
  }
  .rock{
    background: rgb(102, 70, 14);
    color: white
  }
  .ghost{
    background: rgb(145, 70, 132);
    color: white
  }
  .ice{
    background: rgb(165, 255, 225);
    color: rgb(122, 122, 122)
  }
  .dragon{
    background: rgb(2, 50, 95);
    color: white
  }
  .flying{
    background: rgb(160, 187, 212);
    color: rgb(122, 122, 122)
  }
  .steel{
    background: rgb(118, 128, 136);
    color: white
  }
  .dark{
    background: rgb(49, 49, 49);
    color: white
  }
</style>