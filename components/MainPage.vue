<template>
  <section id="mainPage" class="container">
    <BarreRecherche id="barreDeRecherche" v-on:idRecherche="getId"/>
    <div class="pokedex">
    <Pokemon v-for="pokemon in pokemons"
    :key="pokemon.id"
    :name="pokemon.data.name"
    :id="pokemon.id"
    :types="pokemon.data.types"
    :imgSrc="pokemon.data.sprites.front_default"
    /> 
    </div>
    <a href="#mainPage" class="arrow_button"></a>
    <button v-on:click="chargerPokemons" class="charger">Charger plus de Pokémons !</button>
  </section>
</template>





<script>
import BarreRecherche from "@/components/BarreRecherche.vue";
import Pokemon from "@/components/Pokemon.vue";
import axios from 'axios';

export default {
  components:{
    BarreRecherche,
    Pokemon,
  },

  data () {
    return {
      pokemons: [],
      startNbPokemons: 1,
      nbPokemons: 9,
      chercher: false,
      options: {},
      observer: null
    }
  },

  methods:{
    async getId(idRecherche) {
      axios.get(`https://pokeapi.co/api/v2/pokemon/${idRecherche}`)
      .then( response => {
        this.pokemons = [];
        this.pokemons.push({"id" : response.data.id, "data": response.data});
        this.chercher = true;
        document.getElementsByClassName("charger")[0].textContent = "Afficher les premiers Pokémons !";
      })
      .catch((error)=>{
        alert('Le Pokémon spécifié n\'a pas été trouvé');
      });
    },

    async chargerPokemons(){
      if (this.chercher){
        this.startNbPokemons = 1;
        this.nbPokemons = 9;
        this.pokemons.splice(0,1);
        document.getElementsByClassName("charger")[0].textContent = "Charger plus de Pokémons !";
        this.chercher = false;
      } else {
        this.startNbPokemons+=9;
        this.nbPokemons+=9;
      }

      for (let i = this.startNbPokemons; i <= this.nbPokemons; i++) {
        axios.get(`https://pokeapi.co/api/v2/pokemon/${i}`)
        .then( response =>{
          this.pokemons.push({ "id" : response.data.id, "data": response.data});
          this.pokemons.sort((id1, id2)=>{
            return id1.id > id2.id ? 1 : -1;
          });
        });
    }
    }
  },

  mounted() {
    // Affichage des premiers Pokémons
    for (let i = this.startNbPokemons; i <= this.nbPokemons; i++) {
      axios.get(`https://pokeapi.co/api/v2/pokemon/${i}`)
      .then( response =>{
        this.pokemons.push({ "id" : response.data.id, "data": response.data});
        this.pokemons.sort((id1, id2)=>{
          return id1.id > id2.id ? 1 : -1;
        });
      }); 
    }
  
    //Initialisation de l'Observer
    this.options = {
      root: null,
      rootMargin: '-50%',
      threshold: 0
    }
    this.observer = new IntersectionObserver(function (entries, self){
      let arrow_button = document.getElementsByClassName('arrow_button')[0];
      if(entries[0].isIntersecting == false){
        arrow_button.style.visibility = 'hidden';
        arrow_button.style.opacity = '0';
      } else {
        arrow_button.style.visibility = 'visible';
        arrow_button.style.opacity = '1';
      }
    }, this.options);
    this.observer.observe(document.getElementsByClassName('pokedex')[0]);

  }

}
</script>

<style scoped>
.container{
  position: relative;
  height: 100%;
  background-image: url("/wallpaper_poke3.jpg");
  padding: 100px 0;
}

.pokedex{
    display: flex;
    flex-flow: wrap;
    width: 65%;
    height: auto;
    border-radius: 35px;
    padding: 20px 0;
    margin: 10vh auto;
    justify-content: center;
    background-color: #eaeaead5;
    
}
.arrow_button{
  visibility: hidden;
  position: fixed;
  bottom: 20px;
  right: 20px;
  height: 50px;
  width: 50px;
  background-color: black;
  background-image: url('/arrow.svg');
  background-size: 50%;
  background-repeat: no-repeat;
  background-position: center;
  border: solid white 2px;
  border-radius: 50px;
  transition: 0.3s;
}
.charger{
  display: flex;
  background-color: black;
  height: 100px;
  width: 300px;
  margin: auto;
  border-radius: 35px;
  border: none; 
  cursor: pointer;
  color: #ffffff;
  text-align: center;
  font-size: 24px;
  font-weight: bold;
  align-items: center;
  box-shadow: #9d9b9b 0 2px 2px;
  transition: 0.3s;
}
.charger:hover{
  background-color: white;
  border: solid black 5px;
  color: black;
  transform: translateY(-5px);
}
.arrow_button:hover{
  transform: translateY(-5px);
}



@media screen and (max-width:550px){
  .pokedex{
    flex-direction: column;
    justify-content: center;
  }
}
</style>
