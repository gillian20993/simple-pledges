<template>
  <div>
    <p>On June 7th, 2019, I am unplugging 
    to </p>
    <input class="activity" v-bind:class="{editing: editing}" type="text" @focus="editing=true" @blur="setEditing" v-model="pledge" @input="go" :style="{ width: pledgeWidth + 'px' }"></input>
    <div><span ref="hiddenActivity" class="activity hidden">{{ pledge }}</span></div>
  </div>
</template>

<script>
import * as pledges from './mocks/pledges.json'

export default {
  name: 'NaturalPledge',
  data () {
    return {
      editing: false,
      timer: null,
      checked: null,
      pledge: null,
      pledgeWidth: null
    }
  },
  methods: {
    setEditing: function () {
      console.log(this.pledge)
      console.log('hola')
      console.log(this.$refs.hiddenActivity.clientWidth)
      if(!this.pledge) {
        this.editing = false
        // restart timer
        //this.triggerSampler();
      }
    },
    go: function ($event) {
      console.log('yoyo')
      console.log($event)
      this.pledgeWidth = this.$refs.hiddenActivity.clientWidth + 50
    },
    triggerSampler: function () {
      console.log('hola ')
      this.switchSample()
      this.timer = window.setTimeout(this.switchSample,2000)
    },
    switchSample: function () {
      //this.pledge = pledges[0]
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
  font-size: 1rem;
  font-weight: normal;
  display: inline-block;
  min-width:15rem;
  min-height:1rem;
  border:0;
  border-bottom:2px solid LightGray; /* consider text-underline */
  outline:0;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
},
.hidden {

}
</style>
