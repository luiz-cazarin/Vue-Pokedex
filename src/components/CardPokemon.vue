<!-- eslint-disable vue/valid-template-root -->
<template>
  <div class="body">
    <div class="card-pokemon">
      <div class="box-figure">
        <div class="card-header">
          <button @click="closeCard">X</button>
        </div>
        <div
          class="card-figure"
          :style="`background: ${dynamicStyle(currItem.types[0].type.name)};`"
        >
          <img :src="currItem.sprites.front_default" alt="figure" />
        </div>
      </div>
      <h3>{{ currItem.name }}</h3>
      <div class="card-skills">
        <div class="pokemon-types" v-for="t in currItem.types" :key="t.slot">
          <div
            class="box-type"
            :style="`background: ${dynamicStyle(t.type.name)}`"
          >
            <p>{{ t.type.name }}</p>
          </div>
        </div>
      </div>
      <TabsCardPokemon @changeTab="changeTab" />
      <KeepAlive>
        <component :is="currTab" v-bind="{ item: currItem }" />
      </KeepAlive>
    </div>
  </div>
</template>

<script>
import StatsPokemon from './StatsPokemon.vue'
import AbilitiesPokemon from './AbilitiesPokemon.vue'
import TabsCardPokemon from './TabsCardPokemon.vue'
export default {
  props: {
    item: undefined
  },
  components: { StatsPokemon, AbilitiesPokemon, TabsCardPokemon },
  data () {
    return {
      currTab: 'StatsPokemon',
      currItem: {
        sprites: [],
        name: undefined,
        types: [
          {
            slot: 0,
            type: {}
          }
        ]
      }
    }
  },
  computed: {},
  mounted () {
    this.currItem = this.item
  },
  methods: {
    dynamicStyle (type) {
      if (type === 'fire') return '#ce4354;'
      if (type === 'ice') return '#32414c'
      if (type === 'bug') return '#8eb433'
      if (type === 'fighting') return '#cc4357'
      if (type === 'fantasma') return '#5366a7'
      if (type === 'fairy') return '#cd90bf'
      if (type === 'electric') return '#e8d255'
      if (type === 'dragon') return '#116bb3'
      if (type === 'water') return '#5ca2d2'
      if (type === 'stell') return '#569ba1'
      if (type === 'flying') return '#91a8d6'
      if (type === 'poison') return '#9a61a5'
      if (type === 'ground') return '#d2794c'
      if (type === 'dark') return '#5c5b66'
      if (type === 'psychic') return '#e97876'
      if (type === 'grass') return '#5cb359'
      if (type === 'rock') return '#ccc08b'
      if (type === 'normal') return '#9b9ea0'
      else return 'box-type'
    },
    changeTab (payload) {
      this.currTab = payload
    },
    closeCard () {
      this.$emit('closeCard')
    }
  }
}
</script>

<style lang="scss">
.body {
  background: rgba(0, 0, 0, 0.5);
  transition: all 1s ease;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
  display: flex;

  .card-pokemon {
    box-shadow: -1px 1px 25px rgba(0, 0, 0, 0.3);
    background-color: rgb(26, 26, 26);
    color: white;
    border-radius: 10px;
    width: 380px;
    height: 680px;
    margin: auto;
    h3 {
      font-size: 22px;
      text-align: center;
      margin: 1rem 0rem 0.1rem 0rem;
    }
    h3::first-letter {
      text-transform: uppercase;
    }
    .box-figure {
      text-align: center;
      display: flex;
      justify-content: right;
      .card-header {
        position: fixed;
        color: black;
        button {
          cursor: pointer;
          margin: 0.5rem;
          height: 22px;
          width: 22px;
          border-radius: 200px;
          outline: none;
          border: none;
          background: transparent;
          &:hover {
            transition: all 200ms ease;
            background: black;
            color: white;
          }
        }
      }
      .card-figure {
        width: 100%;
        height: 300px;
        border-radius: 10px 10px 40px 40px;
        margin: auto;
        img {
          margin-top: 2rem;
          width: 230px;
          height: 230px;
        }
      }
    }
    .card-skills {
      display: flex;
      column-gap: 1rem;
      padding: 1rem;
      .pokemon-types {
        border-radius: 10px;
        text-align: center;
        width: 50%;
        font-weight: bold;
        p {
          margin: 0.5rem;
        }
        p::first-letter {
          text-transform: uppercase;
        }
        .box-type {
          padding: 0.1rem;
          border-radius: 10px;
        }
      }
    }
  }
}
</style>
