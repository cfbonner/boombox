<template>
  <div>
    <header>
      <h1 class="sr-only">
        boombox
      </h1>
    </header>
    <main>
      <Player v-bind:collection="collection"/>
    </main>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      collection: [
        {
          id: 1,
          title: 'Ritual',
          songs: [
            {
              src: '/audio/ritual/01_Ritual.webm',
              title: 'Ritual',
              artist: 'Cellarghost',
              playlist: 1
            },
            {
              src: '/audio/ritual/02_Hotel.webm',
              title: 'Hotel',
              artist: 'Cellarghost',
              playlist: 1
            },
            {
              src: '/audio/ritual/03_No_Dawn.webm',
              title: 'No Dawn',
              artist: 'Cellarghost',
              playlist: 1
            },
            {
              src: '/audio/ritual/04_Mothic.webm',
              title: 'Mothic',
              artist: 'Cellarghost',
              playlist: 1
            },
            {
              src: '/audio/ritual/05_Burial.webm',
              title: 'Burial',
              artist: 'Cellarghost',
              playlist: 1
            },
          ]
        },
        {
          id: 2,
          title: 'In The Whiteout',
          songs: [
            {
              src: '/audio/in_the_whiteout/01_La_fin_du_monde.webm',
              title: 'La fin du monde',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: '/audio/in_the_whiteout/02_vampire.webm',
              title: 'Vampire',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: '/audio/in_the_whiteout/03_Winter.webm',
              title: 'Winter',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: '/audio/in_the_whiteout/04_Cinders.webm',
              title: 'Cinders',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: '/audio/in_the_whiteout/05_Jackals.webm',
              title: 'Jackals',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: '/audio/in_the_whiteout/06_Wilderness.webm',
              title: 'Wilderness',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: '/audio/in_the_whiteout/07_Scissors.webm',
              title: 'Scissors',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: '/audio/in_the_whiteout/08_Television.webm',
              title: 'Television',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: '/audio/in_the_whiteout/09_Apothecary.webm',
              title: 'Apothecary',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: '/audio/in_the_whiteout/10_Whiteout.webm',
              title: 'Whiteout',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: '/audio/in_the_whiteout/11_Black_Money.webm',
              title: 'Black Money',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: '/audio/in_the_whiteout/12_In_The_Dark.webm',
              title: 'In the Dark',
              artist: 'Cellarghost',
              playlist: 2
            },
          ]
        }
      ]
    }
  }
}
</script>
