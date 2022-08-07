<template>
  <div>
<v-card
  class="mx-auto"
    max-width="500"
    style="padding:20px"
>
  <v-form
    ref="form"
    v-model="valid"
    lazy-validation
  >
    <v-text-field
      v-model="name"
      :counter="10"
      :rules="nameRules"
      label="Name"
      required
    ></v-text-field>

    <v-text-field
      v-model="age"
      :counter="10"
      :rules="nameRules"
      label="Age"
      required
    ></v-text-field>

    <v-text-field
      v-model="occupation"
      :counter="10"
      :rules="nameRules"
      label="Occupation"
      required
    ></v-text-field>

    <v-text-field
      v-model="address"
      :counter="10"
      :rules="nameRules"
      label="Address"
      required
    ></v-text-field>

    <v-select
      v-model="select"
      :items="items"
      :rules="[v => !!v || 'Item is required']"
      label="Gender"
      required
    ></v-select>

    <v-text-field
      v-model="mobileno"
      :rules="nameRules"
      label="Mobile Number"
      required
    ></v-text-field>

    <v-btn
      :disabled="!valid"
      color="success"
      class="mr-4"
      @click="validate"
    >
      Validate
    </v-btn>

    <v-btn
      color="error"
      class="mr-4"
      @click="reset"
    >
      Reset Form
    </v-btn>

    <v-btn
      color="warning"
      @click="resetValidation"
    >
      Reset Validation
    </v-btn>
  </v-form>
  </v-card>
  </div>

</template>

<script>
export default {
  data: () => ({
    valid: true,
    name: '',
    age: '',
    occupation: '',
    address: '',
    mobileno: '',

    nameRules: [
      v => !!v || 'Name is required',
      v => (v && v.length <= 10) || 'Name must be less than 10 characters'
    ],
    select: null,
    items: [
      'Female',
      'Male'
    ],
    checkbox: false
  }),

  methods: {
    validate () {
      // this.$refs.form.validate()
      // console.log(this.$refs.form.validate())
      if (this.$refs.form.validate()) {
        localStorage.setItem('name', this.name)
      }
    },
    reset () {
      this.$refs.form.reset()
    },
    resetValidation () {
      this.$refs.form.resetValidation()
    }
  }
}
</script>

<style>

</style>
