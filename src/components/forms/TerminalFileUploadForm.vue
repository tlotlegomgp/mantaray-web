<template>
  <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-col>
          <v-file-input
            label="Upload terminal image"
            accept="image/*"
            model="terminalImage"
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
    terminalImage: "",
    rules: [
      (v) => !!v || "Terminal image is required",
      (v) => (v && v.size > 0) || "Terminal image is required",
    ],
  }),
};
</script>
