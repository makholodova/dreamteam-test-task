<script setup>

const props = defineProps({
  modelValue: {
    type: [String, Number],
    default: ''
  },
  label: {
    type: String,
    default: '',
  },
  placeholder: {
    type: String,
    default: '',
  },

  error: {
    type: String,
    default: '',
  },

});
const emit = defineEmits(['update:modelValue']);

function onInput(e) {
  emit('update:modelValue', e.target.value)
}
</script>

<template>
  <div :class="{'field--error':error}"
       class="field ">
    <label v-if="label" class="field__label text-small">
      {{ label }}
    </label>
    <textarea
        :placeholder="placeholder"
        :value="modelValue"
        class="text-base field__control  field__control--textarea"
        @input="onInput"
    />
  </div>
</template>

<style lang="scss" scoped>
@use "@/assets/styles/mixins.scss" as m;

.field {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 4px;


  &__control {

    outline: none;
    border: 1px solid $neutral-200;
    border-radius: 8px;
    padding: 14px 16px;
    background: $neutral-200;
    color: $neutral-800;
    resize: none;
    transition: color 0.2s ease,
    border-color 0.2s ease;

    &::placeholder {
      color: $neutral-500;
    }

    &:focus {
      border-color: $base-blue;
    }

    &--textarea {
      min-height: 144px;

      @include m.phone {
        min-height: 76px;
      }
    }

    @include m.phone {
      padding: 10px 16px;
    }
  }

  &__error {
    color: $danger;
  }

  &--error .field__control {
    border-color: $semantic-danger;
    background: $semantic-danger-bg;
  }
}
</style>