<script >

export default {
    data() {
        return {
            nombreid: [],
            foto: [],
            infotipo: [],
            pokemon: "",
            visible: false
        }
    },
    methods: {
        async buscarNombreId(async) {
            this.nombreid = []
            let input = document.getElementById('pokemon').value;
            this.pokemon = input;
            const url = "https://pokeapi.co/api/v2/pokemon/" + this.pokemon;
            await fetch(url)
                .then((response) => response.json())
                .then((data) => {
                    this.nombreid.push(data.name, data.id),
                        this.infotipo = data["types"],
                        this.foto = data["sprites"]
                });
            this.visible = true;
        },
    }
}
</script>


<template>
    <div class="app">
        <div class="dos">
            <input type="text" placeholder="introuce el nombre/id de un pokemon" id="pokemon">
            <button @click="buscarNombreId()">Search</button>
        </div>
        <div class="pokemon" v-if="visible">
            <div class="nombre">{{ nombreid[0] }} #{{ nombreid[1] }}</div>
            <h1>Types</h1>
            <div class="tipos">
                <p v-if="visible">{{ infotipo[0].type.name }}</p>
                <p v-if="visible, infotipo.length > 1">{{ infotipo[1].type.name }}</p>
            </div>
            <div class="tipos"><img src={{foto[0]}} alt=""></div>
            <p>{{ foto["front-default"] }}</p>
        </div>1
    </div>
</template>


<style scoped>
img {
    width: 100px;
    height: 100px;
}

.tipos {
    display: flex;
    justify-content: center;
}

p {
    margin: 10px;
    text-transform: capitalize;
}

h1 {
    text-align: center;
}

p {
    color: var(--color);
}

.pokemon {
    width: 300px;
    height: 400px;
    background-color: var(--background2);
    border-radius: 5px;
    color: var(--color);
    margin-top: 40px;
}

button {
    width: 60px;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    height: 30px;
    outline: none;
    background-color: var(--enfasis);
    text-align: center;
}

.nombre {
    width: 100%;
    height: 20%;
    font-size: 2rem;
    display: flex;
    justify-content: center;
    border-radius: 5px;
    align-items: center;
    text-align: center;
    flex-direction: row;
    color: var(--color);
    text-transform: capitalize;
    background-color: var(--enfasis);
}

.dos {
    display: flex;
    flex-direction: row;
    align-items: center;
}

input {
    border: 1px var(--enfasis);
    border-radius: 5px;
    background-color: var(--background2);
    outline: var(--enfasis);
    color: var(--color);
    height: 30px;
    width: 400px;
    font-size: larger;
    text-indent: 30px;
}

.app {
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    margin: 100px;
}

li {
    list-style: none;
}
</style>