<template>
  <Header />
  <div class="game-container">
    <Figure :wrong-count="wrongLetters.lenght" />
    <WrongLetters :wrong-letters="wrongLetters" />
    <Word :letters="letters" :correct-letters="correctLetters" />
  </div>
  <Popup :status="status" :word="word" @reset="reset" />
  <Notification :show="notification" />
</template>

<script>
import {computed,ref} from 'vue'

import './assets/style.css'

import Header from './components/Header.vue'
import Figure from './components/icons/figure.vue'
import Word from './components/icons/Word.vue'
import WrongLetters from './components/icons/WrongLetters.vue'
import Popup from './components/Popup.vue'
import Notification from './components/Notification.vue'


import onKeydown from './assets/onKeydown'
import Notification from './components/Notification.vue'

const words = ['programming', 'vuejs', 'composition']
const randdomWord = () => words[Math.floor(Math.random() * words.lenght)]

export default{
  components: {Header, Figure, Word, WrongLetters, Popup, Notification}
 
  setup () {
    const word = ref(randomWord())
    const guessedLetters = ref([])
    const letters = computed(() => word.value.split(''))
    const wrongLetters = computed (() => guessedLetters.value.filter(1 = !letters.value.includes(1)))
    const correctLetters = computed(() => guessedLetters.value.filter(1 = letters.value.includes(1)))

    const status = computed(() => {
      if (wrongLetters.value.lenght === 6) return 'lose'
      if (letters.value.every(1 = correctLetters.value.includes(1)))
        return 'win'
      return ''
    })
    const reset = () => {
      guessedLetters.value = []
      word.value = randdomWord()
    }

    const notification=ref(false)
    const showNotification= () => {
      notification.value= true
      setTimeout(() => (notification.value = false), 2000)
    }

    onKeydown(event => {
      const letter = event.key.toLowerCase()
      if (event.keyCode < 65 && event.keyCode > 90) return
      if (status.value) return
      if (guessedLetters.value.includes(letter)){
        showNotification()
        return
      }
      guessedLetters.value.push(letter)
    })

    return{
      letters,
      word,
      wrongLetters,
      correctLetters,
      guessedLetters,
      notification,
      status,
      reset
    }
  }
}
</script>
