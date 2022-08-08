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
      label="Name"
    ></v-text-field>

    <v-text-field
      v-model="age"
      label="Age"
    ></v-text-field>

    <v-text-field
      v-model="occupation"
      label="Occupation"
    ></v-text-field>

    <v-text-field
      v-model="address"
      label="Address"
    ></v-text-field>

    <v-select
      v-model="select"
      :items="items"
      label="Gender"
    ></v-select>

    <v-text-field
      v-model="mobileno"
      :rules="mobilenoRules"
      label="Mobile Number"
      required
    ></v-text-field>

    <input
    label="selecte image"
    type="file"
    @change="onFileChange"
  >
  <br>

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
    image: '',

    nameRules: [
      v => !!v || 'Name is required',
      v => (v && v.length <= 10) || 'Name must be less than 10 characters'
    ],
    mobilenoRules: [
      v => !!v || 'Mobile Number is required',
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
      // console.log(this.userimage)
      if (this.$refs.form.validate()) {
        localStorage.setItem('name', this.name)
        localStorage.setItem('age', this.age)
        localStorage.setItem('occupation', this.occupation)
        localStorage.setItem('address', this.address)
        localStorage.setItem('gender', this.select)
        localStorage.setItem('mobileno', this.mobileno)
        localStorage.setItem('userimage', this.userimage)
        this.alert = true
      }
    },
    set (key) {
      // var vm = this
      try {
        localStorage.setItem(key, this.image)
      } catch (e) {
        console.log(e)
      }
    },
    onFileChange (e) {
      var files = e.target.files || e.dataTransfer.files
      if (!files.length) {
        return
      }
      this.createImage(files[0])
    },
    createImage (file) {
      // var image = new Image()
      var render = new FileReader()
      var vm = this

      render.onload = (e) => {
        vm.image = e.target.result
        vm.set('img')
      }
      render.readAsDataURL(file)
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
