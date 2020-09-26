<template>
  <div class="flex h-screen overflow-hidden max-h-screen flex-col">
    <div class="h-full overflow-y-scroll">
      <player-explorer v-bind:collection="collection"
                       v-bind:current_track="current_track"
                       v-bind:current_playlist="current_playlist"
                       v-bind:playing="playing"
                       @select="select"
                       @pause="pause"
                       />
    </div>
    <div class="boombox-lower text-black p-4 w-full">
      <div class="space-y-4">
        <player-details  v-bind:current_time="current_time"
                         v-bind:current_duration="duration"
                         v-bind:current_title="current_track.title"
                         v-bind:current_artist="current_track.artist"
                         />
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
    collection: Array
  },
  data: function() {
    return {
      index: 0,
      collection_index: 0,
      playing: false,
      duration: 0,
      current_time: 0,
      current_track: {},
      current_playlist: null
    }
  },
  created: function() {
    this.current_playlist = this.collection[this.collection_index]
    this.initialize()
  },
  watch: {
    collection_index: function(index) {
      this.current_playlist = this.collection[index]
      this.changeTrack()
    },
    index: function (index) {
      this.changeTrack()
    },
    playing: function(playing) {
      if (this.current_track.audio && playing) {
        this.current_track.audio.play()
        setInterval(() => {
          this.current_time = !Number.isNaN(this.current_track.audio.seek()) ? this.current_track.audio.seek() : 0
        }, 1000)
      } else if (this.current_playlist.songs[this.index] && !playing) {
        this.current_track.audio.pause()
      }
    }
  },
  methods: {
    initialize() {
      this.playing = false
      this.current_track = this.current_playlist.songs[this.index]
      this.duration = 0
      this.current_time = 0
      this.current_track.audio = new Howl({
        src: this.current_track.src,
        html5: true,
        onload: () => {
          this.duration = this.current_track.audio.duration()
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
      this.index = (current + this.current_playlist.songs.length - 1) % (this.current_playlist.songs.length)
    },
    next() {
      const current = this.index
      this.index = (current + 1) % (this.current_playlist.songs.length)
    },
    select(track, playlist) {
      this.collection_index = playlist
      this.index = track

      if (!this.playing) {
        this.playing = !this.playing
      }
    },
    changeTrack() {
      if (this.current_track.audio.playing() || this.playing) {
        this.current_track.audio.stop()
        this.initialize()
        this.playing = true
        this.current_track.audio.play()
      } else {
        this.initialize()
      }
    }
  }
}
</script>

<style>
.boombox-section {
  @apply flex flex-col items-start w-full;
  @screen sm {
    @apply w-2/3 m-auto;
  }
}

.boombox-lower {
  position: relative;
}

.boombox-lower::before {
  position: absolute; z-index: -1;
  top: -1px; right: 0; left: 0;
  display: block;
  width: 100vw;
  height: 1px;
  background-color: #000;
  content: '';
}

</style>
