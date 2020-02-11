<template>
  <div id="app">
   <v-app light>
    <v-toolbar color="white">
      <h1 style="font-family: Brush Script Std;">Estimators</h1>
    </v-toolbar>
    <v-content>
      <section>
        <v-parallax :src="require('../public/assets/wuhan-estimator.png')">
          <v-layout
            column
            align-center
            justify-center
            class="white--text"
          >
            <h1 class="white--text mb-2 display-1 font-weight-thin text-center">Number Of Death</h1>
            <vue-odometer :value="numOfDeath" format="d" theme="car" class="odometer" animation="smooth"></vue-odometer>
            <br>
            <h1 class="white--text mb-2 display-1 font-weight-thin text-center">Number Of Infected</h1>
            <vue-odometer :value="numOfInfected" theme="car" format="d" class="odometer" animation="smooth"></vue-odometer>
            <div class="subheading mb-4 font-weight-thin text-center">From Wuhan Coronavirus</div>
          </v-layout>
        </v-parallax>
      </section>

      <section>
        <v-layout
          column
          wrap
          class="my-12"
          align-center
        >
          <v-flex xs12 sm4 class="my-4">
            <div class="text-center">
              <h2 class="headline">Summary of Wuhan Corona Virus</h2>
              <span class="subheading">
                Last updated in 02-02-2020
              </span>
            </div>
          </v-flex>
          <v-flex xs12>
            <v-container grid-list-xl>
              <v-layout row wrap align-center>
                <v-flex xs12 md4>
                  <v-card flat class="transparent">
                    <v-card-text class="text-center">
                      <img width="64" src="../public/assets/death.png"/>
                    </v-card-text>
                    <v-card-title primary-title class="layout justify-center">
                      <div class="headline text-center">Number Of Death</div>
                    </v-card-title>
                    <date-picker/>
                    <v-card-text class="display-3 font-weight-thin" align="center">
                      110
                    </v-card-text>
                  </v-card>
                </v-flex>
                <v-flex xs12 md4>
                  <v-card flat class="transparent">
                    <v-card-text class="text-center">
                      <img width="64" src="../public/assets/infection.png"/>
                    </v-card-text>
                    <v-card-title primary-title class="layout justify-center">
                      <div class="headline">Number Of Infected</div>
                    </v-card-title>
                    <date-picker/>
                    <v-card-text class="display-3 font-weight-thin" align="center">
                      6719
                    </v-card-text>
                  </v-card>
                </v-flex>
                <v-flex xs12 md4>
                  <v-card flat class="transparent" width="1000">
                    <v-card-text class="text-center">
                      <img src="../public/assets/lethality.png"/>
                    </v-card-text>
                    <v-card-title primary-title class="layout justify-center">
                      <div class="headline text-center">Lethality</div>
                    </v-card-title>
                    <v-card-text class="display-3 font-weight-thin" align="center">
                      2.2%
                    </v-card-text>
                  </v-card>
                </v-flex>
              </v-layout>
            </v-container>
          </v-flex>
        </v-layout>
      </section>

      <!-- <section>
        <v-parallax :src="require('../public/assets/statistics2.jpg')" height="380">
          <v-layout column align-center justify-center>
            <div class="headline white--text mb-4 text-center">Check out other Estimators!</div>
            <em>Wanna know usage of plastic in 2030?</em>
            <v-btn
              class="mt-12"
              color="blue lighten-2"
              dark
              large
              href="/pre-made-themes"
            >
              Check other Estimators
            </v-btn>
          </v-layout>
        </v-parallax>
      </section>

      <section>
        <v-container grid-list-xl>
          <v-layout row wrap justify-center class="my-12">
            <v-flex xs12 sm4>
              <v-card flat class="transparent">
                <v-card-title primary-title class="layout justify-center">
                  <div class="headline">Estimate number of Death</div>
                </v-card-title>
                <RandomChart></RandomChart>
              </v-card>
            </v-flex>
            <v-flex xs12 sm4 offset-sm1>
              <v-card flat class="transparent">
                <v-card-title primary-title class="layout justify-center">
                  <div class="headline">Estimate number of Infected</div>
                </v-card-title>
                <RandomChart></RandomChart>
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>
      </section> -->

      <v-footer color="blue darken-2">
        <v-layout row wrap align-center>
          <v-flex xs12>
            <div class="white--text ml-4">
              Please contact to 
              by <a class="white--text" href="https://vuetifyjs.com" target="_blank">jwhan0316@gmail.com</a>
              Junyoung Park
            </div>
          </v-flex>
        </v-layout>
      </v-footer>
    </v-content>
  </v-app>
  </div>
</template>

<script>
import Vuetify from 'vuetify'
import VueOdometer from 'v-odometer/src'
import DatePicker from './components/DatePicker.vue'
import { setTimeout } from 'timers';

export default {
  name: 'app',
  Vuetify: new Vuetify(),
  data () {
        let table = [
                    [1,41],
                    [1,41],
                    [1,41],
                    [1,41],
                    [2,45],
                    [2,45],
                    [2,62],
                    [2,121],
                    [3,198],
                    [6,291],
                    [9,440],
                    [17,571],
                    [25,830],
                    [41,1287],
                    [56,1975],
                    [80,2744],
                    [106,4515],
                    [132,5974],
                    [170,7711],
                    [213,9692],
                    [259,11791],
                    [304,14380],
                    [361,17205],
                    [425,20440],
                    [490,24324],
                    [563,28018],
                    ];

      let l = table.length; //length of table

      let table_x1 = [1]; //creating an array with one element
      let table_x2 = []; //creating empty array

      let sum = 0; //sum of element in table_x2
      let num = 0; //num of non-zero elements in table_x2
      let avg_percentage = 0; //sum/num - 0.1 (If you substract 0.1, it gives you a better value)
      this.death_today = 0; // number of death occured on the day

      let i = 0;
      for (i=1; i<=l-1; i++){
        table_x1[i] = table[i][0]-table[i-1][0]; //calculating number of death occured on single day
        if (table_x1[i-1]==0){ //calculating percentage of death increment compare to the day before
          table_x2[i-1] = 0; //if an element in table_x1 is zero, then skip division and set new element in table_x2 as zero
        }else{
          table_x2[i-1] = table_x1[i]/table_x1[i-1]; //if an element in table_x1 is not zero, perform division
          num++; //calculating number of non-zero elements in table_x2
        }
        sum = sum + table_x2[i-1]; //sum of all elements in table_x2 
      }
      avg_percentage = sum/num-0.1; //calculating average percentage over total period of time (since day 1)
      this.death_today = table[l-1][0]+Math.round( table_x1[table_x1.length-1]*avg_percentage ); //returns number of death will occur the next day
      table.push([this.death_today,0]); // creating new array in table
    return {
      title: 'Estimator',
      numOfDeath: 0,
      numOfInfected: 0,
      duration: 0,
      // junyoung's data
      n: this.death_today,
      x: 421,
      n2: 2500,
      x2: 16880,
    }
  },
  mounted() {
    clearTimeout();
    console.log('component has mounted');
    this.calculateNum();
    this.startTime();
  },
  components: {
    'vue-odometer': VueOdometer,
    'date-picker': DatePicker,
    // RandomChart,
  },
  destroyed() {
    console.log('destroyed');
    clearTimeout();
  },
  methods: {
    startTime() {
      let td = 86400 / this.n;
      let ti = 86400 / this.n2;
      let today = new Date();
      let h = today.getHours();
      let m = today.getMinutes();
      let s = today.getSeconds();

      h = h + 16;
      if (h >= 24) {h = h - 24}

      h = h * 3600; 
      m = m * 60;

      let current_time_in_second = h + m + s;

      let c = current_time_in_second/td;
      let c2 = current_time_in_second/ti;

      this.numOfDeath = this.x + Math.round(c);
      this.numOfInfected = this.x2 + Math.round(c2);  

      console.log("Num Of Death: ", this.numOfDeath, "Num Of Infected", this.numOfInfected);

      setTimeout(this.startTime, 500);
    },
  }
}
</script>

<style>
.odometer {
  font-size: 50px;
}
</style>
