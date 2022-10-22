<template>
  <div>
    <div class="header">
      <h1>Pokedex</h1>
      <input
        type="text"
        name="name"
        id="name"
        placeholder="Informe o nome do pokemon"
        v-model="pokemonName"
      />
    </div>
    <div class="box">
      <div v-if="pokemonName && !filteredList().length">
        <h1>Nenhum pokemon foi encontrado!</h1>
      </div>
      <div class="box-content">
        <div class="grid-content">
          <div v-for="item in filteredList()" :key="item.id">
            <div class="card" @click="showCard(item)">
              <div class="figure">
                <img :src="item.sprites.front_default" alt="figure" />
              </div>
              <p>{{ item.name }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-if="dialog">
      <CardPokemon :item="currItem" @closeCard="closeCard" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import CardPokemon from '../components/CardPokemon.vue'

export default {
  name: 'HomeView',
  components: { CardPokemon },
  data () {
    return {
      apiItems: [],
      items: [],
      currItem: undefined,
      pokemonName: '',
      dialog: false
    }
  },
  mounted () {
    this.getData()
  },
  methods: {
    getData () {
      axios
        .get('https://pokeapi.co/api/v2/pokemon?limit=300')
        .then((res) => {
          this.apiItems = res.data.results
          const newItems = []
          this.apiItems.forEach((element) => {
            newItems.push(element.url)
          })
          newItems.map((item) =>
            axios.get(item).then((res) => {
              this.items.push(res.data)
            })
          )
        })
        .catch((err) => {
          console.log(err)
        })
    },
    filteredList () {
      return this.items.filter((item) =>
        item.name.toLowerCase().includes(this.pokemonName.toLowerCase())
      )
    },
    showCard (item) {
      this.currItem = item
      this.dialog = true
    },
    closeCard () {
      this.dialog = false
    }
  }
}
</script>

<style lang="scss" scoped>
.card-pokemon {
  width: 1000px;
  height: 100px;
}

.header {
  text-align: center;
  margin-bottom: 2rem;
  h1 {
    font-size: 36px;
  }
  input {
    height: 32px;
    width: 1014px;
    padding: 1rem;
    border-radius: 10px;
    font-size: 18px;
    outline: none;
    @media screen and (max-width: 1100px) {
      width: 670px;
    }
    @media screen and (max-width: 720px) {
      max-width: 80%;
    }
  }
}

.box {
  display: flex;
  justify-content: center;
}
.box-content {
  min-height: 500px;
  max-width: 1200px;
  .grid-content {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    padding: 1rem;
    row-gap: 1rem;
    column-gap: 1rem;
    @media screen and (max-width: 1100px) {
      grid-template-columns: repeat(2, 1fr);
    }
    @media screen and (max-width: 720px) {
      grid-template-columns: repeat(1, 1fr);
    }
    .card {
      border: 1px solid #2c2c6c;
      transition: all 350ms ease;
      cursor: pointer;
      padding: 0.5rem;
      border-radius: 10px;
      background: #2c2c6c;
      min-width: 320px;
      min-height: 420px;
      text-align: center;
      p::first-letter {
        text-transform: uppercase;
      }
      p {
        font-size: 18px;
        font-weight: bold;
      }
      .figure {
        display: flex;
        height: 350px;
      }
      img {
        margin: auto;
        height: 170px;
        width: 170px;
      }
      &:hover {
        border: 1px solid #45b1fd;
        background: transparent;
      }
    }
  }
}
</style>
