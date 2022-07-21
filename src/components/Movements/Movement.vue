<template>
  <div class="movement">
    <div class="content">
      <h4>{{ title }}</h4>
      <p>{{ description }}</p>
    </div>
    <div class="action">
      <img src="@/assets/trash-icon.svg" alt="Borrar" @click="remove" />
      <p :class="{ green: !isNegative, red: isNegative }">
        {{ currencyAmount }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { computed, defineProps, defineEmits, toRefs } from "vue";
import currencyFormater from "@/js/currencyFormater";

const props = defineProps({
  id: {
    type: Number,
    required: true,
  },
  title: {
    type: String,
  },
  description: {
    type: String,
  },
  amount: {
    type: Number,
  },
});

const { id, title, description, amount } = toRefs(props);

const currencyAmount = computed(() => {
  return currencyFormater.format(amount.value);
});
const isNegative = computed(() => {
  return amount.value < 0;
});

const emit = defineEmits(["remove"]);

const remove = () => {
  emit("remove", id.value);
};
</script>

<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}
.movement .content {
  width: 100%;
}
.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}
h4,
p {
  margin: 0;
  padding: 0;
}
h4 {
  margin-bottom: 8px;
}
.movement .action img {
  margin-bottom: 16px;
}
.red {
  color: red;
}
.green {
  color: green;
}
</style>
