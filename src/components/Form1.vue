<template>
  <div class="form1">
    <h2>Personal info</h2>
    <p>Please provide your name, email address, and phone number.</p>
    <el-form
      :label-position="'top'"
      :model="formData.form1"
      :rules="rules"
      class="el-form"
    >
      <el-form-item label="Name" prop="name" class="el-form-item">
        <el-input
          v-model="formData.form1.name"
          type="text"
          autocomplete="off"
          placeholder="e.g. Stephen King"
        />
      </el-form-item>
      <el-form-item label="Email Adress" prop="email">
        <el-input
          v-model="formData.form1.email"
          type="email"
          autocomplete="off"
          placeholder="e.g. stephenking@lorem.com"
        />
      </el-form-item>
      <el-form-item label="Phone Number" prop="phone">
        <el-input
          v-model="formData.form1.phone"
          type="tel"
          maxlength="10"
          autocomplete="off"
          placeholder="e.g. +1 234 567 890"
        />
      </el-form-item>
    </el-form>
  </div>
</template>

<script setup lang="ts">
import { reactive, defineProps, ref } from "vue";

const props = defineProps({
  formData: { type: Object, required: true },
});

const validateName = ref((rule: any, value: any, callback: any) => {
  if (!props.formData.form1.name) {
    return callback(new Error("Please input name"));
  }
});

const validateEmail = ref((rule: any, value: any, callback: any) => {
  if (!props.formData.form1.email) {
    callback(new Error("Please input your email"));
  }
});

const validatePhone = ref((rule: any, value: any, callback: any) => {
  if (!props.formData.form1.phone) {
    return callback(new Error("Please input your phone number"));
  }
});

const rules = reactive({
  name: [{ validator: validateName, trigger: "blur" }],
  email: [{ validator: validateEmail, trigger: "blur" }],
  phone: [{ validator: validatePhone, trigger: "blur" }],
});
</script>

<style lang="scss">
.form1 {
  h2 {
    font-weight: 700;
    font-family: $font-ubuntu-medium;
  }
  p {
    color: $secondary-color;
    margin-top: 15px;
    line-height: 25px;
    font-family: sans-serif;
  }

  .el-form {
    margin-top: 20px;

    .el-form-item label {
      color: $primary-color;
      font-weight: 300;
    }
  }
}
</style>
