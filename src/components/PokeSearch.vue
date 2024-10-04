<template>
    <div class="container">
        <form class="form">
            <h2 class="form__title">Buscador</h2>
            <div class="form__item">
                <label>Id o nombre</label>
                <input type="text" v-model="id">
                <button @click.prevent="fetchPokemon(id)">Buscar</button>
            </div>
            
            
        </form>
        <div class="card">
            <h2 class="card__title">Pokemón</h2>
            <div class="card__row">
                <div class="card__data">
                    <div><strong>Id: </strong>{{ pokeId }}</div>
                    <div><strong>Nombre: </strong>{{ pokeName }}</div>
                    <div><strong>Habilidades: </strong>{{ pokeAbilities }}</div>
                </div>
                <div class="card__img">
                    <img :src="myPokemon.image" alt="">
                </div>
            </div>
            </div>
            
    </div>
</template>

<script>
export default {
    name: 'poke-comp',
    // props: {},
    data: function(){
        return {
            id:"pikachu",
            myPokemon:{
                id:"",
                name:"",
                image:"",
                abilities:[],
            }
        }
    },
    computed: {
        pokeId(){
            return this.myPokemon.id
        },
        pokeName(){
            return this.myPokemon.name
        },
        pokeAbilities(){
            let myAbilities = []

            this.myPokemon.abilities.forEach(ability=>{
                myAbilities.push(ability.ability.name)
            })

            return myAbilities.toString()

        }
    },
    methods: {
        async fetchPokemon(id){
            try {
                const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${id}`)

                //validar response
                if(!response.ok){
                    if(response.status == 404){
                        alert("Pokemón no encontrado")
                        return
                    }else{
                        throw new Error(`HTML ERROR ${response.status}`)
                    }
                }

                //obtener json
                let pokemon = await response.json()

                this.myPokemon.id = pokemon.id
                this.myPokemon.name = pokemon.name
                this.myPokemon.image = pokemon['sprites']['other']['official-artwork']['front_default']
                this.myPokemon.abilities = pokemon.abilities

                console.log(this.myPokemon)

                this.id = ""

            } catch (error) {
               console.log("error fetch", error) 
            }
        }
    },
    // watch: {},
    // components: {},
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    created(){
        this.fetchPokemon(this.id)
    }
    // -- End Lifecycle Methods
}
</script>

<style scoped>
    .container{
        margin: 30px auto;
        width: 80%;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        column-gap: 1.25rem;
        row-gap: 30px;
    }
    .form, .card{
        align-self: flex-start;
        border: 1px solid rgb(185, 182, 182);
        border-radius: 5px;
    }
    h2{
        padding: 10px;
        background-color: rgb(236, 236, 236);
        border-bottom: 1px solid rgb(185, 182, 182);
    }
    .form__item{
        display: flex;
        column-gap: 0.625rem;
        padding: 10px;
    }
    button{
        border: none;
        border-radius: 5px;
        padding: 10px;
        background-color: rgb(11, 167, 11);
        color: white;
    }
    .card{
        width: 30%;
        min-width: 400px;
    }
    .card__row{
        display: flex;
        justify-content: space-between;
    }
    .card__data{
        padding: 1.25rem;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
    }
    .card__img{
        width: 35%;
        padding: 20px;
        
    }
    img{
        width: 100%;
        border: 1px solid rgb(204, 204, 204);
    }
</style>