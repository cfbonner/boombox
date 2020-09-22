<template>
  <div class="boombox-section">
    <div class="boombox-controls border-2 divide-x divide-black">
      <div class="boombox-control">
        <button id="previous"
          class="control"
          v-on:click="previous">
          <span class="sr-only">previous</span>
          <img src="~/assets/images/rewind.svg" />
        </button>
      </div>
      <div class="boombox-control"
           v-bind:class="{'hidden':this.playing}">
        <button v-on:click="play"
                class="control">
          <span class="sr-only">play</span>
          <img src="~/assets/images/play.svg" />
        </button>
      </div>
      <div class="boombox-control"
           v-bind:class="{'hidden':!this.playing}">
        <button v-on:click="pause"
                class="control">
          <span class="sr-only">pause</span>
          <img src="~/assets/images/pause.svg" />
        </button>
      </div>
      <div class="boombox-control">
        <button v-on:click="next"
                id="next"
                class="control">
          <span class="sr-only">next</span>
          <img src="~/assets/images/fast-forward.svg" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    playing: Boolean
  },
  methods: {
    play: function() {
      this.$emit('play')
    },
    pause: function() {
      this.$emit('pause')
    },
    next: function() {
      this.$emit('next')
    },
    previous: function() {
      this.$emit('previous')
    },
  }
}
</script>

<style scoped>
.boombox-controls {
  @apply flex items-center border border-black flex-grow w-full
}

.boombox-control {
  @apply relative flex-grow h-10
}

.control {
  @apply flex items-center justify-center w-full h-full
}

.control.hidden {
  @apply invisible
}

.control img {
  @apply w-5 h-5
}

.control:hover {
  @apply bg-yellow-500
}

.control:active {
  @apply bg-red-500
}
</style>
