<template>
  <div>
      <v-alert
      dense
      type="success"
      style="margin-top: 20px"
      v-if="alert"
    >
      User details are <strong>added</strong> successfully.
    </v-alert>
<v-card
  class="mx-auto"
    max-width="500"
    style="padding:20px; margin-top: 20px"
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
    ></v-text-field>

    <v-text-field
      v-model="age"
      :counter="10"
      :rules="nameRules"
      label="Age"
    ></v-text-field>

    <v-text-field
      v-model="occupation"
      :counter="10"
      :rules="nameRules"
      label="Occupation"
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
    ></v-select>

    <v-text-field
      v-model="mobileno"
      :rules="mobilenoRules"
      label="Mobile Number"
      required
    ></v-text-field>

    <v-file-input
    accept="image/*"
    label="File input"
    v-model="userimage"
  ></v-file-input>

    <v-btn
      :disabled="!valid"
      color="success"
      class="mr-4"
      @click="validate"
    >
      Submit
    </v-btn>

    <v-btn
      color="error"
      class="mr-4"
      @click="reset"
    >
      Reset
    </v-btn>

  </v-form>
  </v-card>
  </div>

</template>

<script>
export default {
  data: () => ({
    alert: false,
    valid: true,
    name: '',
    age: '',
    occupation: '',
    address: '',
    mobileno: '',
    userimage: '',

    nameRules: [
      v => !!v || 'Name is required',
      v => (v && v.length <= 10) || 'Name must be less than 10 characters'
    ],
    mobilenoRules: [
      v => !!v || 'Name is required',
      v => (v && v.length <= 10) || 'Mobile Number Is Required'
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
        localStorage.setItem('age', this.age)
        localStorage.setItem('occupation', this.occupation)
        localStorage.setItem('address', this.address)
        localStorage.setItem('gender', this.select)
        localStorage.setItem('mobileno', this.mobileno)
        this.alert = true
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
