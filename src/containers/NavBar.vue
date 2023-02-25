<template>
  <div class="nav-bar">
    <div class="steps">
      <el-steps v-bind:active="props.currentStep" finish-status="success">
        <el-step title="Step 1" description="YOUR INFO" />
        <el-step title="Step 2" description="SELECT PLAN" />
        <el-step title="Step 3" description="ADD-ONS" />
        <el-step title="Step 4" description="SUMMARY" />
      </el-steps>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

const props = defineProps({
  currentStep: { type: Number, required: true },
});
</script>

<style lang="scss">
.nav-bar {
  background-image: url("../assets/images/bg-sidebar-mobile.svg");
  background-position: center center;
  background-size: cover;
  background-repeat: no-repeat;
  min-height: 200px;
  width: 100%;

  @media screen and (min-width: 1000px) {
    background-image: url("../assets/images/bg-sidebar-desktop.svg");
    background-position: center center;
    background-size: cover;
    background-repeat: no-repeat;
    height: 100%;
    border-radius: 20px;
    max-width: 350px;
  }

  .steps {
    display: flex;
    justify-content: center;
    padding-top: 20px;
    margin-bottom: 15px;
    height: 100%;

    @media screen and (min-width: 1000px) {
      display: block;
      height: auto;
      margin-left: 30px;
    }

    .el-steps {
      @media screen and (min-width: 1000px) {
        flex-direction: column;
      }
    }

    .el-step {
      margin: 10px;
      width: 100%;
      display: flex;
      align-items: start;

      @media screen and (min-width: 1000px) {
        width: 100px;
      }

      .el-step__line {
        display: none;
      }
      .el-step__icon {
        padding: 18px;
      }
      .el-step__main {
        margin-left: 16px;
        width: 100%;

        @media screen and (max-width: 1000px) {
          display: none;
        }
      }
      .el-step__title {
        color: $secondary-color;
        white-space: nowrap;
      }
      .el-step__description {
        color: rgb(234, 234, 234);
        font-family: $font-ubuntu-bold;
        font-size: 15px;
        white-space: nowrap;
      }
    }
  }
}
</style>
