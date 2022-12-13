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
  import { computed, ref } from 'vue';

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
          amount: 100,
          time: new Date('12-01-2022'),
        },
        {
          id: 1,
          title: 'Movimiento 2',
          description: 'lorem ipsum dolor sit amet',
          amount: 200,
          time: new Date('12-13-2022'),
        },
        {
          id: 2,
          title: 'Movimiento 3',
          description: 'lorem ipsum dolor sit amet',
          amount: 500,
          time: new Date('12-12-2022'),
        },
        {
          id: 3,
          title: 'Movimiento 4',
          description: 'lorem ipsum dolor sit amet',
          amount: 200,
          time: new Date('12-12-2022'),
        },
        {
          id: 4,
          title: 'Movimiento 5',
          description: 'lorem ipsum dolor sit amet',
          amount: -400,
          time: new Date('12-12-2022'),
        },
        {
          id: 5,
          title: 'Movimiento 6',
          description: 'lorem ipsum dolor sit amet',
          amount: -600,
          time: new Date('12-12-2022'),
        },
        {
          id: 6,
          title: 'Movimiento 7',
          description: 'lorem ipsum dolor sit amet',
          amount: -300,
          time: new Date('12-12-2022'),
        },
        {
          id: 7,
          title: 'Movimiento 8',
          description: 'lorem ipsum dolor sit amet',
          amount: 0,
          time: new Date('12-12-2022'),
        },
        {
          id: 8,
          title: 'Movimiento 9',
          description: 'lorem ipsum dolor sit amet',
          amount: 300,
          time: new Date('11-12-2022'),
        },
        {
          id: 9,
          title: 'Movimiento 0',
          description: 'lorem ipsum dolor sit amet',
          amount: 500,
          time: new Date('11-12-2022'),
        },
      ]);

      const amounts = computed(() => {
        const lastDays = movements.value
          .filter((m) => {
            const today = new Date();
            const oldDate = today.setDate(today.getDate() - 30);

            // const dayDiff = (today.getTime() - m.time.getTime())/(1000 * 60 *24)

            // console.log(dayDiff <= 30);
            // return dayDiff <= 30
            return m.time > oldDate;
          })
          .map((m) => m.amount);

        return lastDays.map((m, i) => {
          const lastMovements = lastDays.slice(0, i);

          return lastMovements.reduce((suma, movement) => {
            return suma + movement;
          }, 0);
        });
      });

      return { amount, label, movements, amounts };
    },
  };
</script>

<style></style>
