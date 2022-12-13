<template>
  <div>
    <svg
      @touchstart="tap"
      @touchmove="tap"
      @touchend="untap"
      viewBox="0 0 300 200"
    >
      <line
        stroke="#c4c4c4"
        stroke-width="2"
        x1="0"
        :y1="zero"
        x2="300"
        :y2="zero"
      />
      <polyline
        fill="none"
        stroke="#0689B0"
        stroke-width="2"
        :points="points"
      />
      <line
        v-show="showPointer"
        stroke="#04b500"
        stroke-width="2"
        :x1="pointer"
        y1="0"
        :x2="pointer"
        y2="200"
      />
    </svg>
    <p>Ultimos 30 dias</p>
  </div>
</template>

<script setup>
  import { defineProps, toRefs, defineEmits, computed, ref } from 'vue';
  const props = defineProps({
    amounts: {
      type: Array,
      default: () => [],
    },
  });
  const { amounts } = toRefs(props);

  const amountToPx = (amount) => {
    const min = Math.min(...amounts.value);
    const max = Math.max(...amounts.value);

    const amountAbs = amount + Math.abs(min);
    const minmax = Math.abs(max) + Math.abs(min);

    return 200 - ((amountAbs * 100) / minmax) * 2;
  };

  const zero = computed(() => {
    return amountToPx(0);
  });

  const points = computed(() => {
    const totalEl = amounts.value.length;
    return amounts.value.reduce((points, amount, i) => {
      const x = (300 / totalEl) * (i + 1);
      const y = amountToPx(amount);
      return `${points} ${x},${y}`;
    }, '0,100');
  });

  const showPointer = ref(false);

  const pointer = ref(0);

  const emit = defineEmits(['select'])

  const tap = ({ target, touches }) => {
    showPointer.value = true;
    const elWidth = target.getBoundingClientRect().width; // Esta funcion nativa de JS nos permite calcular el width de un elemento cuando se presenta en diferentes anchos de pantalla
    const elX = target.getBoundingClientRect().x; // Obtenemos el punto inicial del lienzo en el eje x
    const touchX = touches[0].clientX; // Obtenemos el valor del touch del cliente en el eje x

    pointer.value = ((touchX - elX) * 300) / elWidth;
    // TODO Propagar el monto al component padre
    emit('select', )
  };

  const untap = ({ target, touches }) => {
    showPointer.value = false;
  };
</script>

<style scoped>
  svg {
    width: 100%;
  }

  p {
    text-align: center;
  }
</style>
