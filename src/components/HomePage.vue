<template>
  <v-container>
    <v-row class="text-center">
      <v-col 
        cols="12" 
        style="margin-top:100px"
      > 
      </v-col>
      <v-col 
        class="mb-4" 
        cols="12"
      >
        <h3 
          class="display-2 font-weight-bold mb-3"
        >
          Country
        </h3>
      </v-col>
      <v-col 
       class="mb-4"
       width="300"
      >
        <v-text-field 
          v-model="inputText"
          class="input"
          label=""
          placeholder="Type any country name" 
          outlined
          @input="showSuggest()"
        >
        </v-text-field>

      <v-list
      v-if="inputText.length > 0 && this.items.length > 0"
      >
        <v-list-item
          v-for="item in items.slice(0, 5)"
          :key="item.name"
          class="suggestion-list"
          link
          :to="'/country-page/'+item.name"
        >
          <v-list-item-title v-text="item.name"></v-list-item-title>
        </v-list-item>
      </v-list>
      <!-- Data Not Found -->
       <v-list
      v-if="inputText.length > 0 && this.items.length === 0"
      >
        <v-list-item
          class="suggestion-list"
          link
        >
          <v-list-item-title>Data Not Found</v-list-item-title>
        </v-list-item>
      </v-list>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
export default {
  name: "HelloWorld",
  data(){
    return{
      show: false,
      inputText: '',
      items: [],
    }
  },

  methods:{
    showSuggest(){
      this.items = [],
      axios.get('https://restcountries.eu/rest/v2/name/'+this.inputText+'/?_limit=10',)
      .then((res)=>{
        this.items = res.data
      })
    }
  },

};
</script>

<style>
.input {
  width: 700px;
  height: 60px;
  left:220px;
  border-radius: 10px;
}
.suggestion-list{
  width: 700px;
  left:220px;
  text-align: left;
}
</style>
