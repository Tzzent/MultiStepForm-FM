<template>
  <div class="container-thanks">
    <img src="/assets/images/icon-thank-you.svg" alt="Thank you" />
    <h1>Thank you!</h1>
    <p>Thanks for confirming your subscription!</p>
    <p>
      We hope you have fun using our platform. If you ever need support, please
      feel free to email us at support@loremgaming.com.
    </p>
  </div>
</template>

<script setup lang="ts"></script>

<style lang="scss">
.container-thanks {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 80px 10px;
  text-align: center;

  img {
    width: 4rem;
  }
  h1 {
    font-family: $font-ubuntu-medium;
    font-size: 1.5rem;
    margin: 18px auto;
  }
  p {
    color: $secondary-color;
    line-height: 25px;
  }
}
</style>
