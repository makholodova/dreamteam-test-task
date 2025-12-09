<script setup>

</script>

<template>
  <div class="feedback-layout">
    <div class="feedback-card">
      <slot/>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use "@/assets/styles/mixins.scss" as m;

.feedback-layout {
  width: 100%;
  padding: 0 clamp(11px, 11px, 80px);
  margin: 20px auto;
  display: flex;
  justify-content: center;
  @include m.phone {
    margin: 20px auto;
  }
}

.feedback-card {
  width: 100%;
  max-width: 637px;
  padding: 44px;
  border-radius: 32px;
  background-color: $neutral-100;
  @include m.phone {
    padding: 20px 20px 16px 12px;
    border-radius: 16px;
  }
}
</style>