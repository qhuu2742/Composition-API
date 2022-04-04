<template>
  <h2>{{ userName }}</h2>
  <h3>{{ age }}</h3>
</template>

<script>
import { computed, inject } from 'vue';

export default {
  props: ['lastName', 'firstName'],
  //   computed: {
  //     userName() {
  //       return this.firstName + ' ' + this.lastName;
  //     },
  //   },

  // tham số mặc định đầu tiên của setup - props, cho phép ta có quyền truy cập vào các props hiện có trong component
  setup(props) {
    const userName = computed(function () {
      return props.firstName + ' ' + props.lastName;
    });

    const age = inject('userAge');

    // tham số thứ hai là context
    // context.emit('save-data', 1); // this.$emit('save-data', 1);

    return {
      userName,
      age
    };
  },
};
</script>