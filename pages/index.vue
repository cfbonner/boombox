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
              src: [
                '/audio/ritual/01_Ritual.webm',
                '/audio/ritual/01_Ritual.mp3'
              ],
              title: 'Ritual',
              artist: 'Cellarghost',
              playlist: 1
            },
            {
              src: [
                '/audio/ritual/02_Hotel.webm',
                '/audio/ritual/02_Hotel.mp3'
              ],
              title: 'Hotel',
              artist: 'Cellarghost',
              playlist: 1
            },
            {
              src: [
                '/audio/ritual/03_No_Dawn.webm',
                '/audio/ritual/03_No_Dawn.mp3'
              ],
              title: 'No Dawn',
              artist: 'Cellarghost',
              playlist: 1
            },
            {
              src: [
                '/audio/ritual/04_Mothic.webm',
                '/audio/ritual/04_Mothic.mp3'
              ],
              title: 'Mothic',
              artist: 'Cellarghost',
              playlist: 1
            },
            {
              src: [
                '/audio/ritual/05_Burial.webm',
                '/audio/ritual/05_Burial.mp3'
              ],
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
              src: [
                '/audio/in_the_whiteout/01_La_fin_du_monde.webm',
                '/audio/in_the_whiteout/01_La_fin_du_monde.mp3'
              ],
              title: 'La fin du monde',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: [
                '/audio/in_the_whiteout/02_vampire.webm',
                '/audio/in_the_whiteout/02_vampire.mp3'
              ],
              title: 'Vampire',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: [
                '/audio/in_the_whiteout/03_Winter.webm',
                '/audio/in_the_whiteout/03_Winter.mp3'
              ],
              title: 'Winter',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: [
                '/audio/in_the_whiteout/04_Cinders.webm',
                '/audio/in_the_whiteout/04_Cinders.mp3'
              ],
              title: 'Cinders',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: [
                '/audio/in_the_whiteout/05_Jackals.webm',
                '/audio/in_the_whiteout/05_Jackals.mp3'
              ],
              title: 'Jackals',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: [
                '/audio/in_the_whiteout/06_Wilderness.webm',
                '/audio/in_the_whiteout/06_Wilderness.mp3'
              ],
              title: 'Wilderness',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: [
                '/audio/in_the_whiteout/07_Scissors.webm',
                '/audio/in_the_whiteout/07_Scissors.mp3'
              ],
              title: 'Scissors',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: [
                '/audio/in_the_whiteout/08_Television.webm',
                '/audio/in_the_whiteout/08_Television.mp3'
              ],
              title: 'Television',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: [
                '/audio/in_the_whiteout/09_Apothecary.webm',
                '/audio/in_the_whiteout/09_Apothecary.mp3'
              ],
              title: 'Apothecary',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: [
                '/audio/in_the_whiteout/10_Whiteout.webm',
                '/audio/in_the_whiteout/10_Whiteout.mp3'
              ],
              title: 'Whiteout',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: [
                '/audio/in_the_whiteout/11_Black_Money.webm',
                '/audio/in_the_whiteout/11_Black_Money.mp3'
              ],
              title: 'Black Money',
              artist: 'Cellarghost',
              playlist: 2
            },
            {
              src: [
                '/audio/in_the_whiteout/12_In_The_Dark.webm',
                '/audio/in_the_whiteout/12_In_The_Dark.mp3'
              ],
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
