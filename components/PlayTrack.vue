<template>
<div>

  <p class="lead">
 <audio ref="song">
  <source src="~assets/the-entertainer.mp3" type="audio/mpeg">
</audio> 
      <v-btn @click="playPause" icon large>
          <v-icon large>{{ getIcon() }}</v-icon>
          </v-btn>
          {{ name.toLowerCase() }}
        </p>

<v-container style="max-width: 50%">
<p :style="style">Lorem ipsum dolor sit amet consectetur adipisicing elit. Unde molestias, libero praesentium quis, aliquid distinctio a ab itaque, repudiandae dolor temporibus sed officiis recusandae nostrum nesciunt eveniet asperiores neque at.
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Unde molestias, libero praesentium quis, aliquid distinctio a ab itaque, repudiandae dolor temporibus sed officiis recusandae nostrum nesciunt eveniet asperiores neque at.
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Unde molestias, libero praesentium quis, aliquid distinctio a ab itaque, repudiandae dolor temporibus sed officiis recusandae nostrum nesciunt eveniet asperiores neque at.
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Unde molestias, libero praesentium quis, aliquid distinctio a ab itaque, repudiandae dolor temporibus sed officiis recusandae nostrum nesciunt eveniet asperiores neque at.
</p>
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
        name: String,
        id: Number
    },
    methods: {
        getIcon() {
            if (this.playing) {
                return "mdi-stop";
            }
            return "mdi-play-outline";
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
                maxHeight: "0px",
                textOverflow: "clip",
                overflow: "hidden",
                fontSize: "20px",
                transitionDuration: "1s"

            }
            }
            return {
                maxHeight: "500px",
                textOverflow: "clip",
                overflow: "hidden",
                fontSize: "20px"
            }
            
        }
    }
    



}
</script>

<style scoped>

</style>