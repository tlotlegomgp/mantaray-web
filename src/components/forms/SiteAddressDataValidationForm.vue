<template>
  <v-form v-model="valid">
    <p
      class="text-center mb-5"
      style="font-size: 30px; font-weight: 600; color: #636b30"
    >
      Site Address
    </p>
    <br />
    <p class="mb-3" style="padding: 10px">Confirm site address information:</p>
    <v-container>
      <v-row>
        <v-col>
          <v-text-field
            v-model="address"
            :rules="rules"
            :counter="100"
            label="Site address"
            variant="outlined"
            required
            readOnly
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
    address:
      "F3, Block D, Sable Square Corner of Bosmansdam Rd and, Ratanga Rd, Milnerton, 7441",
    rules: [
      (value) => (value ? true : `Site address is required.`),
      (value) =>
        value?.length <= 100
          ? true
          : `Site address must be less than 100 characters.`,
    ],
  }),
};
</script>
