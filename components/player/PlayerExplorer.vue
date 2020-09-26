<template>
  <div>
  <player-explorer-menu v-bind:playlist_selected="playlist_selected"
               @viewAll="toggleView"/>
  <ul v-if="!playlist_selected" class="flex flex-col text-xs h-full overflow-y-scroll list-disc border-b border-black divide-y divide-black">
    <li v-for="(playlist, i) in collection" class="flex w-full h-auto">
      <button v-on:click.prevent="selectPlaylist(i)"
              class="explorer-item"
              >
         <img class="w-4 h-full mr-4" src="~/assets/images/folder.svg" v-if="!isCurrentlyPlaying(playlist)"/>
         <img class="w-4 h-full mr-4" src="~/assets/images/volume.svg" v-if="isCurrentlyPlaying(playlist)"/>
         <span class="h-full">{{ playlist.title }}</span>
      </button>
    </li>
  </ul>
  <player-explorer-playlist v-if="playlist_selected"
                            v-bind:playlist_index="playlist_index"
                            v-bind:playlist="selectedPlaylist"
                            v-bind:playing="playing"
                            v-bind:current_track="current_track"
                            @selectTrack="selectTrack"
                            @pauseTrack="pauseTrack"
                            />
  </div>
</template>

<script>
export default {
  props: {
    collection: Array,
    current_playlist: Object,
    current_track: Object,
    collection_index: Number,
    playing: Boolean,
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
    },
  },
  methods: {
    selectTrack(index) {
      this.$emit('select', index, this.playlist_index)
    },
    pauseTrack() {
      this.$emit('pause')
    },
    selectPlaylist(index) {
      this.playlist_index = index
      this.toggleView()
    },
    toggleView() {
      this.playlist_selected = !this.playlist_selected
    },
    isCurrentlyPlaying(playlist) {
      return playlist == this.current_playlist &&
             this.playing
    }
  }
}
</script>

<style>
.explorer-item {
  @apply flex items-center w-full px-4 py-4;
}

@media (hover: hover) {
  .explorer-item:hover {
    @apply bg-yellow-500;
  }
}

img.hidden {
  @apply invisible
}
</style>
