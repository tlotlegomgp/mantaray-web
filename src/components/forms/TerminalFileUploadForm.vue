<template>
  <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-col>
          <v-file-input
            label="Upload terminal image"
            accept="image/png, image/jpeg, image/bmp"
            prepend-icon="mdi-camera"
            model="terminalImage"
            :rules="rules"
          ></v-file-input>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

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
