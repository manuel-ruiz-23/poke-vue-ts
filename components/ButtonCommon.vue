<template>
  <component @click="$emit('click')" :is="type" :to="to" class="button">
    <slot />
  </component>
</template>

<script>
export default {
  props: {
    to: {
      type: String,
      default: null
    }
  },
  computed: {
    type() {
      if (this.to) {
        return 'nuxt-link'
      } else {
        return 'button'
      }
    }
  },
}
</script>

<style scoped>
.button {
  display: flex;
  text-decoration: none;
  padding: 0px 8px;
  justify-content: center;
  align-items: center;
  height: 32px;
  min-width: 64px;
  width: fit-content;
  background-color: #00DC81;
  border: none;
  border-radius: 8px;
  font-family: sans-serif;
  color: white;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  cursor: pointer;
}

.button:hover {
  background-color: #009350;
}
</style>