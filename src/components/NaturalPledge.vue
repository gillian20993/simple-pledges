<template>
  <div>
    <p>On June 7th, 2019, I am unplugging 
    to </p>
    <input class="activity" v-bind:class="{sample: !editing, fadeout: fadeout, fadein: fadein}" type="text" @focus="setEditing(true)" @blur="setEditing(false)" v-model="pledge" @input="go" :style="{ width: pledgeWidth + 'px' }"></input>
    <div><span ref="hiddenActivity" class="activity hidden">{{ pledge }}</span></div>
    <button class="pledgeButton" v-on:click="pledgeActivity">Pledge !</button>
    <div style="clear:both"></div>
    <div class="container" v-if='pledged' style="display: inline-block; width: auto; padding: 2rem">
               <div class="card" style="width: 275px">
                 <div class="card-body" >
                   <h5 style="text-align: center;" class="card-title">On June 7th, 2019, I will</h5>
                   <p style="text-align:center;">                   
                       <img height="100" src="http://www.unplugtoconnect.ca/wp-content/uploads/2018/10/big-UnplugToConnect-NoBackground.png" class="vc_single_image-img attachment-full" alt="" srcset="http://www.unplugtoconnect.ca/wp-content/uploads/2018/10/big-UnplugToConnect-NoBackground.png 450w, http://www.unplugtoconnect.ca/wp-content/uploads/2018/10/big-UnplugToConnect-NoBackground-300x259.png 300w" sizes="(max-width: 450px) 100vw, 450px">
                   </p>
                   <h5 style="text-align: center;" class="card-title">to {{ pledge }}</h5>
                 </div>
               </div>
           </div>
    <LegacySocial v-if='pledged' />
    <div style="clear:both"></div>
    <div id="container">
    <div id="box" >
      <p v-for="p in pledges.slice().reverse()">{{p}}</p>
    </div>
    </div>
    <!-- change this to geosheets -->
    <iframe src="https://www.geoshee.com/map/s:V6O5KYJQ/Unplug-to-Connect/embed" style="border:none;width:640px;height:480px"></iframe>
  </div>
  </div>
</template>

<script>
import * as pledges from './mocks/pledges.json'
import LegacySocial from './LegacySocial.vue'

export default {
  name: 'NaturalPledge',
  components: {
    LegacySocial
  },
  data () {
    return {
      editing: false,
      timer: null,
      checked: null,
      pledge: null,
      pledgeWidth: null,
      fadeout: false,
      fadein: false,
      pledges: pledges.default,
      pledged: false
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
      this.$nextTick(this.go)
    },
    pledgeActivity: function () {
      this.pledges.push(this.pledge)
      this.pledged = true
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
  background: rgba(255,255,255, 0.75);;
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
#container {
    height: 200px;
    width: 800px;
    border: 2px solid LightGray;
    overflow: hidden;
    margin: 25px auto;
    white-space:nowrap;
}
#box {
    -webkit-animation-name: fx;
    -webkit-animation-duration: 10s;
    -webkit-animation-iteration-count: infinite;
    -webkit-animation-timing-function: linear;
    
}


@-webkit-keyframes fx {
    0% {
        margin-top: -400px;
    }
    100% {
        margin-bottom: 800px;
    }
}
.pledgeButton {
  position:relative;
  top: -15px;
  margin: 10px;
}
body {
  background: top center no-repeat url('../assets/Activities.png');
}
</style>
