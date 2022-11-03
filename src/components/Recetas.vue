<script >

export default {
    data() {
        return {
            nombreid: [],
            foto: [],
            x: "",
            rgb: "",
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
                        this.foto = data["sprites"],
                        this.x = this.foto.front_default
                });
            this.visible = true;
            console.log(this.foto.length)
            this.color()
        },
        color() {
            let a = (this.infotipo[0].type.name).toString();
            if (a === 'grass') {
                this.rgb = 'green'
            }
            else if (a === 'fire') {
                this.rgb = '#e62d20'
            }
            else if (a === 'ground') {
                this.rgb = '#804f2a'
            }
            else if (a === 'water') {
                this.rgb = '#1a74db'
            }
            else if (a === 'ice') {
                this.rgb = '#8fc7c6'
            }
            else if (a === 'electric') {
                this.rgb = '#e4f261'
            }
            else if (a === 'ghost') {
                this.rgb = '#191521'
            }
            else if (a === 'poison') {
                this.rgb = '#5006c7'
            }
            else if (a === 'steel') {
                this.rgb = '#4a4a4a'
            }
            else if (a === 'rock') {
                this.rgb = '#9e843a'
            }
            else if (a === 'flying') {
                this.rgb = '#9ddbe0'
            }
            else if (a === 'dark') {
                this.rgb = '#1c1c1f'
            }
            else if (a === 'fighting') {
                this.rgb = '#9c2d17'
            }
            else if (a === 'psychic') {
                this.rgb = '#b611c2'
            }
            else if (a === 'fairy') {
                this.rgb = '#d059d9'
            }
            else if (a === 'dragon') {
                this.rgb = '#080854'
            }
            else if (a === 'bug') {
                this.rgb = '#6db536'
            }
            else if (a === 'normal') {
                this.rgb = '#a6a6a6'
            }
        }
    }
}
</script>


<template>
    <div class="app">
        <div class="dos">
            <input type="text" placeholder="introuce el nombre/id de un pokemon" id="pokemon" autocomplete="off">
            <button @click="buscarNombreId()">Search</button>
        </div>
        <div class="pokemon" v-if="visible">
            <div class="nombre" :style="{ backgroundColor: rgb }">{{ nombreid[0] }} #{{ nombreid[1] }}</div>
            <h1>Types</h1>
            <div class="tipos">
                <p v-if="visible">{{ infotipo[0].type.name }}</p>
                <p v-if="visible, infotipo.length > 1">{{ infotipo[1].type.name }}</p>
            </div>
            <div class="tipos"><img v-if="visible, x !== ''" :src="x"></div>
        </div>
    </div>
</template>


<style scoped>
img {
    width: 150px;
    height: 150px;
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