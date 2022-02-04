<template>
  <h2>{{ userName }}</h2>
  <h3>{{ age }}</h3>
  <h3>Stage: {{ stage }}</h3>
</template>

<script>
import {
  ref,
  computed,
  inject,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
} from 'vue';
export default {
  props: ['firstName', 'lastName'],
  setup(props) {
    const stage = ref(0);

    const userName = computed(function () {
      return `${props.firstName} ${props.lastName}`;
    });

    const age = inject('age');

    onBeforeMount(function () {
      stage.value++;
    });
    onMounted(function () {
      stage.value++;
    });
    onBeforeUpdate(function () {});
    onUpdated(function () {});
    onBeforeUnmount(function () {
      stage.value++;
    });
    onUnmounted(function () {
      stage.value++;
    });

    return { userName, age, stage };
  },
};
</script>
