<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="body">
    <div class="content">
      <h1>404</h1>
      <h2>Page Not Found</h2>
      <button @click="goHome">Go to Home</button>
    </div>
  </div>
</template>

<script>
import router from '@/router'
export default {
  methods: {
    goHome () {
      router.push('/')
    }
  }
}
</script>

<style lang="scss">
.body {
  display: flex;
  justify-content: center;
  align-content: center;
  .content {
    margin: auto;
    height: 300px;
    padding: 1rem;
    text-align: center;
    h1 {
      font-size: 120px;
      color: rgba(255, 255, 255, 0.9);
      margin: 0;
    }
    h2 {
      margin: 0;
      font-size: 42px;
      font-weight: 400;
      color: rgba(255, 255, 255, 0.3);
    }
    button {
      background-color: #3e95d7;
      color: black;
      margin-top: 3rem;
      cursor: pointer;
      border: none;
      padding: 1rem;
      border-radius: 5px;
      font-size: 18px;
      &:hover {
        transition: all 300ms ease;
        background-color: #ffff;
      }
    }
  }
}
</style>
