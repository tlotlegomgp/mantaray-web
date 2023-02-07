<template>
  <v-form v-model="valid">
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
  </v-form>
</template>

<script>
import axios from "axios";

export default {
  mounted() {
    axios
      .post(
        "https://1ydvd2q6ka.execute-api.us-east-1.amazonaws.com/v1/uploadcontent/",
        {}
      )
      .then((response) => {
        console.log("response", response);
      })
      .catch((error) => {
        console.error("error", error);
      });
  },

  data: () => ({
    valid: false,
    terminalImage: "",
    rules: [
      (value) => !!value || "Terminal image is required",
      (value) => (value && value[0]?.size > 0) || "Terminal image is required",
    ],
  }),

  methods: {
    post: () => {
      axios
        .post(
          "https://1ydvd2q6ka.execute-api.us-east-1.amazonaws.com/v1/uploadcontent/",
          {}
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
