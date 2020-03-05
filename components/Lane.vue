<template>
  <div>
    <h3>{{ lane.title }}</h3>
    <slot />
  </div>
</template>

<script>
export default {
  props: {
    lane: {
      type: Object,
      required: true
    }
  }
}
</script>

<style></style>
