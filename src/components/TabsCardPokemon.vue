<template>
  <div class="tab">
    <button
      @click="changeTab('StatsPokemon')"
      :style="currTab === 'StatsPokemon' ? 'background-color: grey' : ''"
    >
      Status
    </button>
    <button
      @click="changeTab('AbilitiesPokemon')"
      :style="currTab === 'AbilitiesPokemon' ? 'background-color: grey' : ''"
    >
      Habilidades
    </button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      currTab: 'StatsPokemon'
    }
  },
  methods: {
    changeTab (tab) {
      this.currTab = tab
      this.$emit('changeTab', tab)
    }
  }
}
</script>

<style lang="scss">
.tab {
  display: flex;
  column-gap: 0.5rem;
  padding: 0 1rem;
  justify-content: space-between;
  button {
    cursor: pointer;
    background-color: rgb(43, 43, 43);
    color: white;
    font-weight: bold;
    border: none;
    border-radius: 3px;
    height: 32px;
    width: 50%;
  }
}
</style>
