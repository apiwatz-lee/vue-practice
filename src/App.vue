<script setup>
import { ref, computed, onMounted, watch } from 'vue';

const isLoading = ref(false);
const isUpdated = ref(false);
const isValid = ref(true);
const firstname = ref('');
const lastname = ref('');
const email = ref('');
const errors = ref({});

const fullname = computed(() => {
  return `${firstname.value} ${lastname.value}`;
});

const updateProfile = async () => {
  if (!isValid.value) {
    alert('Please fix the errors before submitting');
    return;
  }
  isLoading.value = true;
  try {
    // Simulate an API call
    await new Promise((resolve) => setTimeout(resolve, 2000));
    isUpdated.value = true;
  } catch (error) {
    alert('Error updating profile');
  } finally {
    isLoading.value = false;
  }
};

const validateName = (name) => {
  const re = /\d/;
  return !re.test(name);
};

const validateEmail = (email) => {
  return email.includes('@');
};

watch([firstname, lastname, email], () => {
  isValid.value = true;
  isUpdated.value = false;
  errors.value = {};

  if (!validateName(firstname.value)) {
    isValid.value = false;
    errors.value.firstname = 'Firstname should not contain numbers';
  }

  if (!validateName(lastname.value)) {
    isValid.value = false;
    errors.value.lastname = 'Lastname should not contain numbers';
  }

  if (!validateEmail(email.value)) {
    isValid.value = false;
    errors.value.email = 'Email should contain @';
  }
});

onMounted(() => {
  firstname.value = 'John ';
  lastname.value = 'Doe';
  email.value = 'johndoe@gmail.com';
});
</script>

<template>
  <div class="container">
    <div>
      <div>Fullname: {{ fullname }}</div>
      <div>email: {{ email }}</div>
    </div>
    <div>
      <div>Firstname:</div>
      <input type="text" v-model="firstname" />
      <div class="errors">{{ errors.firstname }}</div>
    </div>

    <div>
      <div>Lastname:</div>
      <input type="text" v-model="lastname" />
      <div class="errors">{{ errors.lastname }}</div>
    </div>

    <div>
      <div>Email:</div>
      <input type="text" v-model="email" />
      <div class="errors">{{ errors.email }}</div>
    </div>

    <div v-if="isLoading">Loading ...</div>

    <button :disabled="!isValid" @click="updateProfile()">
      Update profile
    </button>
    <div v-if="isUpdated">updated successfully</div>
  </div>
</template>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  max-width: 320px;
  margin: 0 auto;
}

.container > div {
  width: 100%;
}

input {
  width: 100%;
}

button {
  width: 100%;
  height: 24px;
  margin-top: 10px;
}

.errors {
  color: red;
  font-size: 12px;
}
</style>
