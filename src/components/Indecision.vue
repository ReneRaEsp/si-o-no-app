<template>
  <img v-if="image" class="fondo"
  v-bind:src="image" alt="bg">
  <img v-else class="fondo"
  src="../assets/stars.gif" alt="bg">
  <div class="bg-dark"></div>
    <h1 class=""> SI O NO APP </h1>
  <div class="indecision-container">

      <input v-model="pregunta"
       type="text" placeholder="Hazme una pregunta">
      <p class="recordatorio">Recuerda terminar con un signo de interrogación (?)</p>

        <div>
            <h2 class="pregunta">{{ pregunta }}</h2>
            <p class="respuesta">{{ respuesta }}</p>
        </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            pregunta:'',
            respuesta: null,
            image: null
        }
    },
    watch: {
        pregunta(value, oldValue){

            if( !value.includes('?') ) return

            this.getAnswer()
        }
    },
    methods:{
        async getAnswer(){

            this.respuesta = 'Pensando...';
            
            const {answer, image} = await fetch('https://yesno.wtf/api').then(
                r => r.json()
            )
            this.respuesta = answer.toUpperCase()
            this.respuesta == 'YES' ? this.respuesta = 'SI' : null
            this.image = image

        }
    }
}
</script>

<style>
.fondo {
    width: 70vw;
    height: 100vh;
    position: absolute;
    z-index: -4;
    background-size: cover;
}
input {
    width: 90%;
    margin-bottom: 1rem;
    padding: .6rem;
    border-radius: .5rem;
    border: 0px solid rgba(0, 255, 255, 0);
}
h1 {
    margin-top: 1rem;
    font-weight: bold;
    font-size: 4rem;
    color: white;
}

.bg-dark {
    position: absolute;
    width: 70vw;
    height: 100vh;
    background: rgba(116, 112, 112, 0.187);
}
.recordatorio {
    color: rgb(177, 188, 205);
    font-weight: bold;
    font-size: 15px;
}
.indecision-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    top: 30vh;
    padding: 4rem;
    border: 2px solid rgba(60, 201, 187, 0.516);
    border-radius: 2rem;
    position: absolute;
    background: rgba(23, 31, 30, 0.201);
    z-index: 2;
    box-shadow: 4px 5px 40px 10px rgba(0, 255, 255, 0.414);
}
.pregunta{
    margin-top: 1.7rem;
    text-align: center;
    font-size: 20px;

    color: rgba(226, 231, 237, 0.914);
}

.respuesta{
    text-align: center;
    font-weight: bold;
    margin-top: 2rem;
    font-size: 50px;
    color: rgba(210, 244, 223, 0.852);
}

@media screen and (max-width: 900px) {
    .fondo, .bg-dark {
        width: 100vw;
    }
}


@media screen and (max-width: 540px) {
    .fondo, .bg-dark {
        top: 60vh;
        height: 40vh;
    }
    h1{
        font-size: 2rem;
    }
    .indecision-container {
        top: 8vh;
    }
}
</style>