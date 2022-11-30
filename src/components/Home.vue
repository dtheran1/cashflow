<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume
        :total-label="label"
        :label="label"
        :amount="amount"
        :total-amount="10000000"
      >
        <template #graphic>
          graphic
        </template>

        <template #action>Action</template>
      </Resume>
    </template>
    <template #movements>
      <Movements />
    </template>
  </Layout>
</template>

<script>
  import { ref } from 'vue';

  import Layout from './Layout.vue';
  import Header from './Header.vue';
  import Resume from './Resume/Index.vue';
  import Movements from './Movements.vue';

  export default {
    name: 'Home',
    components: {
      Layout,
      Header,
      Resume,
      Movements,
    },
    setup() {
      const amount = ref(100000);
      const label = ref('Ahorro total');
      return { amount, label };
    },
  };
</script>

<style></style>
