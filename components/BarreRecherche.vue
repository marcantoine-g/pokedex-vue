<template>
  <div class="recherche">
      <div class="cercleG"></div>
      <h3>Une idée en tête ?</h3>
      <p>Vous pouvez chercher ici un Pokémon en particulier, selon son nom ou son ID</p>
      <form @submit="onSubmit">
        <input class="input" v-model="id" placeholder="Nom ou ID du Pokémon à chercher"/>
        <button class="bouton_submit" type="submit"></button>
      </form>
      <div class="cercleD"></div>
  </div>
</template>

<script>
export default {
    data(){
        return {
            id: ""
        };
    },
    methods: {
        onSubmit(e){
            e.preventDefault();
            this.id = this.id.replace(/\s/g,"");
            if (this.id != ""){
                this.id = this.id.toLowerCase();
                this.$emit("idRecherche", this.id);
                this.id="";
            }
        }
    }
}
</script>

<style scoped>
.recherche{
    position: relative;
    height: 25vh;
    background-color:  #ed1c24;
    margin-bottom: 5%;
    padding: 20px;
    display: grid;
    grid-template-columns: 10% 1fr 1fr 10%;
    grid-template-rows: 5% 1fr 1fr 5%;
    overflow: hidden;
}
h3{
    grid-column: 2;
    grid-row: 2;
    color:  #ffffff;
    font-size: 48px;
    font-weight: bold;
    align-self: center;
}
p{
    grid-column: 3;
    grid-row: 1/4;
    color: white;
    font-size: 36px;
    align-self: center;
    text-align: center;
}
.bouton_submit{
    background-image: url("/loupe.svg");
    background-size: cover;
    border: none;
    background-color: rgba(0, 0, 0, 0);
    background-repeat: no-repeat;
    cursor: pointer;
    width: 40px;
    height: 40px;
    margin: auto 10px;
}
.input{
    border-radius: 35px;
    border: solid black 5px;
    min-width: 70%;
    padding: 5px 20px;
    height: 3rem;
}
form{
    display: flex;
    grid-column: 2;
    grid-row: 3;
    align-self: center;
}
.cercleG{
    position: absolute;
    background-color: #ffffff;
    width: 200px;
    height: 100%;
    border-radius: 250px;
    left: -150px;
    border: black solid 10px;
}
.cercleD{
    position: absolute;
    background-color: #ffffff;
    width: 200px;
    height: 100%;
    border-radius: 250px;
    right: -150px;
    border: black solid 10px;
}

@media screen and (max-width: 920px){
    .cercleD, .cercleG{
        display: none;
    }
    h3{
        font-size: 35px;
    }
    p {
        font-size: 25px;
    }
}
@media screen and (max-width: 550px){
    .recherche{
        grid-template-columns: 1% 1fr 1%;
        grid-template-rows: 5% 1fr 1fr 1fr 5%;
    }
    h3{
        font-size: 20px;
        grid-column: 2;
        grid-row: 2;
        text-align: center;
    }
    p{
        font-size: 16px;
        grid-column: 2;
        grid-row: 3;
        padding-bottom: 15px;
    }
    form{
        grid-column: 2;
        grid-row: 4;
        justify-content: center;
    }
    .bouton_submit{
        width: 30px;
        height: 30px;
    }
    .input{
        height: 40px;
    }
}

</style>