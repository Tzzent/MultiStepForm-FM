<template>
  <div class="form3">
    <h2 class="title">Pick add-ons</h2>
    <p class="description">Add-ons help enhance your gaming experience.</p>
    <div class="options">
      <div
        class="add-on"
        v-bind:class="formData.form3.add_ons.onlineService && 'isFocused'"
        @click="
          () => {
            formData.form3.add_ons.onlineService =
              !formData.form3.add_ons.onlineService;
          }
        "
      >
        <el-checkbox
          size="large"
          v-model="formData.form3.add_ons.onlineService"
        />
        <div class="detail">
          <div>
            <h3>Online service</h3>
            <p>Access to multiplayer games</p>
          </div>
          <span>{{
            formData.form2.option == "Yearly" ? "+$10/yr" : "+$1/mo"
          }}</span>
        </div>
      </div>
      <div
        class="add-on"
        v-bind:class="formData.form3.add_ons.largerStorage && 'isFocused'"
        @click="
          () => {
            formData.form3.add_ons.largerStorage =
              !formData.form3.add_ons.largerStorage;
          }
        "
      >
        <el-checkbox
          size="large"
          v-model="formData.form3.add_ons.largerStorage"
        />
        <div class="detail">
          <div>
            <h3>Larger storage</h3>
            <p>Extra 1TB of cloud save</p>
          </div>
          <span>{{
            formData.form2.option == "Yearly" ? "+$20/yr" : "+$2/mo"
          }}</span>
        </div>
      </div>
      <div
        class="add-on"
        v-bind:class="formData.form3.add_ons.customizableProfile && 'isFocused'"
        @click="
          () => {
            formData.form3.add_ons.customizableProfile =
              !formData.form3.add_ons.customizableProfile;
          }
        "
      >
        <el-checkbox
          size="large"
          v-model="formData.form3.add_ons.customizableProfile"
        />
        <div class="detail">
          <div>
            <h3>Customizable profile</h3>
            <p>Custom theme on your profile</p>
          </div>
          <span>
            {{ formData.form2.option == "Yearly" ? "+$20/yr" : "+$2/mo" }}</span
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, ref } from "vue";

const props = defineProps({
  formData: { type: Object, required: true },
});

const optionBilling = ref(
  props.formData.form2.option == "Yearly" ? "yr" : "mo"
);
</script>

<style lang="scss">
.form3 {
  .title {
    font-family: $font-ubuntu-bold;
    color: $primary-color;
  }
  .description {
    color: $secondary-color;
    font-family: sans-serif;
    line-height: 25px;
    margin: 13px auto;
  }
}

.options {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 100%;

  .add-on {
    width: 100%;
    display: flex;
    gap: 10px;
    border: 1px solid $secondary-color;
    border-radius: 8px;
    padding: 10px;
    cursor: pointer;

    .detail {
      display: flex;
      justify-content: space-between;
      align-items: center;
      width: 100%;
      line-height: 20px;

      h3 {
        color: $primary-color;
        font-size: 1rem;
      }
      p {
        color: $secondary-color;
        font-size: 0.8rem;
      }
      span {
        font-size: 0.9rem;
        color: #66009d;
      }
    }
  }
  .isFocused {
    background-color: $bg-body;
    border-color: #66009d;
  }
}
</style>
