<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">{{current.title}} - <span>{{ current.artist }}</span></h2>
        
       <div class="contro">
        <button class="prev" @click="prev">Prev</button>
        <button class="play" v-if="!isPlaying" @click="play">Play</button>
        <button class="pause" v-else @click="pause">Pause</button>
        <button class="next" @click="next">Next</button>
       </div>
      </section>
      <section class="playlist">
  <h3>The Playlist</h3>
  <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">
  {{ song.title }}-{{ song.artist }}</button>
</section>

    </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      current: {},
      index: 0,
      isPlaying:false,
      songs: [
        { 

          title: 'Invincible',
          artist: 'Deaf Kev',
          src: require('./assets/deaf-kev-invincible_filesgarage.mp3')


        },
        {
          
          title: 'Grateful',
          artist: 'Neffex',
          src: require('./assets/Grateful_320(PaglaSongs).mp3')

        },

        {

          title: 'Faded ncs',
          artist: 'Allen Walker',
          src: require('./assets/Alan Walker  Fade NCS Release.mp3') 


        },
        {


          title: 'Collide',
          artist: 'Elektronomia',
          src: require('./assets/Elektronomia - Collide [NCS Release].mp3') 


        },
        {

         title: 'Feel Good',
         artist: 'Syn Cole',
         src: require('./assets/Syn cole Feel Good.mp3') 


 },



      ],
      player: new Audio(),
      
    }
  },
  methods: {
  pause() {
    this.storedSong = this.current;
    this.player.pause();
    this.isPlaying = false;
  },
  play(song = this.songs[this.index]) {
  this.current = song;
  this.player.src = this.current.src;
  this.player.currentTime = 0;
  this.player.play();
  this.isPlaying = true;

  this.player.addEventListener('ended', () => {
    this.index++;
    if (this.index > this.songs.length - 1) {
      this.index = 0;
    }

    this.current = this.songs[this.index];
    this.play(this.current);
    });
  },
  prev() {
    this.index--;
    if (this.index < 0) {
      this.index = this.songs.length - 1;
    }

    this.current = this.songs[this.index];
    this.storedSong = this.current;
    this.play(this.current);
  },
  next() {
    this.index++;
    if (this.index > this.songs.length - 1) {
      this.index = 0;
    }

    this.current = this.songs[this.index];
    this.storedSong = this.current;
    this.play(this.current);
  }
},
created() {
  this.current = this.songs[this.index];
  this.player.src = this.current.src;
    
  }
}

</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  background-color:gray;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color:white;
}
main{
  width:100%;
  max-width:768px;
  margin:0 auto ;
  padding:25px;
}
.contro {
  display: flex;
  justify-content: center;
  align-items: center;
}
.song-tittle{
  font-size:32px;
  color:#53565a;
  font-weight:700;
  text-transform: uppercase;
  text-align:center;
}
.song-title span{
  font-weight:400;
  font-style:italic;
  text-align: center;
  
}
#app{text-align: center;}
.controls{
  display:flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}
button{
  appearance:none;
  background:none;
  border:none;
  outline:none;
  cursor:pointer;
}
.play, .pause{
  font-size:20px;
font-weight:700;
padding:15px 25px;
margin:0px 15px;
border-radius: 8px;
color:#fff;
background-color:#CC2e5d;
}
button:hover{opacity:0.8;}
.next, .prev{font-size:16px;
font-weight:700;
padding:10px 20px;
margin:0px 15px;
border-radius: 6px;
color:#fff;
background-color: #ff5858;

}
.playlist{ padding:0px 30px}
.playlist h3{
  color:#212121;
  font-size:28px;
  font-weight:400;
  margin-bottom:30px;
  text-align:center;
}
.playlist .song{
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor:pointer;
}
.playlist .song:hover{
  color:#ff5858;
}
.playlist .song.playing{
  color:white;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
}

</style>