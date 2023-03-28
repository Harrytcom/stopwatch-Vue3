<template>
  <button class="add-btn"  @click="onAdd">
    <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
      <rect x="8.5" width="3" height="20" fill="#9e9e9e" />
      <rect y="11.5" width="3" height="20" transform="rotate(-90 0 11.5)" fill="#9e9e9e" />
    </svg>
  </button>
</template>

<script>
export default {
  methods: {
    onAdd() {
      this.$emit('add')
    }
  },
}
</script>

<style>
.add-btn {
  background-color: var(--secondary-bg-color);
  height: 120px;
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
  border: none;
}
</style>
