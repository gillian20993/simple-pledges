<template>
  <div>
    <p>On June 7th, 2019, I am unplugging 
    to </p>
    <input class="activity" v-bind:class="{sample: !editing, fadeout: fadeout, fadein: fadein}" type="text" @focus="setEditing(true)" @blur="setEditing(false)" v-model="pledge" @input="go" :style="{ width: pledgeWidth + 'px' }"></input>
    <div><span ref="hiddenActivity" class="activity hidden">{{ pledge }}</span></div>
    <button v-on:click="pledgeActivity">Pledge !</button>
    <p v-for="p in pledges.slice().reverse()">{{p}}</p>
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
      pledgeWidth: null,
      fadeout: false,
      fadein: false,
      pledges: pledges.default
    }
  },
  created: function () {
    this.triggerSampler()
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
      this.pledge = this.pledges[rand]
      this.timer = window.setTimeout(this.switchSample,2000)
    },
    pledgeActivity: function () {
      this.pledges.push(this.pledge)
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
  animation-duration: 2s;
  animation-iteration-count: infinite;
  animation-name: fade;
}
@keyframes fade {
  from {
    color: white;
  }

  15% {
    color: SlateGray;
  }

  85% {
    color: SlateGrey;
  }

  to {
    color: white;
  }
}
.hidden {
  visibility: hidden;
}
.fadeout {
  color: white;
  transition-property: all;
  transition-duration: 0.3s;
  transition-delay: 1.7s;
}
.fadein {
  color: SlateGray;
  transition-property: all;
  transition-duration: 0.3s;
}
</style>
