<template>
  <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-col>
          <v-file-input
            chips
            multiple
            model="storeFiles"
            label="Store images"
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
    storeFiles: [],
    rules: [
      (value) => (value && value.length >= 3) || "At least 3 files required",
      (value) => (value && value.length <= 5) || "At most 5 files required",
    ],
  }),
};
</script>
