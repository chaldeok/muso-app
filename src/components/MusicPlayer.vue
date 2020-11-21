<template>
  <div class="container">
    <header>
      <h1>My music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">{{ current.title }} – <span>{{ current.artist}}</span></h2>
        <div class="controls">
          <button class="prev" v-on:click="prev">Prev</button>
          <button class="play"
                  v-if="!isPlaying"
                  v-on:click="play">Play</button>
          <button class="pause"
                  v-else
                  v-on:click="pause">Pause</button>
          <button class="next" v-on:click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <button v-bind:key="song.src"
                v-for="song in songs"
                v-on:click="play(song)"
                v-bind:class="(song.src === current.src) ? 'song songIsPlaying' : 'song' ">{{ song.title }} - {{ song.artist }}</button>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: 'MusicPlayer',
  data () {
    return {
      isPlaying: false,
      current: {},
      index: 0,
      songs: [
        {
          title: 'I Resign',
          artist: 'Susan Sundorf',
          src: require('../assets/Susanne Sundfør - I Resign.mp3'),
          index: 0
        },
        {
          title: 'Morocco',
          artist: 'Susan Sundorf',
          src: require('../assets/Susanne Sundfør - Morocco.mp3'),
          index: 1
        },
        {
          title: 'Walls',
          artist: 'Susan Sundorf',
          src: require('../assets/Susanne Sundfør - Walls.mp3'),
          index: 2
        },
        {
          title: 'Always Where I Need To Be',
          artist: 'The Kooks',
          src: require('../assets/The Kooks - Always Where I Need To Be.mp3'),
          index: 3
        },
        {
          title: 'Be Who You Are',
          artist: 'The Kooks',
          src: require('../assets/The Kooks - Be Who You Are.mp3'),
          index: 4
        },
        {
          title: 'See The Sun',
          artist: 'The Kooks',
          src: require('../assets/The Kooks - See The Sun.mp3'),
          index: 5
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play (song) {
      if (typeof song.src !== 'undefined') {
        this.current = song
        this.player.src = this.current.src
        this.index = song.index
      }
      this.player.play()
      this.player.addEventListener('ended', function () {
        this.index++
        if (this.index > this.songs.length - 1) {
          this.index = 0
        }
        this.current = this.songs[this.index]
        this.play(this.current)
      }.bind(this))

      console.log(this.index)
      this.isPlaying = true
    },
    pause () {
      this.player.pause()
      this.isPlaying = false
    },
    prev () {
      this.index--
      if (this.index < 0) {
        this.index = this.songs.length - 1
      }
      this.current = this.songs[this.index]
      this.play(this.current)
    },
    next () {
      this.index++
      if (this.index > this.songs.length - 1) {
        this.index = 0
      }
      this.current = this.songs[this.index]
      this.play(this.current)
    }
  },
  created () {
    this.current = this.songs[this.index] // назначаю свойству с именем current значение из массива songs
    this.player.src = this.current.src
    this.player.play()
  }
}
</script>

<style lang="scss" scoped>

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  header {
    padding: 10px;
    background-color: #ba68c8;
    color: whitesmoke;
  }
  main {
    padding: 25px;
  }
  h2, .controls {
    margin-bottom: 25px;
  }
  .controls {
    display: flex;
    display: -o-flex;
    display: -moz-flex;
    display: -webkit-flex;
    justify-content: center;
    align-items: center;
    padding: 5px;
  }
  button {
    appearance: none;
    background: none;
    border: none;
    outline: none;
    cursor: pointer;
    padding: 10px;
    transition: opacity .5s ease;
  }
  button:hover {
    opacity: .7;
  }
  .play, .pause {
    font-size: 20px;
    border-radius: 6px;
    background-color: #ec407a;
    color: whitesmoke;
    margin: 0 15px;
    padding: 13px;
  }
  .next, .prev {
    font-size: 16px;
    border-radius: 6px;
    background-color: #ba68c8;
    color: whitesmoke;
  }
  .playlist {
    max-width: 400px;
    margin: 0 auto;
    .song {
      display: block;
      width: 100%;
      padding: 10px;
    }
    .song.songIsPlaying {
      color: whitesmoke;
      background-image: linear-gradient(to right, #ef6c00, #ffa726);
    }
  }
</style>
