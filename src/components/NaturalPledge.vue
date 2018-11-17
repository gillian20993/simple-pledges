<template>
  <div>
    <p>On June 7th, 2019, I am unplugging 
    to </p>
    <div class="activity" v-bind:class="{editing: editing}" type="text" @focus="editing=true" @blur="setEditing" @input="setPledge($event)" v-html="pledge" contenteditable="true"></div>
  </div>
</template>

<script>
import * as pledges from './mocks/pledges.json'

export default {
  name: 'NaturalPledge',
  data () {
    return {
      editing: false,
      pledge: '',
      timer: null
    }
  },
  methods: {
    setEditing: function () {
      console.log(this.pledge)
      console.log('hola')
      if(this.pledge='') {
        this.editing = false
        // restart timer
        this.triggerSampler();
      }
    },
    setPledge: function($event) {
      this.pledge = $event.target.innerText
    },
    triggerSampler: function () {
      console.log('hola ')
      this.switchSample()
      this.timer = window.setTimeout(this.switchSample,2000)
    },
    switchSample: function () {
      this.pledge = pledges[0]
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
span {
  border: 1px solid black;
  outline: none;
  min-width:15rem;
  min-height:1rem;
}
.activity {
  display: inline-block;
  min-width:15rem;
  min-height:1rem;
  border:0;
  border-bottom:2px solid LightGray; /* consider text-underline */
  outline:0;
}
</style>
