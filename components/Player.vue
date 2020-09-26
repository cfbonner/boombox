<template>
  <div class="flex h-screen overflow-hidden max-h-screen flex-col">
    <div class="h-full overflow-y-scroll">
      <player-explorer v-bind:collection="collection"
                       v-bind:index="index"
                       v-bind:playing="playing"
                       @selectTrack="selectTrack"
                       />
    </div>
    <div class="text-black p-4 w-full">
      <div class="boombox space-y-4">
        <player-details  v-bind:current_time="current_time"
                         v-bind:current_duration="duration"
                         v-bind:current_title="title"
                         v-bind:current_artist="artist"
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
      sounds: [],
      duration: 0,
      current_time: 0,
      title: null,
      artist: null,
      current_track: null,
      current_playlist: null
    }
  },
  created: function() {
    this.current_playlist = this.collection[this.collection_index]
    this.initialize()
  },
  watch: {
    collection_index: function(index, last_index) {
      this.collection[index]
    },
    index: function (index) {
      if (this.current_track.playing() || this.playing) {
        this.current_track.stop()
        this.initialize()
        this.playing = true
        this.current_track.play()
      } else {
        this.initialize()
      }
    },
    playing: function(playing) {
      if (this.current_track && playing) {
        this.current_track.play()
        setInterval(() => {
          this.current_time = !Number.isNaN(this.current_track.seek()) ? this.current_track.seek() : 0
        }, 1000)
      } else if (this.current_playlist.songs[this.index] && !playing) {
        this.current_track.pause()
      }
    }
  },
  methods: {
    initialize() {
      this.playing = false
      this.current_track = this.current_playlist.songs[this.index]
      this.title = this.current_track.title
      this.artist = this.current_track.author
      this.duration = 0
      this.current_time = 0
      this.current_track = new Howl({
        src: [this.current_track.src],
        onload: () => {
          this.duration = this.current_track.duration()
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
    selectTrack(track, playlist) {
      this.collection_index = playlist
      this.index = track

      if (!this.playing) {
        this.playing = !this.playing
      }
    },
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
</style>
