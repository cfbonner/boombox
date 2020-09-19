<template>
  <div id="player"
       class="boombox-player">
    <div class="boombox space-y-6">
      <div class="boombox-section space-y-1">
        <div class="text-xs font-bold"><span>{{ current_time || '00:00' }}</span> / <span>{{ duration || '00:00' }}</span></div>
        <div class="text-sm"><span>{{ title }}</span> - <span>{{ author }}</span></div>
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
      sounds: [],
      current_time: null,
      title: null,
      author: null
    }
  },
  created: function() {
    this.initialize()
  },
  watch: {
    index: function (index, last_index) {
      if (this.sounds[last_index].playing()) {
        this.sounds[last_index].stop()
        this.initialize()
        this.sounds[index].play()
      } else {
        this.initialize()
      }
    },
    playing: function(playing) {
      if (this.sounds[this.index] && playing) {
        this.sounds[this.index].play()
        setInterval(() => {
          this.current_time = Math.round(this.sounds[this.index].seek())
        }, 1000)
      } else if (this.sounds[this.index] && !playing) {
        this.sounds[this.index].pause()
      }
    }
  },
  methods: {
    initialize() {
      const track = this.songs[this.index]
      this.title = track.title
      this.author = track.author
      this.duration = null
      this.current_time = null
      this.sounds[this.index] = new Howl({
        src: [track.src],
        onload: () => {
          this.duration = this.sounds[this.index].duration()
        }
      })
    },
    play() {
      this.playing = !this.playing
    },
    pause() {
      this.playing = !this.playing
    },
    previous() {
      const current = this.index
      this.index = (current + this.songs.length - 1) % (this.songs.length)
    },
    next() {
      const current = this.index
      this.index = (current + 1) % (this.songs.length)
    }
  }
}
</script>

<style>
.boombox {
   @apply flex flex-col items-start
 }

.boombox-section {
  @apply flex flex-col items-start w-full;
  @screen sm {
    @apply w-2/3 m-auto;
  }
}

.boombox-player {
  @apply text-black p-4 fixed bottom-0 w-full border-t border-black
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
  @apply w-5 h-5
}

.control:hover {
  @apply bg-gray-200
}

.control:active {
  @apply bg-gray-400
}
</style>
