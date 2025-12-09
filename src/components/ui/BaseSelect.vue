<script setup>
import {computed, onBeforeUnmount, onMounted, ref} from "vue";

const props = defineProps({
  modelValue: {
    type: [String, Number, null],
    default: "",
  },
  label: {
    type: String,
    default: "",
  },
  options: {
    type: Array,
    default: () => [],
  },
  placeholder: {
    type: String,
    default: "Выберите",
  },
  error: {
    type: String,
    default: "",
  },
});

const emit = defineEmits(["update:modelValue", "change"]);

const isOpen = ref(false);

const normalizedOptions = computed(() =>
    props.options.map((opt) =>
        typeof opt === "string" ? {label: opt, value: opt} : opt
    )
);

const selectedOption = computed(() =>
    normalizedOptions.value.find((o) => o.value === props.modelValue)
);

function toggle() {
  isOpen.value = !isOpen.value;
}

function select(value) {
  emit("update:modelValue", value);
  emit("change", value);
  isOpen.value = false;
}

function onDocumentClick(e) {
  const root = e.target.closest(".field__select-wrapper");
  if (!root) {
    isOpen.value = false;
  }
}

onMounted(() => document.addEventListener("click", onDocumentClick));
onBeforeUnmount(() => document.removeEventListener("click", onDocumentClick));
</script>

<template>
  <div :class="['field', { 'field--error': error }]">
    <label v-if="label" class="field__label text-small">
      {{ label }}
    </label>

    <div class="field__select-wrapper">
      <button
          class="field__control text-base"
          type="button"
          @click="toggle"
      >
        <span class="field__value">
          {{ selectedOption?.label || placeholder }}
        </span>

        <span
            :class="{ 'field__arrow--open': isOpen }"
            class="field__arrow"
        >
          <svg fill="none" height="8" viewBox="0 0 14 8" width="14" xmlns="http://www.w3.org/2000/svg">
  <path d="M0.75 0.75L6.75 6.75L12.75 0.75" stroke="#170F49" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"/>
</svg>
        </span>
      </button>

      <div v-if="isOpen" class="field__dropdown">
        <button
            v-for="opt in normalizedOptions"
            :key="opt.value"
            class="field__option text-base"
            type="button"
            @click="select(opt.value)"
        >
          {{ opt.label }}
        </button>
      </div>
    </div>

    <p v-if="error" class="field__error text-small">
      {{ error }}
    </p>
  </div>
</template>

<style lang="scss" scoped>
@use "@/assets/styles/mixins.scss" as m;

.field {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 4px;

  &__select-wrapper {
    position: relative;
    width: 100%;
  }

  &__control {
    width: 100%;
    height: 56px;

    border-radius: 8px;
    padding: 14px 16px;
    background: $neutral-200;
    color: $neutral-800;
    display: flex;
    align-items: center;
    justify-content: space-between;
    cursor: pointer;

    transition: border-color 0.2s ease,
    box-shadow 0.2s ease,
    background 0.2s ease;

    &:hover {
      border: 1px solid $neutral-400;
      border-color: $base-blue;
    }

    &:focus-visible {
      outline: none;
      border-color: $base-blue;
      box-shadow: 0 0 0 2px rgba($base-blue, 0.15);
    }

    @include m.phone {
      height: 48px;
      padding: 10px 40px 10px 16px;
    }
  }

  &__arrow {
    display: inline-flex;
    color: $neutral-400;
    transition: transform 0.2s ease;

    &--open {
      transform: translateY(-1px) rotate(180deg);
    }
  }

  &__dropdown {
    position: absolute;
    border-radius: 8px;
    width: 100%;
    max-height: 270px;
    top: calc(100% + 4px);
    left: 0;
    overflow-y: auto;
    box-shadow: 0 2px 4px -2px rgba(10, 10, 10, 0.06), 2px 4px 8px -2px rgba(10, 10, 10, 0.08);
    background: $neutral-100;
    z-index: 20;
  }

  &__option {
    width: 100%;
    padding: 13px 16px;
    height: 54px;
    text-align: left;
    cursor: pointer;
    background: $neutral-100;
    line-height: 175%;
    color: $neutral-800;

    &:hover {
      background: $neutral-200;
    }
  }

  &__error {
    color: $semantic-danger;
  }

  &--error {
    .field__control {
      border-color: $semantic-danger;
      background: $semantic-danger-bg;
    }
  }
}
</style>
