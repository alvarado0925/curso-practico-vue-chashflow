<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume :label="label" :amount="amount" :total-amount="15000">
        <template #graphic>Graficos</template>
        <template #action>Acciones</template>
      </Resume>
    </template>
    <template #movements>
      <Movements />
    </template>
  </Layout>
</template>

<script>
import Header from "./Header.vue";
import Layout from "./Layout.vue";
import Resume from "./Resume/Index.vue";
import Movements from "./Movements.vue";

export default {
  components: {
    Header,
    Layout,
    Resume,
    Movements,
  },
  data() {
    return {
      label: null,
      amount: null,
    };
  },
};
</script>
