<template>
  <div class="form4">
    <h2 class="title">Finishing up</h2>
    <p class="description">
      Double-check everything looks OK before confirming.
    </p>
    <div class="container-end">
      <div class="checks">
        <div class="head">
          <div>
            <p>{{ findPlan().name }} ({{ formData.form2.option }})</p>
            <button @click="changePlan()">Change</button>
          </div>
          <span>${{ findPlan().price }}/{{ optionBilling }}</span>
        </div>
        <hr />
        <div v-for="(value, key) in formData.form3.add_ons" v-bind:key="key">
          <div v-if="value" class="check">
            <p>{{ formatKey(key) }}</p>
            <span
              >${{ getPriceByKey(key.toString()) }}/{{ optionBilling }}</span
            >
          </div>
        </div>
      </div>
      <div class="total">
        <p>
          Total (per {{ formData.form2.option == "Yearly" ? "year" : "month" }})
        </p>
        <span>+${{ getTotal() }}/{{ optionBilling }}</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, ref } from "vue";

const props = defineProps({
  formData: { type: Object, required: true },
  getTotal: { type: Function, required: true },
  changePlan: { type: Function, required: true },
  plans: { type: Array, required: true },
});

const optionBilling = ref(
  props.formData.form2.option == "Yearly" ? "yr" : "mo"
);

const findPlan = ref((): any => {
  return props.plans.find((p: any) => {
    return p.name == props.formData.form2.plan;
  });
});

function getPriceByKey(key: string) {
  const opBilling = props.formData.form2.option;
  switch (key) {
    case "onlineService":
      return opBilling == "Yearly" ? 10 : 1;
    case "largerStorage":
      return opBilling == "Yearly" ? 20 : 2;
    case "customizableProfile":
      return opBilling == "Yearly" ? 20 : 2;
  }
}

function formatKey(key: any) {
  return (
    key
      .replace(/([A-Z])/g, " $1")
      .charAt(0)
      .toUpperCase() + key.replace(/([A-Z])/g, " $1").slice(1)
  );
}
</script>

<style lang="scss">
.form4 {
  .title {
    font-family: $font-ubuntu-medium;
    color: $primary-color;
  }
  .description {
    color: $secondary-color;
    font-family: sans-serif;
    line-height: 25px;
    margin: 13px auto;
  }
  .container-end {
    .checks {
      background-color: $bg-body;
      padding: 15px;
      border-radius: 12px;
      color: $primary-color;
      hr {
        height: 1px;
        background-color: $secondary-color;
        border: none;
      }

      .head {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 12px;
        p {
          font-weight: 600;
        }
        span {
          font-weight: 600;
        }

        button {
          background-color: transparent;
          border: none;
          text-decoration: underline;
          cursor: pointer;
          color: $secondary-color;
        }
      }
      .check {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-top: 12px;
        p {
          color: $secondary-color;
          font-size: 0.8rem;
        }
        span {
          font-family: $font-ubuntu-medium;
          font-size: 0.9rem;
        }
      }
    }
    .total {
      padding: 15px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      p {
        color: $secondary-color;
      }
      span {
        color: #66009d;
        font-family: $font-ubuntu-medium;
      }
    }
  }
}
</style>
