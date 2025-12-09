<script setup>
import ErrorIcon from "../../assets/icons/error-icon.svg";
import BaseButton from "@/components/ui/BaseButton.vue";
import FeedbackHeader from "@/components/feedback/FeedbackHeader.vue";

const emit = defineEmits(['cancel', 'retry'])
</script>

<template>
  <div class="feedback-wrapper">
    <FeedbackHeader
        subtitle="Попробуйте заполнить форму позже"
        title="Что-то пошло не так"
    />
    <img :src="ErrorIcon" alt="Успешно" class="feedback-icon"/>
    <div class="feedback__actions">
      <BaseButton
          text="Закрыть"
          variant="secondary"
          @click="emit('cancel')"/>
      <BaseButton
          text="Попробовать снова"
          @click="emit('retry')"
      />
    </div>
  </div>

</template>

<style lang="scss" scoped>
@use "@/assets/styles/mixins.scss" as m;

.feedback-wrapper {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 95px;
  @include m.phone {
    gap: 44px;
  }
}

.feedback-icon {
  width: 100px;
}

.feedback__actions {
  width: 100%;
  display: flex;
  gap: 28px;

  @include m.phone {
    flex-direction: column-reverse;
    gap: 20px;
  }
}
</style>