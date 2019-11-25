<template>
  <div class="container">
    <Textboard :userInput="userInput" @win="deleteInput++" @finished="finished++"/>
    <Inputbox @userInput="userInput = $event" :deleteInput="deleteInput" />
    <Timer :userInput="userInput" :finished="finished"/>
  </div>
</template>

<script>
import Textboard from './components/textboard/textboard.vue'
import Inputbox from './components/inputbox/inputbox.vue'
import Timer from './components/timer/timer.vue'

export default {
  data() {
    return {
      userInput: '',
      deleteInput: 0,
      finished: 0
    }
  },
  components: {
    Textboard,
    Timer,
    Inputbox
  }
}
</script>

