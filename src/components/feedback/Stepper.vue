<script setup>
const props = defineProps({
  step: {
    type: Number,
    required: true,
  },
  totalSteps: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <div class="feedback-steps">
      <span
          :class="{ 'step-circle--active': step >= 1 }"
          class="step-circle"
      >
        1
      </span>
    <div class="feedback-steps__bar">
      <div
          :style="{ width: (step / totalSteps) * 100 + '%' }"
          class="feedback-steps__bar-fill"
      />
    </div>
    <span
        :class="{ 'step-circle--active': step >= 2 }"
        class="step-circle"
    >
        2
      </span>
  </div>
</template>

<style lang="scss" scoped>
.feedback-steps {
  display: flex;
  align-items: center;
  gap: 16px;
}

.step-circle {
  border-radius: 17px;
  padding: 5px 13px;
  width: 34px;
  height: 34px;
  display: flex;
  align-items: center;
  justify-content: center;

  font-weight: 400;
  font-size: 16px;
  line-height: 144%;
  color: $neutral-600;

  background-color: $neutral-300;

  &--active {
    padding: 8px 14px;

    font-weight: 500;
    line-height: 112%;
    color: $neutral-100;
    background: $base-blue;
  }
}

.feedback-steps__bar {
  position: relative;
  width: 98px;
  height: 6px;
  border-radius: 40px;
  background: $neutral-300;
  overflow: hidden;
}

.feedback-steps__bar-fill {
  height: 100%;
  border-radius: inherit;
  background: $base-blue;
  transition: width 0.25s ease;
}
</style>
