<script setup>
const props = defineProps({
  title: {
    type: String,
    default: ''
  },
  subtitle: {
    type: String,
    default: ''
  }
})
</script>

<template>
  <div class="feedback-header">
    <h2 class="feedback-title">{{ title }}</h2>
    <p class="feedback-subtitle text-small">{{ subtitle }}</p>
  </div>
</template>

<style lang="scss" scoped>
@use "@/assets/styles/mixins.scss" as m;

.feedback-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  @include m.phone {
    gap: 4px
  }
}

.feedback-title {
  text-align: center;
}

.feedback-subtitle {
  text-align: center;
}

</style>