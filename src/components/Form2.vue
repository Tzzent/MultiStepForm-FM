<template>
  <div class="form2">
    <h2>Select your plan</h2>
    <p class="description">You have the option of mountly or yearly billing</p>
    <div class="plans">
      <div
        class="plan"
        v-for="(plan, index) in plans"
        :key="index"
        v-on:click="setPlan(plan.name)"
        v-bind:class="formData.form2.plan == plan.name && 'isFocused'"
      >
        <img v-bind:src="plan.src" v-bind:alt="plan.name" />
        <div>
          <h3>{{ plan.name }}</h3>
          <span
            >${{ plan.price }}/{{
              formData.form2.option == "Yearly" ? "yr" : "mo"
            }}</span
          >
          <p v-if="formData.form2.option == 'Yearly'">2 months free</p>
        </div>
      </div>
    </div>
    <div class="option-billing">
      <p class="mountly">Mountly</p>
      <el-switch
        v-model="formData.form2.option"
        @click="changePayMode"
        style="--el-switch-on-color: #032258; --el-switch-off-color: #032258"
        active-value="Yearly"
        inactive-value="Mountly"
      />
      <p class="yearly">Yearly</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, PropType } from "vue";

const changePayMode = () => {
  props.isYearly();
};

const props = defineProps({
  formData: { type: Object, required: true },
  plans: {
    type: Array as PropType<
      {
        name: string;
        src: string;
        price: number;
      }[]
    >,
    required: true,
  },
  isYearly: { type: Function, required: true },
});

function setPlan(plan: string) {
  props.formData.form2.plan = plan;
}
</script>

<style lang="scss">
.form2 {
  h2 {
    font-family: $font-ubuntu-bold;
  }

  .description {
    color: $secondary-color;
    font-family: sans-serif;
    line-height: 25px;
    margin: 18px auto;
  }

  .plans {
    display: flex;
    flex-direction: column;
    gap: 18px;

    .plan {
      display: flex;
      gap: 15px;
      border: 1px solid $secondary-color;
      border-radius: 8px;
      padding: 20px;
      cursor: pointer;

      img {
        width: 40px;
        height: 40px;
      }
      h3 {
        font-family: $font-ubuntu-regular;
      }
      span {
        color: $secondary-color;
      }
    }

    .isFocused {
      background-color: $bg-body;
      border: 1px solid #66009d;
    }
  }

  .option-billing {
    margin-top: 20px;
    border-radius: 8px;
    background-color: $bg-body;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    padding: 18px 0px;

    .mountly {
      font-family: $font-ubuntu-medium;
    }

    .yearly {
      color: $secondary-color;
      font-family: $font-ubuntu-medium;
    }
  }
}
</style>
