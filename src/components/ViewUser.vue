<template>
  <div>
    <v-alert
      dense
      type="success"
      style="margin-top: 20px"
      v-if="alert"
    >
      User details are <strong>deleted</strong>.
    </v-alert>

  <v-card
    class="mx-auto"
    max-width="500"
    style="margin-top: 20px"
    outlined
  >
    <v-list-item three-line>
      <v-list-item-content>
        <div class="text-overline mb-4">
          User Details
        </div>
        <v-list-item-title class="text-h5 mb-1">

        </v-list-item-title>
        <v-list-item-subtitle>
        </v-list-item-subtitle>
        <ul>
            <li>
              Name: {{name}}
            </li>
            <li>
              Age: {{ age }}
            </li>
            <li>
              Occupation: {{ occupation }}
            </li>
            <li>
              Address: {{ address }}
            </li>
            <li>
              Gender: {{ select }}
            </li>
            <li>
              Mobile Number: {{ mobileno }}
            </li>
          </ul>
      </v-list-item-content>

      <v-list-item-avatar
        tile
        size="80"
        color="grey"

      >
      <img :src='userimage' alt="">
      </v-list-item-avatar>
    </v-list-item>

    <v-card-actions>
      <v-dialog
      v-model="dialog"
      persistent
      max-width="600px"
    >
      <template v-slot:activator="{ on, attrs }">
      <v-btn
        outlined
        rounded
        text
        v-bind="attrs"
        v-on="on"
      >
        Edit
      </v-btn>
      </template>
      <v-card style="padding:20px;">
        <v-alert
      dense
      type="success"
      style="margin-top: 20px"
      v-if="alertedit"
    >
      User details are <strong>edited</strong> successfully.
    </v-alert>
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

    <v-btn
      :disabled="!valid"
      color="success"
      class="mr-4"
      @click="editDetails"
    >
      Save
    </v-btn>

    <v-btn
      color="error"
      class="mr-4"
      @click="dialog = false"
    >
      Cancle
    </v-btn>
  </v-form>
      </v-card>
    </v-dialog>

      <v-btn
        outlined
        rounded
        text
        @click="deleteDetails"
      >
        Delete
      </v-btn>

    </v-card-actions>
  </v-card>

  <v-row justify="center">
  </v-row>
  </div>
</template>

<script>
export default {
  data () {
    return {
      valid: true,
      name: '',
      age: '',
      occupation: '',
      address: '',
      mobileno: '',
      select: '',
      alert: false,
      alertedit: false,
      dialog: false,
      userimage: '',
      mobilenoRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 10) || 'Mobile Number Is Required'
      ],
      items: [
        'Female',
        'Male'
      ],
      nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 10) || 'Name must be less than 10 characters'
      ]
    }
  },
  created () {
    this.getDetails()
  },
  methods: {
    getDetails () {
      this.name = localStorage.getItem('name')
      this.age = localStorage.getItem('age')
      this.occupation = localStorage.getItem('occupation')
      this.address = localStorage.getItem('address')
      this.mobileno = localStorage.getItem('mobileno')
      this.select = localStorage.getItem('gender')
      this.userimage = localStorage.getItem('img')
    },
    editDetails () {
      localStorage.setItem('name', this.name)
      localStorage.setItem('age', this.age)
      localStorage.setItem('occupation', this.occupation)
      localStorage.setItem('address', this.address)
      localStorage.setItem('gender', this.select)
      localStorage.setItem('mobileno', this.mobileno)
      this.alertedit = true
    },
    deleteDetails () {
      localStorage.clear()
      this.alert = true
    }
  }
}
</script>
