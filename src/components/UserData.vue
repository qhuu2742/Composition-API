<template>
  <h2>{{ userName }}</h2>
  <h3>{{ age }}</h3>
</template>

<script>
import { computed } from 'vue';

export default {
  props: ['lastName', 'firstName', 'age'],
  //   computed: {
  //     userName() {
  //       return this.firstName + ' ' + this.lastName;
  //     },
  //   },

  // tham số mặc định của setup, cho phép ta có quyền truy cập vào các props hiện có trong component
  setup(props) {
    const userName = computed(function () {
      return props.firstName + ' ' + props.lastName;
    });

    return {
      userName,
    };
  },
};
</script>