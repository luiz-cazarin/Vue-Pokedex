<template>
  <div class="tab-abilities">
    <div v-for="a in item.abilities" :key="a.name">
      <div class="box-ability">
        <p>{{ a.ability.name }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      abilities: [],
      ability: {
        name: ''
      },
      name: ''
    }
  }
}
</script>

<style lang="scss">
.tab-abilities {
  padding: 0rem 1rem;
  .box-ability {
    text-align: center;
    width: 100%;
    margin-top: 1rem;
    p {
      padding: 10px 0;
      border-radius: 10px;
      background: rgb(31, 31, 31);
      margin: 0;
    }
    p::first-letter {
      text-transform: uppercase;
    }
  }
}
</style>
