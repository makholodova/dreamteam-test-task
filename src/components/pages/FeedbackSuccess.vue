<script setup>
import SuccessIcon from "../../assets/icons/success-icon.svg";
import BaseButton from "@/components/ui/BaseButton.vue";
import FeedbackHeader from "@/components/feedback/FeedbackHeader.vue";

const emit = defineEmits(['cancel'])
</script>

<template>
  <div class="feedback-wrapper">
    <FeedbackHeader
        subtitle="Свяжемся с вами в ближайшее время"
        title="Спасибо, ваш ответ отправлен"
    />
    <img :src="SuccessIcon" alt="Успешно" class="feedback-icon"/>
    <BaseButton
        text="На главную"
        @click="emit('cancel')"
    />
  </div>
</template>

<style lang="scss" scoped>
@use "@/assets/styles/mixins.scss" as m;

.feedback-wrapper {
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

</style>