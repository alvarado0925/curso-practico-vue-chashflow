<template>
  <div>
    <svg :viewBox="viewBox">
      <line
        stroke="#c4c4c4"
        stroke-with="2"
        x1="0"
        :y1="zero"
        x2="300"
        :y2="zero"
      />
      <polyline fill="none" stroke="#0689B0" stroke-with="2" :points="points" />
      <line
        stroke="#04b500"
        stroke-with="2"
        x1="200"
        y1="0"
        x2="200"
        y2="200"
      />
    </svg>
    <p>Últimos 30 días</p>
  </div>
</template>

<script setup>
import { defineProps, toRefs, computed } from "vue";

const props = defineProps({
  amounts: {
    type: Array,
    default: () => [],
  },
});

const { amounts } = toRefs(props);

const boxHeight = 200;
const boxWidth = 300;
const viewBox = `0 0 ${boxWidth} ${boxHeight}`;

const min = Math.min(...amounts.value);
const max = Math.max(...amounts.value);

const amountToPx = (amount) => {
  const amountAbsolute = amount + Math.abs(min);
  const minmax = Math.abs(min) + Math.abs(max);
  return boxHeight - ((amountAbsolute * 100) / minmax) * 2;
};

const zero = computed(() => {
  return amountToPx(0);
});

const points = computed(() => {
  const total = amounts.value.length;
  return amounts.value.reduce((points, amount, index) => {
    const x = (boxWidth / total) * (index + 1);
    const y = amountToPx(amount);
    return `${points} ${x},${y}`;
  }, "0,100");
});
</script>

<style scoped>
svg {
  width: 100%;
}

p {
  text-align: center;
}
</style>
