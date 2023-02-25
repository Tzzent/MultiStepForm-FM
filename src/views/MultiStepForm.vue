<template>
  <div class="container-view">
    <NavBar v-bind:current-step="currentStep - 1" />
    <div class="box-form">
      <div class="multistep-form">
        <component
          v-bind:is="currentComponent"
          v-bind:formData="formData"
          v-bind:plans="plans"
          v-bind:addOns="addOns"
          v-bind:changePlan="changePlan"
          v-bind:isYearly="isYearly"
          v-bind:getTotal="getTotal"
        ></component>
      </div>
      <div class="buttons-box" v-if="currentStep < 5">
        <el-button
          v-on:click="previous"
          class="btn-back"
          v-bind:disabled="currentStep == 1"
          >Go back</el-button
        >
        <el-button v-on:click="next" class="btn-next">
          {{ currentStep == 4 ? "Confirm" : "Next step" }}
        </el-button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineComponent, ref } from "vue";
import NavBar from "../containers/NavBar.vue";
import Form1 from "../components/Form1.vue";
import Form2 from "../components/Form2.vue";
import Form3 from "../components/Form3.vue";
import Form4 from "../components/Form4.vue";
import FormEnd from "../components/FormEnd.vue";

const steps = [Form1, Form2, Form3, Form4, FormEnd];
const currentStep = ref<number>(1);
const currentComponent = ref(steps[currentStep.value - 1]);
const formData = ref({
  form1: { name: "", email: "", phone: "" },
  form2: { plan: "", option: "" },
  form3: {
    add_ons: {
      onlineService: false,
      largerStorage: false,
      customizableProfile: false,
    },
  },
});

function changePlan() {
  if (currentStep.value > 1 && currentStep.value <= 4) {
    currentStep.value = 2;
    currentComponent.value = steps[currentStep.value - 1];
  }
}
function verifyForm(form: object) {
  return Object.values(form).every((value) => value !== "");
}

function next() {
  if (currentStep.value < steps.length) {
    if (currentStep.value > 2) {
      currentStep.value++;
      currentComponent.value = steps[currentStep.value - 1];
    }
    if (currentStep.value == 2) {
      if (verifyForm(formData.value.form2)) {
        currentStep.value++;
        currentComponent.value = steps[currentStep.value - 1];
      } else {
        alert("Please select a plan!");
      }
    }
    if (currentStep.value == 1) {
      if (verifyForm(formData.value.form1)) {
        currentStep.value++;
        currentComponent.value = steps[currentStep.value - 1];
      } else {
        alert("Please complete inputs!");
      }
    }
  }
}

function previous() {
  if (currentStep.value > 1 && currentStep.value <= 4) {
    currentStep.value--;
    currentComponent.value = steps[currentStep.value - 1];
  }
}

defineComponent({
  components: { Form1, Form2, Form3, Form4, FormEnd },
  currentComponent,
  currentStep,
  steps,
  next,
  previous,
});

let plans = ref([
  { name: "Arcade", src: "../../src/assets/images/icon-arcade.svg", price: 9 },
  {
    name: "Advanced",
    src: "../../src/assets/images/icon-advanced.svg",
    price: 12,
  },
  { name: "Pro", src: "../../src/assets/images/icon-pro.svg", price: 15 },
]);

let addOns = ref([
  { name: "onlineService", desc: "SomeOnline", price: 1 },
  { name: "largerStorage", desc: "SomeLarger", price: 2 },
  { name: "customizableProfile", desc: "SomeCustom", price: 2 },
]);

const isYearly = ref(() => {
  if (formData.value.form2.option == "Yearly") {
    plans.value = plans.value.map((p) => {
      return { name: p.name, src: p.src, price: p.price * 10 };
    });
    addOns.value = addOns.value.map((ad) => {
      return { name: ad.name, desc: ad.desc, price: ad.price * 10 };
    });
  }
  if (formData.value.form2.option == "Mountly") {
    plans.value = plans.value.map((p) => {
      return { name: p.name, src: p.src, price: p.price / 10 };
    });
    addOns.value = addOns.value.map((ad) => {
      return { name: ad.name, desc: ad.desc, price: ad.price / 10 };
    });
  }
});

const getTotal = ref(() => {
  let totalBilling = 0;
  const foundPlan = plans.value.find(
    (p) => p.name == formData.value.form2.plan
  );
  if (foundPlan) {
    totalBilling += foundPlan.price;
  }
  const obj: any = formData.value.form3.add_ons;
  for (let key in obj) {
    if (obj[key] === true) {
      addOns.value.map((ad) => {
        if (ad.name == key) {
          return (totalBilling += ad.price);
        }
      });
    }
  }
  return totalBilling;
});
</script>

<style lang="scss">
@import "../sass/multistep-form/index.scss";
</style>
