<template>
  <ul class="flex flex-col text-xs h-auto overflow-y-scroll list-disc border-b border-black divide-y divide-black">
    <li v-for="(song, i) in playlist.songs" class="flex w-full h-full">
      <button v-on:click.prevent="selectTrack(i, playlist_index)"
              href="#"
              class="flex items-center w-full px-4 py-4 hover:bg-yellow-500"
              v-bind:class="{'bg-yellow-500':currentlyPlaying(i, playlist.id)}">
         <img class="w-4 h-4 mr-4" src="~/assets/images/play.svg" v-if="(index == i && !playing) || (index != i)" />
         <img class="w-4 h-4 mr-4" src="~/assets/images/pause.svg" v-if="currentlyPlaying(i)" />
         <span class="h-full">{{ song.title }}</span>
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    playlist: Object,
    playlist_index: Number,
    index: Number,
    collection_index: Number,
    playing: Boolean,
  },
  methods: {
    selectTrack(index, playlist) {
      this.$emit('selectTrack', index, playlist)
    },
    currentlyPlaying: function(song, playlist) {
      // TODO : this is wrong
      return this.index == song && this.playlist_playing == playlist && this.playing
    }
  }
}
</script>

<style>
img.hidden {
  @apply invisible
}
/style>
