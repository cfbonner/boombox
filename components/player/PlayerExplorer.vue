<template>
  <div>
  <player-menu v-bind:playlist_selected="playlist_selected"
               @viewAll="toggleView"/>
  <ul v-if="!playlist_selected" class="flex flex-col text-xs h-full overflow-y-scroll list-disc border-b border-black divide-y divide-black">
    <li v-for="(playlist, i) in collection" class="flex w-full h-auto">
      <button v-on:click.prevent="selectPlaylist(i)"
              class="flex items-center w-full px-4 py-4 hover:bg-yellow-500"
              >
         <img class="w-4 h-full mr-4" src="~/assets/images/folder.svg" />
         <span class="h-full">{{ playlist.title }}</span>
      </button>
    </li>
  </ul>
  <player-playlist v-if="playlist_selected"
                   v-bind:playlist_index="playlist_index"
                   v-bind:playlist="selectedPlaylist"
                   v-bind:index.sync="index"
                   v-bind:collection_index.sync="playlist_index"
                   v-bind:playing.sync="playing"
                   @selectTrack="selectTrack"
                   />
  </div>
</template>

<script>
export default {
  props: {
    collection: Array,
    currentTrack: Object,
    playing: Boolean,
    index: Number
  },
  data: function() {
    return {
      playlist_selected: false,
      playlist_index: 0,
    }
  },
  computed: {
    selectedPlaylist() {
      return this.collection[this.playlist_index]
    }
  },
  methods: {
    selectTrack(index, playlist) {
      this.$emit('selectTrack', index, playlist)
    },
    selectPlaylist(index) {
      this.playlist_index = index
      this.toggleView()
    },
    toggleView() {
      this.playlist_selected = !this.playlist_selected
    }
  }
}
</script>

<style>
img.hidden {
  @apply invisible
}
/style>
