<template>
  <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-col>
          <v-text-field
            v-model="serial_number"
            :rules="rules"
            :counter="20"
            label="Serial number"
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
