<script setup>
const props = defineProps({
  modelValue: Array,
  options: {
    type: Array,
    default: () => ["Интересно", "Легко", "Быстро сделал", "Красиво", "Подробно описано", "Все понятно и по делу"],
  },
});

const emit = defineEmits(["update:modelValue"]);

function toggle(opt) {
  const arr = [...props.modelValue];
  const i = arr.indexOf(opt);
  if (i >= 0) arr.splice(i, 1);
  else arr.push(opt);
  emit("update:modelValue", arr);
}
</script>
<template>
  <div class="chips">
    <button
        v-for="opt in options"
        :key="opt"
        :class="{ active: modelValue.includes(opt) }"
        class="chip text-base"
        @click="toggle(opt)"
    >
      {{ opt }}
    </button>
  </div>
</template>
<style lang="scss" scoped>
@use "@/assets/styles/mixins.scss" as m;

.chips {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  @include m.phone {
    gap: 8px;
  }
}

.chip {
  border-radius: 100px;
  padding: 5px 16px;
  height: 38px;
  background-color: $neutral-300;
  color: $neutral-800;
  cursor: pointer;

  &.active {
    background: $neutral-600;
    color: $neutral-100;
  }

  @include m.phone {
    font-size: 12px;
    line-height: 133%;
    padding: 8px 12px;
    height: 32px;
  }
}

</style>
