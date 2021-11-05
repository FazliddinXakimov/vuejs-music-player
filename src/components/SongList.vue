<template>
  <div v-if="!isPlayerVisible">
    <div class="text-yellow-300 font-bold text-center text-3xl mb-7 mt-3">
      VueJS Music App
      <i class="fas fa-music"></i>
    </div>
    <div
      v-for="(song, songIndex) in list"
      v-bind:key="song.id"
      class="flex flex-row justify-between mb-4 cursor-pointer"
      v-on:click="playSong(songIndex)"
    >
      <div>
        <span class="text-yellow-300">{{ song.name }}</span>
        <br />
        <span class="text-gray-200 text-xs">
          {{ song.artistName }} -
          <span class="text-gray-400">
            {{ song.albumName }} ({{ song.year }})</span
          >
        </span>
      </div>
      <div>
        <img class="max-h-12 rounded" v-bind:src="song.src" />
      </div>
    </div>
  </div>
  <div v-if="isPlayerVisible">
    <SongPlayer
      v-bind:song="list[currentSongIndex]"
      @goback="isPlayerVisible = !isPlayerVisible"
      @next="playNext"
      @previous="playPrevious"
    />
  </div>
</template>

<script>
import SongPlayer from "./SongPlayer.vue";

export default {
  data() {
    return {
      isPlayerVisible: false,
      currentSongIndex: 0,
      list: [
        {
          id: 1,
          name: "Siz yo'qsiz Rasululloh(S.A.V)",
          artistName: "Abror Muxtor, Humoyun Mirzo",
          albumName: "Ummat",
          year: 2021,
          src: `https://firebasestorage.googleapis.com/v0/b/car-service-adf49.appspot.com/o/MusicApp%2FHumoyun%20Mirzo.jpg?alt=media&token=c99523a3-3c0b-4224-be68-c21c941414c9`,
          songSrc: `https://firebasestorage.googleapis.com/v0/b/car-service-adf49.appspot.com/o/MusicApp%2FHumoyun%20Mirzo.mp3?alt=media&token=86c1f1cf-e2c5-4e3b-996d-e46b11261e54`,
        },
        {
          id: 2,
          name: "Assalamu alayka",
          artistName: "Izzat Shukurov",
          albumName: "Ummat",
          year: 2021,
          src: `https://firebasestorage.googleapis.com/v0/b/car-service-adf49.appspot.com/o/MusicApp%2Fizzat%20shukurov.jpg?alt=media&token=7152cc6c-528f-4a82-9f5a-e4e85d7d208c`,
          songSrc: `https://firebasestorage.googleapis.com/v0/b/car-service-adf49.appspot.com/o/MusicApp%2FIzzat%20Shukurov%20-%20Assalamu%20Alayka%20(Music%202021).mp3?alt=media&token=66578346-bb99-40af-92da-186435c893af`,
        },
        {
          id: 3,
          name: "Kim tanisa Rasulullohni(S.A.V)",
          artistName: "Iqbol Muhammad",
          albumName: "Ummat",
          year: 2019,
          src: `https://firebasestorage.googleapis.com/v0/b/car-service-adf49.appspot.com/o/MusicApp%2Fiqbol_mirzo.jpg?alt=media&token=3dfdeb14-70f4-4aeb-bace-b413836c8b98`,
          songSrc: `https://firebasestorage.googleapis.com/v0/b/car-service-adf49.appspot.com/o/MusicApp%2FKim%20tanisa%20Rasulullohni%20(S.A.V)%20(Www.Quvonch.Com)%20%20%20Iqbol%20Mu.mp3?alt=media&token=9b3a17ae-0394-4a90-8f31-0d56d0208370`,
        },
      ],
    };
  },
  methods: {
    playSong(index) {
      this.currentSongIndex = index;
      this.isPlayerVisible = true;
    },
    playNext() {
      if (this.currentSongIndex < this.list.length - 1) {
        this.currentSongIndex += 1;
      } else {
        this.currentSongIndex = 0;
      }
    },
    playPrevious() {
      if (this.currentSongIndex != 0) {
        this.currentSongIndex -= 1;
      } else {
        this.currentSongIndex = this.list.length - 1;
      }
    },
  },
  components: {
    SongPlayer,
  },
  name: "SongList",
};
</script>
