<template>
  <div class="custom-select" @blur="open = false">
    <div class="selected" :class="{ open: open }" @click="toggleDropdown">
      {{ selected }}
    </div>
    <div class="items" :class="{ selectHide: !open }">
      <div
        v-for="(option, i) of options"
        :key="i"
        @click="selectOption(option, i.toString())"
      >
        {{ option }}
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from "vue";

const props = defineProps<{
  options: string[];
  default: string;
  reset: boolean;
}>();

watch(props, (newValue) => {
  if (newValue.reset === true) {
    reset();
  }
});

const emit = defineEmits<{
  (e: "input", id: string): void;
}>();

const selected = ref<string | null>(
  props.default
    ? props.default
    : props.options.length > 0
    ? props.options[0]
    : null
);
const open = ref<boolean>(false);

const toggleDropdown = (): void => {
  open.value = !open.value;
};

const selectOption = (option: string, id: string): void => {
  selected.value = option;
  open.value = false;
  emit("input", id);
};

// Функция сброса в дочернем компоненте
const reset = (): void => {
  selected.value = props.default
    ? props.default
    : props.options.length > 0
    ? props.options[0]
    : null;
};
</script>

<style lang="scss">
.custom-select {
  position: relative;
  width: 100%;
  text-align: left;
  outline: none;
  font-size: 14px;
  height: 48px;
  line-height: 20px;
  z-index: 100;
}

.custom-select .selected {
  background-color: #232532;
  border-radius: 12px;
  color: #fff;
  padding: 14px 24px;
  cursor: pointer;
  user-select: none;
  transition: border-radius 0.3s;
}

.custom-select .selected.open {
  border-radius: 12px 12px 0px 0px;
}

.custom-select .selected:after {
  position: absolute;
  content: "";
  top: 50%;
  transform: translateY(-50%);
  right: 16px;
  background-image: url("/images/dropdown-arrow.svg");
  background-repeat: no-repeat;
  background-size: contain;
  width: 16px;
  height: 16px;
  transition: transform 0.3s;
}

.custom-select .items {
  color: #fff;
  border-radius: 0px 0px 12px 12px;
  overflow: hidden;
  position: absolute;
  background-color: #232532;
  left: 0;
  right: 0;
  z-index: 1;
  transition: opacity 0.3s;
  opacity: 1;
  pointer-events: unset;
  max-height: 250px;
  overflow-y: scroll;

  &::-webkit-scrollbar {
    width: 5px;
  }

  &::-webkit-scrollbar-track {
    background: #4b515a;
  }

  &::-webkit-scrollbar-thumb {
    background: #e6533c;
  }

  &::-webkit-scrollbar-thumb:hover {
    background: #e6533c;
  }
}

.custom-select .items div {
  color: #fff;
  padding: 14px 24px;
  cursor: pointer;
  user-select: none;
  transition: background-color 0.3s;
}

.custom-select .items div:hover {
  background-color: #e6533c;
}

.custom-select .selectHide {
  opacity: 0;
  pointer-events: none;
}

.custom-select .open::after {
  transform: translateY(-50%) rotate(180deg);
}

@media (max-width: 550px) {
  .custom-select {
    font-size: 12px;
    line-height: 16px;
  }
}
</style>
