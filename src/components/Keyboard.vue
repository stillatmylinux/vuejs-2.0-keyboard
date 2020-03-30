<template>
  <div class="layout">
    <div @mouseup="toggleCaps(button)" @mousedown="toggleCaps(button)" @click.stop="updateScreen(button)" class="key" :class="[button.css ? button.css : keyboard.default.css, button.showUpper ? 'view-upper' : '', button.isPressed ? 'pressed' : '']" v-for="(button, index) in keyboard.keys" v-bind:key="index" :style="{width: (button.width ? button.width : keyboard.default.width)+'px'}"><span v-if="button.showUpper && !keyboard.capsOn">{{ button.upper.key }}</span><span>{{ keyboard.capsOn && button.upper ? button.upper.key : button.lower.key }}</span></div>
  </div>
</template>

<script>
export default {
  name: 'Keyboard',
  methods: {
    toggleCaps (button) {
      if (button.lower.key === 'shift') {
        this.keyboard.capsOn = !this.keyboard.capsOn
      }
    },
    updateScreen (button) {
      if (!button.modifier) {
        var value = this.keyboard.capsOn && button.upper ? button.upper.key : button.lower.key
        value = value === 'space' ? ' ' : value
        this.$emit('addValue', value)
      } else if (button.lower.key === 'back') {
        this.$emit('removeValue')
      } else if (button.lower.key === 'caps lock') {
        this.keyboard.capsOn = !this.keyboard.capsOn
      } else if (button.lower.key === 'shift') {
        // this.keyboard.capsOn = true
      }
    }
  },
  data: function () {
    return {

    }
  },
  props: [
    'keyboard'
  ]
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.layout {
  background-color:#aaaaaa;
  border: 3px solid #2b2b2b;
  padding: 2px;
  border-radius: 3px;
  text-align: center;
  width: 688px;
  margin:auto;
}
.key {
  height: 40px;
  line-height: 40px;
  font-weight: bold;
  color: white;
  border-radius: 3px;
  margin: 3px;
  display: inline-block;
  text-align: center;
  -moz-user-select: none;
  -webkit-user-select: none;
  font-size: 11px;
  vertical-align: middle;
  position: relative;
}
.key:hover {
  background-color: #88aa00 !important;
  cursor: pointer;
}
.light {
  background-color: #494949;
}
.key.dark {
  background-color: #2b2b2b;
}
.key.view-upper span {
  position: absolute;
  top: -3px;
}
.key.view-upper span + span {
  top: 6px;
}
.key.pressed {
  background-color: #88aa00;
}
</style>
