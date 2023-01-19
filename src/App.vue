<template>
  <div id="app">
    <h1>Problema de Monty Hall</h1>
    <div class="form">
        <div v-if="!started">
            <label for="doorsAmount">Quantidade de portas</label>
            <input type="text" id="doorsAmount" size="3" v-model.number="doorsAmount">
        </div>

        <div v-if="!started">
            <label for="selectedDoor">Qual a porta premiada?</label>
            <input type="text" id="selectedDoor" size="3" v-model.number="selectedDoor">
        </div>
        <button v-if="!started" @click="started = true" :disabled="!selectedDoor || selectedDoor > doorsAmount || selectedDoor < 1">Iniciar</button>
        <button v-if="started" @click="started = false">Reiniciar</button>
    </div>

    <div class="doors" v-if="started">
        <div v-for="i in doorsAmount" :key="i">
            <DoorComponent :hasGift="i === selectedDoor" :number="i" @event="openDoorWithGift"/>
        </div>
    </div>
  </div>
</template>

<script>
    import DoorComponent from './components/DoorComponent.vue';

    export default {
        name: 'App',
        components: { DoorComponent },
        data: function () {
            return {
                started: false,
                doorsAmount: 3,
                selectedDoor: null
            }
        },
        methods: {
            openDoorWithGift(number, open) {
                console.log("openDoorWithGift")
                if(open && this.selectedDoor == number) {
                    alert('Parabéns, você ganhou o prêmio!');
                }
            }
        }
    }
</script>

<style>
    * {
        box-sizing: border-box;
        font-family: "Montserrat";
    }

    body {
        color: #FFF;
        background: linear-gradient(to right, rgb(21, 153, 87), rgb(21, 87, 153));
    }

    #app {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    #app h1 {
        border: 1px solid #000;
        background-color: #0004;
        padding: 20px;
        margin-bottom: 60px;
    }

    .form {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin-bottom: 40px;
    }

    .form, .form input, .form button {
        margin-bottom: 10px;
        font-size:2rem;
    }

    .form input { 
        margin-left: 15px;
    }

    .doors {
        align-self: stretch;
        display: flex;
        justify-content: space-around;
        flex-wrap: wrap;
    }
</style>