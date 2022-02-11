<script>
export default {
  name: "Home",
  data: () => ({
    audio: null,
    volume: null,
    isPlayed: false,
  }),
  computed: {},
  mounted() {
    this.audio = document.getElementById("myAudio");
    this.audio.volume = 0.5;
    this.volume = document.querySelector(".volume");
    this.volume.addEventListener("mousemove", this.setVolume);
  },
  methods: {
    onPlay() {
      this.isPlayed = !this.isPlayed;

      if (this.isPlayed) {
        console.log("play");
        this.audio.play();
      } else {
        console.log("stop");
        this.audio.pause();
      }
    },
    setVolume() {
      this.audio.volume = this.volume.value / 100;
    },
    stopVideo() {
      this.audio.currentTime = 0;
      this.isPlayed = false;
      this.audio.pause();
    },
  },
};
</script>

<template>
  <main>
    <section class="player-video">
      <div class="player-video--body">
        <!-- v-show="!isPlayed" -->
        <div class="player-video--play">
          <div class="player-video--play__LOGO">
            <button @click="onPlay()" :class="{ pause: isPlayed }"></button>
            <button @click="stopVideo()" :class="{ resize: isPlayed }"></button>
          </div>
        </div>
        <!-- Volume Slider -->
        <div class="player-video--volume">
          vol:
          <input type="range" class="volume" name="volume" min="0" max="100" />
        </div>
      </div>
    </section>
  </main>
  <audio id="myAudio">
    <source
      src="../assets/audio/vince-staples-sheet-music.mp3"
      type="audio/mpeg"
    />
    Your browser does not support the audio element.
  </audio>
</template>

<style lang="scss">
.player-video {
  &--body {
    display: flex;
    font-family: "Yellowtail", cursive;
    -webkit-text-stroke: 1px white;
    height: 500px;

    margin-top: 50px;
    gap: 20px;
    z-index: 99;
    background-color: #2d636c;
  }

  &--play {
    align-self: center;
    &__LOGO {
      display: flex;
      justify-content: center;
      width: 100%;
      position: absolute;
      vertical-align: middle;

      button:last-child {
        width: 74px;
        height: 74px;
        border-style: solid;
        border-width: 37px;
        border-color: #ffffff;
        background-color: #ffffff;
        .resize {
          width: 20px;
          height: 20px;
        }
      }

      button {
        box-sizing: border-box;
        height: 74px;
        background-color: #2d636c;
        border-color: transparent transparent transparent #ffffff;
        transition: 100ms all ease;
        will-change: border-width;
        cursor: pointer;

        // play state
        border-style: solid;
        border-width: 37px 0 37px 60px;

        // paused state
        .pause {
          border-style: double;
          border-width: 0px 0 0px 60px;
        }
      }
    }
  }

  &--volume {
    align-self: end;
  }
}
</style>
