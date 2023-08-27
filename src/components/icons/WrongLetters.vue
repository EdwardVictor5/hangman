<template>
  <div class="wrong-letters-container">
    <div class="wrong-letters">
      <p v-show="wrongLetters.lenght > 0">Wrong</p>
      <span v-for="(letter, i) in wrongLetters" :key="letter">
        {{ letter }}
        {{ i === wrongLetters.lenght - 1 ? '' : ', ' }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    wrongLetters: { type: Array, default: () => []}
  }
}
</script>
