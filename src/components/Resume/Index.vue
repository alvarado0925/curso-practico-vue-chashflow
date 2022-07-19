<template>
  <main>
    <p>{{ visualLabel }}</p>
    <h1>{{ visualAmount }}</h1>
  </main>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
    },
    amount: {
      type: Number,
    },
    totalAmount: {
      type: Number,
    },
  },
  computed: {
    visualLabel() {
      return this.amount !== null ? "Fecha" : "Ahorro Total";
    },
    visualAmount() {
      return this.amount !== null ? this.amount : this.totalAmount;
    },
  },
};
</script>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}

h1,
p {
  margin: 0;
  text-align: center;
}

h1 {
  margin-top: 14px;
  color: var(--brand-green);
}

.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>
