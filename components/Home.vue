<template>
  <div class="container">
    <h1>POKEDEX</h1>
    <h2>
      Bienvenue sur mon Pokédex en Ligne !
      <br />
      <br />Vous trouverez ci-dessous les Pokémons connus à ce jour
    </h2>
    <a href="#mainPage" class="scroll">
      <svg width="40" height="90" viewBox="0 0 50 130">
        <rect id="scroll" x="0" y="5" rx="25" ry="25" width="40" height="80" stroke="#000" fill="#FFF" stroke-width="4"></rect>
        <circle id="circle--shape" cx="20" cy="32" r="8" fill="#000"></circle>
      </svg>
    </a>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.container {
  position: relative;
  overflow: hidden;
  display: grid;
  grid-template-columns: 1% 1fr 1fr 1%;
  grid-template-rows: 1fr 1fr 1fr 50px;
  background-image: url("/pokeball_bg.svg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 20vw -20vh;
}
h1 {
  font-weight: bold;
  font-size: 120px;
  color: #ffffff;
  background: black;
  padding: 0 1rem;
  grid-column: 2;
  grid-row: 2;
  align-self: center;
  text-align: center;
  justify-self: center;
  width: min-content;
  animation: animateTitle 0.5s ease-in;
}
h2 {
  grid-column: 2;
  grid-row: 3;
  font-weight: bold;
  font-size: 30px;
  text-align: center;
  animation: animateSubtitle 1.5s ease-in;
}
.scroll {
  position: absolute;
  background-image: url("/scrollDown.svg");
  background-size: contain;
  height: 50px;
  width: 50px;
  bottom: 3vh;
  left: 50%;
}
#circle--shape {
  animation: animateScroll 1.3s linear infinite;
  animation-delay: 2s;
}
@keyframes animateScroll {
    100%{
      transform: translateY(30px);
      opacity: 0.2;
    }
}
@keyframes animateTitle {
  0%{
    opacity: 0;
    transform: translateY(-80px);
  }
  100%{
    opacity: 1;
    transform: translateY(0px);

  }  
}
@keyframes animateSubtitle {
  0%{
    opacity: 0;
  }
  50%{
    opacity: 0 ;
  }
  100%{
    opacity: 1;
  }
}


@media screen and (max-width: 550px) {
  .container {
    background-position: 0vw -10vh;
  }
  h1{
    font-size: 100px;
  }
  h2{
    font-size: 20px;
  }
}


</style>