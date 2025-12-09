<script setup>
import {formatPhone} from "@/untils/untils.js";

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
  type: {
    type: String,
    default: 'text',
  },
  error: {
    type: String,
    default: '',
  },
  mask: {
    type: String,
    default: '',
  }

});
const emit = defineEmits(['update:modelValue']);

function onInput(event) {
  let value = event.target.value;

  if (props.mask === 'phone') {
    value = formatPhone(value);
    event.target.value = value;
  }

  emit('update:modelValue', value);
}

</script>

<template>
  <div :class="{'field--error':error}"
       class="field ">
    <label v-if="label" class="field__label text-small">
      {{ label }}
    </label>
    <input
        :placeholder="placeholder"
        :type="type"
        :value="modelValue"
        class=" text-base field__control"
        @input="onInput"
    />
    <span
        v-if="error"
        class="field__error-text "
    >{{ error }}</span>
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
    height: 56px;
    border-radius: 8px;
    padding: 14px 16px;
    background: $neutral-200;
    color: $neutral-800;

    transition: color 0.2s ease,
    border-color 0.2s ease;

    &::placeholder {
      color: $neutral-500;
    }

    &:focus {
      border-color: $base-blue;
    }

    @include m.phone {
      padding: 10px 16px;
    }
  }

  &__error-text {
    color: $danger;
  }

  &--error .field__control {
    border-color: $semantic-danger;
    background: $semantic-danger-bg;
  }

}


</style>