<template>
<div>

  <p class="lead">
 <audio ref="song">
  <source src="~assets/the-entertainer.mp3" type="audio/mpeg">
</audio> 
      <v-btn @click="playPause" icon large>
          <v-icon large>{{ getIcon() }}</v-icon>
          </v-btn>
          {{ doc.name.toLowerCase() }}
        </p>

<v-container style="max-width: 1000px">
<div :style="style"><nuxt-content :document="doc"/>
</div>
</v-container>
        
</div>
</template>

<script>
export default {
    data: () => {
        return {
            playing: false
        }
    },
    props: {
        doc: Object
    },
    methods: {
        getIcon() {
            if (this.$refs.song && this.$refs.song.waiting) { // included to show loading symbol if song is loading but not sure if works
                return "mdi-loading";
            }
            if (this.playing) {
                return "mdi-stop";
            }
            if (!this.playing) {
                return "mdi-play-outline";
            }
            
            
        },
        playPause() {
            if (this.$refs.song.paused) {
                this.$emit('play', this.id);
                this.playing = true;
                this.$refs.song.play();
                this.$refs.song.currentTime = 0;
            }
            else {
                this.stop();
            }

            
            
        },
        stop() {
            this.playing = false;
            this.$refs.song.pause();
            this.$refs.song.currentTime = 0;
        }
    },
    computed: {
        style() {
            if (!this.playing) {
                return {
                    color: "red",
                maxHeight: "0px",
                textOverflow: "clip",
                overflow: "scroll", 
                
                fontSize: "10px",
                transitionDuration: "1s"

                }
            }
            return {
                color: "red",
                maxHeight: "500px",
                textOverflow: "clip",
                overflow: "scroll", 
                fontSize: "10px"
            }
            
        }
    }
    



}
</script>

<style scoped>
.nuxt-content {
    font-size: 10px;
}
</style>