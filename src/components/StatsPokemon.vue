<template>
  <div class="tab-stats">
    <div v-for="a in item.stats" :key="a.name">
      <div class="stats">
        <p class="type">{{ a.stat.name }}</p>
        <p class="value">{{ a.base_stat }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      stats: [],
      name: ''
    }
  }
}
</script>

<style lang="scss">
.tab-stats {
  padding: 0rem 1rem;
}

.stats {
  display: flex;
  justify-content: space-between;
  p {
    margin: 0.3rem 0;
  }
  .type::first-letter {
    text-transform: uppercase;
  }
  .value {
    font-weight: 500;
  }
}
</style>
