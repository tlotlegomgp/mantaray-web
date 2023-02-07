<template>
  <v-form v-model="valid" v-on:submit="post">
    <p
      class="text-center mb-5"
      style="font-size: 30px; font-weight: 600; color: #636b30"
    >
      Merchant Terminal
    </p>
    <br />
    <p class="mb-5 mt-5 text-center" style="padding: 10px; font-size: 19px">
      Upload an image of your terminal. Please ensure the image is well lit and
      the terminal is clearly visible.
    </p>
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
    <v-btn type="submit" block class="mt-2">Submit</v-btn>
  </v-form>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    valid: false,
    terminalImage: "",
    rules: [
      (v) => !!v || "Terminal image is required",
      (v) => (v && v.size > 0) || "Terminal image is required",
    ],
  }),

  methods: {
    post: () => {
      axios
        .post(
          "https://1ydvd2q6ka.execute-api.us-east-1.amazonaws.com/v1/uploadcontent/",
          {},
          { crossdomain: true }
        )
        .then((response) => {
          console.log("response", response);
        })
        .catch((error) => {
          console.error("error", error);
        });
    },
  },
};
</script>
