<template>
  <v-form v-model="valid">
    <p
      class="text-center mb-5"
      style="font-size: 30px; font-weight: 600; color: #636b30"
    >
      Merchant Terminal
    </p>
    <br />
    <p class="mb-3" style="padding: 10px">Confirm terminal information:</p>
    <v-container>
      <v-row>
        <v-col>
          <v-text-field
            v-model="serial_number"
            :rules="rules"
            :counter="20"
            label="Serial number"
            variant="outlined"
            required
          ></v-text-field>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  data: () => ({
    valid: false,
    serial_number: "",
    rules: [
      (value) => (value ? true : `Serial number is required.`),
      (value) =>
        value?.length <= 20
          ? true
          : `Serial number must be less than 20 characters.`,
    ],
  }),
};
</script>
