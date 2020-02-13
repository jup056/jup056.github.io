<template>
  <v-menu
    ref="menu"
    v-model="menu"
    :close-on-content-click="false"
    :return-value.sync="date"
    transition="scale-transition"
    offset-y
    min-width="290px"
  >
  <template v-slot:activator="{ on }">
    <v-text-field
      v-model="date"
      label="Choose a date"
      readonly
      v-on="on"
    ></v-text-field>
  </template>
  <v-date-picker v-model="date" no-title scrollable :min="today">
    <v-spacer></v-spacer>
    <v-btn text color="primary" @click="menu = false">Cancel</v-btn>
    <v-btn text color="primary" @click="emitDate(date)">OK</v-btn>
    </v-date-picker>
  </v-menu>
</template>

<script>
import moment from 'moment';

export default {
  name: 'app',
  data () {
    return {
      menu: false,
      today: moment().format('YYYY-MM-DD'),
      date: moment().format('YYYY-MM-DD'),
      modal: false,
    }
  },
  methods: {
    emitDate(date) {
      this.$emit('emitDate', date);
      this.$refs.menu.save(date);
    }
  }
  // props: {

  // },
}
</script>