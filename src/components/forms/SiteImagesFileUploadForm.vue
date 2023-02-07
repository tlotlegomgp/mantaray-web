<template>
  <v-form v-model="valid">
    <p
      class="text-center mb-5"
      style="font-size: 30px; font-weight: 600; color: #636b30"
    >
      Site Inspection
    </p>
    <br />
    <p class="mb-5 mt-5 text-center" style="padding: 10px; font-size: 19px">
      Upload images of the site. Please ensure the images of the site are well
      lit and the site is clearly visible.
    </p>
    <v-container>
      <v-row>
        <v-col>
          <v-file-input
            chips
            multiple
            model="storeFiles"
            label="Store images"
            accept="image/png, image/jpeg, image/bmp"
            prepend-icon="mdi-camera"
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
    storeFiles: [],
    rules: [
      (value) => (value && value.length >= 3) || "At least 3 files required",
      (value) => (value && value.length <= 5) || "At most 5 files required",
    ],
  }),
};
</script>
