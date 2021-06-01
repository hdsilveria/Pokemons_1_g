<template>
<div>

<div id="cardPoke" class="w3-card-4 w3-left w3-margin">
        <h3>{{name | upper}} </h3>

        <img :src="CardPoke.sprites.front_default" v-show="front">
        <img :src="CardPoke.sprites.back_default" v-show="back">

    <div class="w3-container w3-center">
        <button class="w3-button w3-white w3-hover-white" @click="mudaIMG">◀️</button>
        <button class="w3-button w3-white w3-hover-white" @click="mudaIMG">▶️</button>
    </div>
</div>

</div>  
</template>

<script>

import axios from 'axios';

export default {


    created: function(){
    axios.get(this.url).then(response =>{
        this.CardPoke = response.data;
        console.log(this.CardPoke)
    })
  },

    data(){
        return {
            CardPoke: [],
            front: true,
            back: false
        }
    },

    props: {
        name: String,
        url: String
    },

    filters: {
        upper: function(value){
            var newValue = value[0].toUpperCase() + value.slice(1);
            return newValue;
        }
    },

    methods: {
        mudaIMG: function(){
            this.front = !this.front;
            this.back = !this.back
        }
    }
}

</script>

<style>

#cardPoke {
    width: 200px;
    background-color: rgb(255, 255, 255);
}


</style>