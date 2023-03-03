<template>
  <button @click="handleClick" :style="{ background: color}" class="btn">{{ text }}</button>
</template>

<script>
export default {
  name: 'Button',
  props: ['color', 'text'],
  methods: {
    handleClick() {
      this.$emit('toggle-add-task')
    }
  }
}
</script>