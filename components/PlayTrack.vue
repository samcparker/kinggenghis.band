<template>
  <p class="lead">
 <audio ref="song">
  <source src="~assets/the-entertainer.mp3" type="audio/mpeg">
</audio> 
      <v-btn @click="playPause" icon large>
          <v-icon large>{{ getIcon() }}</v-icon>
          </v-btn>
          {{ name.toLowerCase() }}
        </p>
</template>

<script>
export default {
    data: () => {
        return {
            playing: false
        }
    },
    props: {
        name: String,
        id: Number
    },
    methods: {
        getIcon() {
            if (this.playing) {
                return "mdi-stop";
            }
            return "mdi-play";
        },
        playPause() {
            
            
            if (this.$refs.song.paused) {
                this.$emit('play', this.id);
                this.playing = true;
                this.$refs.song.play();
            }
            else {
                console.log("stop playing!")
                this.playing = false;
                this.$refs.song.pause();
                this.$refs.song.currentTime = 0;
            }

            
            
        },
        stop() {
            this.playing = false;
            this.$refs.song.pause();
        }
    },
    



}
</script>

<style>

</style>