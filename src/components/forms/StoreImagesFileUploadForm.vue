<template>
  <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-col cols="12" md="6">
          <v-file-input
            label="Upload store image"
            accept="image/*"
            model="storeFile"
            :rules="rules"
          ></v-file-input>
        </v-col>
        <v-col cols="12" md="6">
          <v-file-input
            label="Upload store image"
            accept="image/*"
            model="storeFile"
            :rules="rules"
          ></v-file-input>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="6">
          <v-file-input
            label="Upload store image"
            accept="image/*"
            model="storeFile"
            :rules="rules"
          ></v-file-input>
        </v-col>
        <v-col cols="12" md="6">
          <v-file-input
            label="Upload store image"
            accept="image/*"
            model="storeFile"
            :rules="rules"
          ></v-file-input>
        </v-col>
      </v-row>
      <SubmitButton />
    </v-container>
  </v-form>
</template>

<script setup>
import SubmitButton from "@/components/SubmitButton.vue";
</script>

<script>
export default {
  data: () => ({
    valid: false,
    storeFile: "",
    rules: [
      (v) => !!v || "Store image is required",
      (v) => (v && v.size > 0) || "Store image is required",
    ],
  }),
};
</script>
