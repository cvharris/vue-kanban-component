<template>
  <div>
    <h2>{{ group.title }}</h2>
    <div class="lane-container">
      <slot :group="group" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    group: {
      type: Object,
      required: true
    }
  }
}
</script>

<style>
.lane-container {
  display: flex;
}
</style>
