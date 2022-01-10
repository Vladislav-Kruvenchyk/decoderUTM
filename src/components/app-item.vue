<template>
  <div class="app-item">
    <div class="app-item__wrapper">
      {{ app_item.name }}
    </div>
  </div>
</template>

<script>
export default {
  name: "app-item",
  props: {
    app_item: {
      type: [Array, Object, String],
      default: null,
    },
  },
};
</script>

<style lang="scss">
.app-item {
  display: flex;
  flex-direction: column;
  margin: 4px;
}
</style>
