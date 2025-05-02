<script setup>
import { reactive } from 'vue';
const genderList = ['ชาย', 'หญิง', 'ไม่ระบุ'];
const interestList = ['กีฬา', 'ดนตรี', 'การศึกษา', 'การท่องเที่ยว'];

const submitForm = () => {
  console.log(formData);
};

const formData = reactive({
  firstName: '',
  lastName: '',
  description: '',
  gender: '',
  interest: [],
});
</script>

<template>
  <div>
    <label for="firstName">firstName</label>
    <input type="text" name="firstName" v-model="formData.firstName" />
  </div>

  <div>
    <label for="lastName">lastName</label>
    <input type="text" name="lastName" v-model="formData.lastName" />
  </div>

  <div>
    <label for="description">description</label>
    <textarea
      name="description"
      id="description"
      v-model="formData.description"
    ></textarea>
  </div>

  <div>
    <label for="gender">gender</label>

    <div v-for="gender in genderList" :key="gender">
      <input
        type="radio"
        :name="gender"
        :value="gender"
        v-model="formData.gender"
      />
      <label :for="gender">{{ gender }}</label>
    </div>
  </div>

  <div>
    <label for="interest">interest</label>
    <div v-for="interest in interestList" :key="interest">
      <input type="checkbox" :value="interest" v-model="formData.interest" />
      <label :for="interest">{{ interest }}</label>
    </div>
  </div>

  <button type="submit" @click="submitForm()">ส่ง form</button>
</template>

<style></style>
