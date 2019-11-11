<template>
  <div class="container">
    <Textboard :userInput="userInput" @win="deleteInput++"/>
    <Inputbox @userInput="userInput = $event" :deleteInput="deleteInput" />
  </div>
</template>

<script>
import Textboard from './components/textboard/textboard.vue'
import Inputbox from './components/inputbox/inputbox.vue'

export default {
  data() {
    return {
      userInput: '',
      deleteInput: 0
    }
  },
  components: {
    Textboard,
    Inputbox
  }
}
</script>

