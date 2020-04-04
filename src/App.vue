<template>
  <div id="app">
    <Screen :screen="screen"/>
    <Keyboard @addValue="onAddValue" @removeValue="onRemoveValue" :keyboard="keyboard" />
  </div>
</template>

<script>
import Keyboard from './components/Keyboard'
import Screen from './components/Screen'

export default {
  name: 'App',
  components: {
    Keyboard,
    Screen
  },
  props: {
    keyCode: {
      type: Number,
      default: null
    },
    modifiers: {
      type: Array, // ['shiftKey', 'ctrlKey', 'altKey', 'metaKey']
      default: () => []
    },
    keydownEvent: {
      type: String,
      default: 'keydown'
    },
    keyupEvent: {
      type: String,
      default: 'keyup'
    },
    preventDefault: {
      type: Boolean
    }
  },
  data: function () {
    return {
      screen: '',
      isKeyDown: false,
      keyboard: {
        capsOn: false,
        default: {
          width: 40,
          css: 'light'
        },
        modifierCodes: ['CapsLock', 'ControlLeft', 'ShiftLeft', 'ControlRight', 'ShiftRight', 'MetaLeft', 'AltLeft'],
        keys: [
          {
            isPressed: false,
            lower: {key: '`', keyCode: 88},
            upper: {key: '~', keyCode: 88},
            showUpper: true
          },
          {
            isPressed: false,
            lower: {key: '1', keyCode: 88},
            upper: {key: '!', keyCode: 88},
            showUpper: true
          },
          {
            isPressed: false,
            lower: {key: '2', keyCode: 88},
            upper: {key: '@', keyCode: 88},
            showUpper: true,
            nudge: 14
          },
          {
            isPressed: false,
            lower: {key: '3', keyCode: 88},
            upper: {key: '#', keyCode: 88},
            showUpper: true
          },
          {
            isPressed: false,
            lower: {key: '4', keyCode: 88},
            upper: {key: '$', keyCode: 88},
            showUpper: true
          },
          {
            isPressed: false,
            lower: {key: '5', keyCode: 88},
            upper: {key: '%', keyCode: 88},
            showUpper: true,
            nudge: 15
          },
          {
            isPressed: false,
            lower: {key: '6', keyCode: 88},
            upper: {key: '^', keyCode: 88},
            showUpper: true
          },
          {
            isPressed: false,
            lower: {key: '7', keyCode: 88},
            upper: {key: '&', keyCode: 88},
            showUpper: true,
            nudge: 16
          },
          {
            isPressed: false,
            lower: {key: '8', keyCode: 88},
            upper: {key: '*', keyCode: 88},
            showUpper: true,
            nudge: 17
          },
          {
            isPressed: false,
            lower: {key: '9', keyCode: 88},
            upper: {key: '(', keyCode: 88},
            showUpper: true
          },
          {
            isPressed: false,
            lower: {key: '0', keyCode: 88},
            upper: {key: ')', keyCode: 88},
            showUpper: true,
            nudge: 17
          },
          {
            isPressed: false,
            lower: {key: '-', keyCode: 88},
            upper: {key: '_', keyCode: 88},
            showUpper: true,
            nudge: 15
          },
          {
            isPressed: false,
            lower: {key: '=', keyCode: 88},
            upper: {key: '+', keyCode: 88},
            showUpper: true
          },
          {
            isPressed: false,
            lower: {key: 'back', keyCode: 88},
            upper: '',
            css: 'dark sm',
            width: 83,
            modifier: true,
            code: 'Backspace'
          },
          {
            isPressed: false,
            lower: {key: 'tab', keyCode: 88},
            upper: '',
            css: 'dark sm',
            width: 60,
            modifier: true,
            code: 'Tab'
          },
          {
            isPressed: false,
            lower: {key: 'q', keyCode: 88},
            upper: {key: 'Q', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'w', keyCode: 88},
            upper: {key: 'W', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'e', keyCode: 88},
            upper: {key: 'E', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'r', keyCode: 88},
            upper: {key: 'R', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 't', keyCode: 88},
            upper: {key: 'T', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'y', keyCode: 88},
            upper: {key: 'Y', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'u', keyCode: 88},
            upper: {key: 'U', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'i', keyCode: 88},
            upper: {key: 'I', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'o', keyCode: 88},
            upper: {key: 'O', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'p', keyCode: 88},
            upper: {key: 'P', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: '[', keyCode: 88},
            upper: {key: '{', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: ']', keyCode: 88},
            upper: {key: '}', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: '\\', keyCode: 88},
            upper: {key: '|', keyCode: 88},
            width: 63
          },
          {
            isPressed: false,
            lower: {key: 'caps lock', keyCode: 88},
            upper: '',
            width: 90,
            css: 'dark',
            modifier: true,
            code: 'CapsLock'
          },
          {
            isPressed: false,
            lower: {key: 'a', keyCode: 88},
            upper: {key: 'A', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 's', keyCode: 88},
            upper: {key: 'S', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'd', keyCode: 88},
            upper: {key: 'D', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'f', keyCode: 88},
            upper: {key: 'F', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'g', keyCode: 88},
            upper: {key: 'G', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'h', keyCode: 88},
            upper: {key: 'H', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'j', keyCode: 88},
            upper: {key: 'J', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'k', keyCode: 88},
            upper: {key: 'K', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'l', keyCode: 88},
            upper: {key: 'L', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: ';', keyCode: 88},
            upper: {key: ':', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: '\'', keyCode: 88},
            upper: {key: '"', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'enter', keyCode: 88},
            upper: '',
            width: 80,
            css: 'dark',
            modifier: true,
            code: 'Enter'
          },
          {
            isPressed: false,
            lower: {key: 'shift', keyCode: 88},
            upper: '',
            width: 112,
            css: 'dark',
            modifier: true,
            code: 'ShiftLeft'
          },
          {
            isPressed: false,
            lower: {key: 'z', keyCode: 88},
            upper: {key: 'Z', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'x', keyCode: 88},
            upper: {key: 'X', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'c', keyCode: 88},
            upper: {key: 'C', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'v', keyCode: 88},
            upper: {key: 'V', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'b', keyCode: 88},
            upper: {key: 'B', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'n', keyCode: 88},
            upper: {key: 'N', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'm', keyCode: 88},
            upper: {key: 'M', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: ',', keyCode: 88},
            upper: {key: '<', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: '.', keyCode: 88},
            upper: {key: '>', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: '/', keyCode: 88},
            upper: {key: '?', keyCode: 88}
          },
          {
            isPressed: false,
            lower: {key: 'shift', keyCode: 88},
            upper: '',
            width: 104,
            css: 'dark',
            modifier: true,
            code: 'ShiftRight'
          },
          {
            isPressed: false,
            lower: {key: 'ctrl', keyCode: 88},
            upper: '',
            css: 'dark',
            width: 60,
            modifier: true,
            code: 'ControlLeft'
          },
          {
            isPressed: false,
            lower: {key: 'fn', keyCode: 88},
            upper: '',
            css: 'dark',
            modifier: true
          },
          {
            isPressed: false,
            lower: {key: 'start', keyCode: 88},
            upper: '',
            css: 'dark',
            modifier: true,
            code: 'MetaLeft'
          },
          {
            isPressed: false,
            lower: {key: 'alt', keyCode: 88},
            upper: '',
            css: 'dark',
            modifier: true,
            code: 'AltLeft'
          },
          {
            isPressed: false,
            lower: {key: 'space', keyCode: 88},
            upper: '',
            css: 'dark',
            width: 240,
            code: 'Space'
          },
          {
            isPressed: false,
            lower: {key: 'alt', keyCode: 88},
            upper: '',
            css: 'dark',
            width: 80,
            modifier: true,
            code: 'AltRight'
          },
          {
            isPressed: false,
            lower: {key: 'fn', keyCode: 88},
            upper: '',
            css: 'dark',
            width: 60,
            modifier: true
          },
          {
            isPressed: false,
            lower: {key: 'ctrl', keyCode: 88},
            upper: '',
            css: 'dark',
            width: 80,
            modifier: true,
            code: 'ControlRight'
          }
        ]
      }
    }
  },
  methods: {
    onAddValue (value) {
      var message = this.screen.split('')
      message.push(value)
      this.screen = message.join('')
    },
    onRemoveValue () {
      if (this.screen) {
        var message = this.screen.split('')
        message.pop()
        this.screen = message.join('')
      }
    },
    onPressed (e) {
      this.keyboard.keys.forEach(key => {
        if (key.lower.key === e.key || e.code === key.code) {
          key.isPressed = true
        }
      })

      if (this.keyboard.modifierCodes.indexOf(e.code) === -1) {
        if (e.key === 'Backspace') {
          this.onRemoveValue()
        } else if (e.key === 'Tab') {
          this.onAddValue('\t')
        } else {
          console.log('e.key', e.key)
          this.onAddValue(e.key)
        }
      } else {
        if (e.key === 'CapsLock') {
          this.keyboard.capsOn = !this.keyboard.capsOn
        }
        console.log('e.key', e.key)
      }
      console.log('onPressed', e.code, e, this.keyboard.modifierCodes.indexOf(e.code))
    },
    onReleased (e) {
      this.keyboard.keys.forEach(key => {
        if (key.lower.key === e.key || e.code === key.code) {
          key.isPressed = false
        }
      })
    },
    emitEvent (e) {
      if (event.type === 'keydown') {
        if (event.keyCode === this.keyCode || !this.keyCode) {
          if (this.preventDefault) {
            e.preventDefault()
          }

          // Check if all modifiers were clicked and return, if not
          if (this.modifiers.length) {
            for (const modifier of this.modifiers) {
              if (!event[modifier]) return
            }
          }
          // Success:
          this.onPressed(event)
        }
      } else if (event.type === 'keyup') {
        this.onReleased(event)
      }
    }
  },
  mounted () {
    window.addEventListener(this.keydownEvent, this.emitEvent)
    window.addEventListener(this.keyupEvent, this.emitEvent)
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
  margin-top: 28px;
}
</style>
