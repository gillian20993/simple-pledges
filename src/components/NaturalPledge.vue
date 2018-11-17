<template>
  <div>
    <p>On June 7th, 2019, I am unplugging 
    to </p>
    <input class="activity" v-bind:class="{sample: !editing}" type="text" @focus="setEditing(true)" @blur="setEditing(false)" v-model="pledge" @input="go" :style="{ width: pledgeWidth + 'px' }"></input>
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
    setEditing: function (isFocus) {
      if(isFocus) { //focus
        if(this.timer) {
          window.clearTimeout(this.timer)
        }
        if(!this.editing) {
          this.pledge = ''
        }
        this.editing = true
      }
      if(!isFocus) { //blur
        if(!this.pledge) {
          this.editing = false
          this.triggerSampler();
        }
      }
    },
    go: function ($event) {
      this.pledgeWidth = this.$refs.hiddenActivity.clientWidth + 50
    },
    triggerSampler: function () {
      window.clearTimeout(this.timer)
      this.switchSample()
    },
    switchSample: function () {
      let rand = Math.floor(Math.random()*pledges.length)
      this.pledge = pledges.default[rand]
      this.timer = window.setTimeout(this.switchSample,2000)
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
}
.sample {
  color: SlateGray;
}
.hidden {
  visibility: hidden;
}
</style>
