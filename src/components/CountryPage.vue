<template>
  <v-container>
    <v-btn color="purple lighten-2" dark to="/">
      <v-icon left>
        mdi-arrow-left
      </v-icon>
      Back to Homepage
    </v-btn>
    <v-row class="mt-6">
        <h1 class="display-1 font-weight-bold mb-3 mt-5">
          {{ this.data[0].name }}
        </h1>
    
        <v-img
            class="display-2 font-weight-bold mb-3 mt-5 ml-2"
            max-height="35"
            max-width="55"
            :src="this.data[0].flag"
        ></v-img>
    </v-row>
    <div>
    <v-chip
    small
    color="blue lighten-4"
    text-color="white"
    v-show="data[0].altSpellings[0] ? true : false"
    >
    {{ this.data[0].altSpellings[0] }}
    </v-chip>
    <v-chip
    small
    color="blue lighten-4"
    text-color="white"
    v-show="data[0].altSpellings[1] ? true : false"
    >
    {{ this.data[0].altSpellings[1] }}
    </v-chip>
    <v-chip
    small
    color="blue lighten-4"
    text-color="white"
    v-show="data[0].altSpellings[2] ? true : false"
    >
    {{ this.data[0].altSpellings[2] }}
    </v-chip>
  </div>
  <v-row class="mt-5">
      <v-col cols="6">
        <v-row>
           <h3>Latlong</h3>
          <div style="font-size:50px;color:#ba68c8">
              {{ this.data[0].latlng[0] }},{{ this.data[0].latlng[1] }}
          </div>
          <v-img
            class="display-2 font-weight-bold mb-3"
            style="margin-left:120px"
            max-height="200"
            max-width="200"
            src="../assets/globe.svg"
        ></v-img>
        </v-row>
      </v-col>
         <v-col cols="6">
          <h3>Calling Code</h3>
           <div>
              Capital : {{ this.data[0].capital }} <br>
              Region : {{ this.data[0].region }} <br>
              Subregion : {{ this.data[0].subregion }} <br>
          </div>
      </v-col>
      <v-col cols="6">
          <h3>Calling Code</h3>
           <div style="font-size:50px;color:#ba68c8">
              {{ this.data[0].callingCodes[0] }}
          </div>
          <a href="">{{ this.countCallCode.length }} countries</a> with this calling code
      </v-col>
      <v-col cols="6">
          <h3>Currency</h3>
           <div style="font-size:50px;color:#ba68c8">
              {{ this.data[0].currencies[0].code }}
          </div>
          <a href="">{{ this.countCurrencies.length }} countries</a> with this currencies
      </v-col>
  </v-row>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      name: this.$route.params.name,
      data: [],
      countCallCode: [],
      countCurrencies: [],
    };
  },

  computed:{
      // eslint-disable-next-line vue/return-in-computed-property
      CallCode(){
          if(this.data.length > 0){
              this.getCallingCode(this.data[0].callingCodes[0])
              return this.data[0].callingCodes[0]
          }
      },
       // eslint-disable-next-line vue/return-in-computed-property
       Currencies(){
          if(this.data.length > 0){
              this.getCurrencies(this.data[0].currencies[0].code)
              return this.data[0].currencies[0].code
          }
      },
      
  },

  mounted() {
    this.getCountry()
  },

  methods: {
    getCountry() {
        this.data = []
      axios("https://restcountries.eu/rest/v2/name/" + this.name).then(res => {
        this.data = res.data;
      });
    },

    getCallingCode(cc){
      this.countCallCode = []
        axios("https://restcountries.eu/rest/v2/callingcode/" + cc).then(res => {
        this.countCallCode = res.data
      });
    },

     getCurrencies(cr){
         this.countCurrencies = []
        axios("https://restcountries.eu/rest/v2/currency/" + cr).then(res => {
        this.countCurrencies = res.data
      });
    },

    }
    
};
</script>

<style>
.purple-text{
    font-size:"40pt"
}
</style>
