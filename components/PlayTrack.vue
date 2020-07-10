<template>
<div>

  <p class="lead" style="font-size: 30px">
 <audio ref="song">
  <source :src="doc.src" type="audio/mpeg">
</audio> 
      <v-btn @click="playPause" icon large>
          <v-icon large>{{ getIcon() }}</v-icon>
          </v-btn>
          {{ doc.trackNumber + ". " + doc.name.toLowerCase() }}
        </p>

<v-container style="max-width: 1000px">
<div :style="style" ref="lyrics" class="mb-4">
    <nuxt-content class="" :document="doc"/>
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
        doc: Object,
        id: Number
    },
    mounted () {
        this.$nextTick(() => {
            this.$refs.song.addEventListener("ended", (event) => {
                this.$emit('play', this.id + 1);
            });
        });
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
            }
            else {
                this.stop();
            }
        },
        stop() {
            this.playing = false;
            this.$refs.song.pause();
            this.$refs.song.currentTime = 0;
            this.$refs.lyrics.scrollTop = 0;
        },
        play() {
            this.playing = true;
            this.$refs.song.play();
        },
        getId() {
            return this.$props.doc.id;
        }
    },
    computed: {
        style() {
            if (!this.playing) {
                return {
                    color: "white",
                    opacity: 0,
                maxHeight: "0px",
                textOverflow: "clip",
                overflowY: "scroll", 
                maxWidth: "100%",
                fontSize: "10px",
                transitionDuration: "1s",

                }
            }
            return {
                opacity: 1,
                color: "white",
                maxHeight: "500px",
                textOverflow: "clip",
                overflowY: "scroll", 
                fontSize: "10px",
                transitionDuration: "1s"
            }
            
        }
    }
    



}
</script>

<style>
.nuxt-content p {
    color: white;
    font-size: 20px;
    margin-bottom: 0px;
}


</style>