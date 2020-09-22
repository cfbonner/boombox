<template>
  <div class="flex h-screen overflow-hidden max-h-screen flex-col">
    <div class="h-full overflow-y-scroll">
      <player-collection v-if="!playlist_selected"
                         v-bind:collection="collection"
                         @selectPlaylist="selectPlaylist"
                         />
      <player-playlist v-if="playlist_selected"
                       v-bind:current_time="current_time"
                       v-bind:songs="songs"
                       v-bind:index.sync="index"
                       v-bind:playing.sync="playing"
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
      playlist_selected: false,
    }
  },
  computed: {
    songs: function() {
      return this.collection[this.collection_index].songs
    }
  },
  created: function() {
    this.initialize()
  },
  watch: {
    collection_index: function(index, last_index) {
      this.sounds = this.collection[index]
      this.playlist_selected = true
    },
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
          this.current_time = !Number.isNaN(this.sounds[this.index].seek()) ? this.sounds[this.index].seek() : 0
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
      this.artist = track.author
      this.duration = null
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
    setIndex(index) {
      if (this.index != index) {
        this.index = index
      }
      if (!this.playing) {
        this.playing = !this.playing
      }
    },
    selectPlaylist(index) {
      if (this.collection_index != index) {
        this.collection_index = index
      }
      if (!this.playlist_selected) {
        this.playlist_selected = !this.playlist_selected
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
