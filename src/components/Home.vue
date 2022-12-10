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
          <Graphic :amounts="amounts" />
        </template>

        <template #action>
          <Action />
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" />
    </template>
  </Layout>
</template>

<script>
  import { ref } from 'vue';

  import Layout from './Layout.vue';
  import Header from './Header.vue';
  import Resume from './Resume/Index.vue';
  import Movements from './Movements/Index.vue';
  import Action from './Action.vue';
  import Graphic from '../components/Resume/Graphic.vue';

  export default {
    name: 'Home',
    components: {
      Layout,
      Header,
      Resume,
      Movements,
      Action,
      Graphic,
    },
    setup() {
      const amount = ref(100000);
      const label = ref('Ahorro total');
      const movements = ref([
        {
          id: 0,
          title: 'Movimiento 1',
          description: 'lorem ipsum dolor sit amet',
          amount: 1000,
        },
        {
          id: 1,
          title: 'Movimiento 2',
          description: 'lorem ipsum dolor sit amet',
          amount: -1000,
        },
        {
          id: 2,
          title: 'Movimiento 3',
          description: 'lorem ipsum dolor sit amet',
          amount: 1000,
        },
        {
          id: 3,
          title: 'Movimiento 4',
          description: 'lorem ipsum dolor sit amet',
          amount: 1000,
        },
        {
          id: 4,
          title: 'Movimiento 5',
          description: 'lorem ipsum dolor sit amet',
          amount: -1000,
        },
        {
          id: 5,
          title: 'Movimiento 6',
          description: 'lorem ipsum dolor sit amet',
          amount: 1000,
        },
      ]);
      const amounts = [100, 200, 500, 200, -400, -600, -300, 0, 300, 500];

      return { amount, label, movements, amounts };
    },
  };
</script>

<style></style>
