<template>
  <section class="container">
    <user-data :first-name="firstName" :last-name="lastName"></user-data>
    <button @click="setAge">Change Age</button>
    <div>
      <input type="text" placeholder="First Name" v-model="firstName" />
      <input type="text" placeholder="last Name" ref="lastNameInput" />
      <button @click="setLastName">Set Last Name</button>
    </div>
  </section>
</template>

<script>
import { ref, reactive, computed, watch, provide } from 'vue';
import UserData from './components/UserData.vue';

export default {
  components: {
    UserData,
  },
  setup() {
    const user = reactive({
      name: 'Sam',
      age: 32,
    });

    const firstName = ref('');
    const lastName = ref('');
    const lastNameInput = ref(null);
    const fullName = computed(function () {
      return `${firstName.value} ${lastName.value}`;
    });

    watch(
      () => user.age,
      function (newVal, oldVal) {
        console.log(`Old Age: ${oldVal}. New Age: ${newVal}`);
      }
    );

    watch([firstName, lastName], (newVal, oldVal) => {
      console.log(`Old: ${oldVal}. New:${newVal}`);
    });

    function setFirstName(event) {
      firstName.value = event.target.value;
    }
    function setLastName() {
      lastName.value = lastNameInput.value.value;
    }

    function setNewAge() {
      user.age += 1;
    }

    provide('age', user.age);

    return {
      user,
      setAge: setNewAge,
      setFirstName,
      setLastName,
      fullName,
      firstName,
      lastName,
      lastNameInput,
    };
  },
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
