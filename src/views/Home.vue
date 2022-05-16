<template>
  <v-container fill-height justify-center>
    <v-card style="text-align: center;" max-width="600">
      <v-card-title class="justify-center">Clash Royale Gems Generator</v-card-title>
      <v-card-subtitle>
        Free and legit way to get the gems! Get up to hundred thousand gems in a very simple way!
        PS: antiban and proxy connection are applied to each request.
      </v-card-subtitle>
      <v-card-text>
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-text-field class="mb-2" v-model="uid" :rules="uidrules" :counter="9" label="User ID (type without the '#')" required outlined :value="uid" id="uid"></v-text-field>
          <v-text-field class="mb-2" type="number" v-model="gems" :rules="gemsrules" :counter="5" label="Amount of gems (up to 99 999)" required outlined :value="gems" id="gems"></v-text-field>
          <v-btn color="success" @click="validate" :loading="loading" :disabled="loading">Generate Gems</v-btn>
          <v-btn color="dark" class="mt-2 mt-md-0 ml-0 ml-md-4" @click="validate" href="https://github.com/SlaVistaPL/cr-fake-gemgen">Github repository</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
export default {
    data: () => ({
      loader: null,
      loading: false,
      valid: true,
      uid: '',
      uidrules: [
        v => !!v || 'UID is required!',
        v => (v && v.length <= 9) || 'Player UID is too long!',
      ],
      gems: 0,
      gemsrules: [
        v => !!v || 'Number of gems is required!',
        v => (v && !isNaN(v)) || 'Value must be a number!',
        v => (v && v.length <= 5) || 'Number of gems must be less than or equal to 99 999!',
        v => (v && v.length > 0) || 'Number of gems must be greater than 0!',
      ]
    }),

    methods: {
      validate () {
        const form = this.$refs.form.validate();
        if (form) {
          this.loading = true;
          this.loader = 'loading';
        }
      }
    },

    watch: {
      loader () {
        const l = this.loader
        this[l] = !this[l]

        setTimeout(() => {
          this[l] = false;
          window.location.href = "/generated.webm";
        }, 3000)

        this.loader = null
      },
    },
}
</script>
