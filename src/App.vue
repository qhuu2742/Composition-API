<template>
  <section class="container">
    <h2>{{ userName }}</h2>
    <h3>{{ userAge }}</h3>
    <button @click="newAge">Change</button>
    <!-- <br />
    <input type="text" @input="setFirstName" />
    <br />
    <input type="text" @input="setLastName" /> -->
    <br />
    <input type="text" v-model="firstName" />
    <br />
    <input type="text" ref="lastNameInput" />
    <button @click="setLastName">Set Last Name</button>
  </section>
</template>

<script>
import { computed, ref, watch } from 'vue';

export default {
  setup() {
    // const uName = ref('Maximilian');
    const uAge = ref(31);
    const lastName = ref('');
    const lastNameInput = ref(null);
    const firstName = ref('');
    // const user = reactive({
    //   name: 'Maximilian',
    //   age: 31,
    // });

    // watch sẽ thực thi khi uAge thay đổi
    // uAge ở đây là giá trị trước khi thay đổi
    watch(uAge, function (newValue, oldValue) {
      console.log('old uAge: ', oldValue);
      console.log('new uAge: ', newValue);
    });

    const uName = computed(function () {
      return firstName.value + ' ' + lastName.value;
    });

    // truyền nhiều điều kiện vào watch, tiện hơn Options API khi mà nó chỉ watch được mỗi 1 điều kiện
    watch([uAge, uName], function (newValues, oldValues) {
      console.log('old uAge: ', oldValues[0]);
      console.log('new uAge: ', newValues[0]);
      console.log('old uName: ', oldValues[1]);
      console.log('new uName: ', newValues[1]);
    });

    function setNewData() {
      uAge.value = 44;
    }

    function setLastName() {
      lastName.value = lastNameInput.value.value;
    }

    // function setFirstName(event) {
    //   firstName.value = event.target.value;
    // }

    // function setLastName(event) {
    //   lastName.value = event.target.value;
    // }

    // ở đây uAge là một ref, còn user là một reative object
    // console.log('đây là một ref sau khi đã thay đổi: ', uAge, user);

    // đây là dữ liệu trước khi có sự thay đổi
    // console.log('đây là dữ liệu chưa thay đổi: ', uAge.value);
    // console.log('đây là dữ liệu chưa thay đổi: ', user.name, user.age);

    // setTimeout(function () {
    //   // uName.value = 'Max';
    //   // uAge.value = 32;
    //   user.name = 'Max';
    //   user.age = 32;
    // }, 2000);

    return {
      userName: uName,
      userAge: uAge,
      newAge: setNewData,
      // setFirstName,
      // setLastName,
      firstName,
      lastNameInput,
      setLastName
    };
  },
  // data() {
  //   return {
  //     userName: 'Maximilian',
  //   };
  // },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>