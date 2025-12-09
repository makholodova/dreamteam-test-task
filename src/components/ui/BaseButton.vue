<script setup>

const {text, variant, disabled} = defineProps({
  text: String,
  variant: {
    type: String,
    default: 'primary',
    validator: (value) => ['primary', 'secondary'].includes(value)
  },
  disabled: {
    type: Boolean,
    default: false
  },

});
</script>

<template>
  <button
      :class="['base-button','size-l', `variant-${variant}`]"
      :disabled='disabled'
  >
    <slot>{{ text }}</slot>
  </button>
</template>

<style lang="scss" scoped>
@use "@/assets/styles/mixins.scss" as m;

.base-button {
  width: 100%;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;

  transition: background 0.2s ease
}

.variant-primary {
  background: $base-blue;
  color: $neutral-100;

  &:hover {
    background: #2a1cca;
  }

  &:active {
    background: #191086;
  }

  &:disabled {
    pointer-events: none;
    cursor: default;
    background: $neutral-400;
  }
}

.variant-secondary {
  border: 1px solid $base-blue;
  color: $base-blue;
  background: transparent;
}

.size-l {
  padding: 14px 16px;
  font-size: 16px;
  line-height: 175%;
  height: 56px;

  @include m.phone {
    padding: 10px 8px;
    font-size: 14px;
    line-height: 143%;
    height: 44px;
  }
}
</style>