<template>
  <div class="flex h-screen overflow-hidden max-h-screen flex-col">
    <ul class="flex flex-col text-xs h-full overflow-y-scroll list-disc border-b border-black divide-y divide-black">
      <li v-for="(song, i) in songs" class="flex w-full h-full">
        <button v-on:click.prevent="playAtIndex(i)"
           href="#"
           class="flex items-center w-full px-4 py-4 hover:bg-yellow-500"
           v-bind:class="{'bg-yellow-500':index == i && playing}"
           >
           <img class="w-4 h-full mr-4" src="~/assets/images/play.svg" v-if="(index == i && !playing) || (index != i)" />
           <img class="w-4 h-full mr-4" src="~/assets/images/pause.svg" v-if="index == i && playing" />
           <span class="h-full">{{ song.title }}</span>
        </button>
      </li>
    </ul>
    <div class="boombox-player">
      <div class="boombox space-y-4">
        <div class="boombox-section space-y-1">
          <div class="text-xs font-bold"><span>{{ current_time || '00:00' }}</span> / <span>{{ duration || '00:00' }}</span></div>
          <div class="text-sm"><span>{{ title }}</span> - <span>{{ author }}</span></div>
        </div>
        <player-controls v-bind:playing="playing"
                         @next="next"
                         @play="play"
                         @pause="pause"
                         @previous="previous"
          />
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
      if (this.sounds[last_index].playing() || this.playing) {
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
        },
        onend: () => {
          this.next()
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
    },
    playAtIndex(index) {
      if (this.index != index) {
        this.index = index
      }
      if (!this.playing) {
        this.playing = !this.playing
      }
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
  @apply text-black p-4 w-full
}

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

img.hidden {
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
