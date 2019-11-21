<template>
  <div class="pokemon">
      <div class="imgPokemon" :style="{backgroundImage: 'url(' + imgSrc +')'}"></div>
      <h3 class="name">{{ name }}</h3>
      <p class="id">N° {{ id }}</p>
        <div class="allTypes">
            <p class="type" v-for="allTypes in types"
            :key="allTypes.slot" 
            >{{ allTypes.type.name }}</p>
        </div>
  </div>
</template>

<script>
export default {
    props: [
        'imgSrc', 'name', 'id', 'types'
    ]
}
</script>

<style scoped>
    .pokemon{
        width: 20%;
        text-align: center;
        margin: 20px 5%;
        border-radius: 30px;
        box-shadow: #9d9b9b 0 3px 5px;
        background-color: #ffffff;

    }
    .imgPokemon{
        min-height: 100px ;
        background-repeat: no-repeat;
        background-position: center;
        background-size: contain;
    }


    .allTypes{
        display: flex;
        margin: 2px 10px 10px;
        font-style: italic;
        border-radius: 15px;
    }

    .allTypes > p {
        background-color: rgba(177, 177, 177, 0.5);
        border-radius: 10px;
        margin: auto;
        padding: 7px 5px;
    }


@media screen and (max-width: 550px) {
    .pokemon{
        min-width: 80%;
        margin: 20px auto;
    }
}

@media screen and (max-width: 850px) {
    .pokemon{
        width: 40%;
        margin: 20px auto;
    }
}
</style>