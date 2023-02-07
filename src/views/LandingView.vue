<template>
  <v-container>
    <v-row no-gutters>
      <v-col cols="12" sm="12" md="10" lg="8" class="text-center">
        <br />
        <v-img src="/kazang-logo.svg" class="mt-5 mb-5"></v-img>
        <br />
        <p
          class="text-center mb-5"
          style="font-size: 31px; font-weight: 600; color: #636b30"
        >
          Manta Ray Registration Site
        </p>
        <p class="mt-5 mb-5">
          Welcome to the Manta Ray Registration Site. From here you will be
          guided through a step-by-step process to onboard you onto the Kazang
          Platform. Please click on the "Get Started" button to begin your
          journey.
        </p>
        <br />
        <v-btn
          :to="{ name: 'home' }"
          variant="flat"
          rounded="pill"
          color="#97a93d"
          class="mt-5"
          size="x-large"
        >
          Get Started
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>
