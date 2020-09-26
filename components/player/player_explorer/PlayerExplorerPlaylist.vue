<template>
  <ul class="flex flex-col text-xs h-auto overflow-y-scroll list-disc border-b border-black divide-y divide-black">
    <li v-for="(song, i) in playlist.songs" class="flex w-full h-full">
      <button v-on:click.prevent="toggleTrack(i, song)"
              href="#"
              class="explorer-item"
              v-bind:class="{'bg-yellow-500':currentlySelected(song)}">
         <img class="w-4 h-4 mr-4" src="~/assets/images/play.svg" v-if="!currentlyPlaying(song)" />
         <img class="w-4 h-4 mr-4" src="~/assets/images/pause.svg" v-if="currentlyPlaying(song)" />
         <span class="h-full">{{ song.title }}</span>
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    playlist: Object,
    current_track: Object,
    playlist_index: Number,
    playing: Boolean,
  },
  methods: {
    toggleTrack(index, song) {
      if (this.currentlyPlaying(song)) {
        this.$emit('pauseTrack')
      } else {
        this.$emit('selectTrack', index)
      }
    },
    currentlySelected(song) {
      return this.current_track.title == song.title
    },
    currentlyPlaying(song) {
      return this.currentlySelected(song) && this.playing
    }
  }
}
</script>

<style>
img.hidden {
  @apply invisible
}
/style>
