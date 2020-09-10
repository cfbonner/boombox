<template>
  <div id="player"
       class="boombox-player border border-black w-64 rounded p-6 shadow-lg">
    <div class="boombox space-y-6">
      <div class="boombox-section space-y-4">
        <div class="text-xs"><span>00:00</span> / <span>{{ duration }}</span></div>
        <div class="text-base"><span>{{ title }}</span> - <span>{{ author }}</span></div>
      </div>
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
               v-bind:class="{'hidden':playing}">
            <button v-on:click="play"
                    class="control">
              <span class="sr-only">play</span>
              <img src="~/assets/images/play.svg" />
            </button>
          </div>
          <div class="boombox-control"
               v-bind:class="{'hidden':!playing}">
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
    </div>
  </div>
</template>

<script>
const {Howl, Howler} = require('howler')
let sound

module.exports = {
  props: {
    songs: Array
  },
  data: function() {
    return {
      index: 0,
      playing: false,
      duration: 0,
      title: null,
      author: null
    }
  },
  created: function() {
    this.initialize()
  },
  methods: {
    initialize() {
      const track = this.songs[this.index]
      sound = new Howl({ src: [track.src] })
      this.title = track.title
      this.author = track.author
      this.duration = sound.duration()
    },
    play() {
      sound.play()
      this.playing = !this.playing
    },
    pause() {
      sound.pause()
      this.playing = !this.playing
    },
    previous() {
      this.index--
      this.initialize()
    },
    next() {
      this.index++
      this.initialize()
    }
  }
}
</script>

<style>
.boombox {
   @apply flex flex-col items-start
 }

.boombox-section {
  @apply flex flex-col items-start w-full
}

.boombox-player {
  @apply text-black border border-gray-900 p-6
}

.boombox-player {
  box-shadow: 1px 1px 0 1px black;
}

.boombox-controls {
  @apply flex items-center border border-black flex-grow w-full rounded
}

.boombox-control {
  @apply relative flex-grow h-8
}

.control {
  @apply absolute inset-0 bg-white flex items-center justify-center w-full rounded
}

.control.hidden {
  @apply invisible
}

.control img {
  @apply w-4 h-4
}

.control:hover {
  @apply bg-gray-200
}

.control:active {
  @apply bg-gray-400
}
</style>
