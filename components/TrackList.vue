<template>
  <div>
      <play-track ref="audioTrack" v-on:play="trackPlay" v-for="(track, index) in tracks" :key="index" :doc="track" :playing="false" :id="index"></play-track>
  </div>
</template>

<script>
import PlayTrack from '@/components/PlayTrack.vue';

export default {

    components: {
        PlayTrack
    },
    methods: {
        trackPlay: function (id) {
            console.log(id);
            id = id % this.$refs.audioTrack.length;
            this.$refs.audioTrack.forEach(element => {
                element.stop();
                console.log(element.id);
                if (element.id == id) {
                    element.play();
                }
            });
            // this.$refs.audioTrack.forEach(element => {
            //     element.stop();
                
            //     if (id == element.getId()) {
            //         element.play();
            //     }
            // })
        }

    },
    props: {
        tracks: Array
    },
    // data: () => {
    //     return {
    //         tracks: [
    //             {
    //                 name: "mao's great famine",
    //                 playing: false
    //             },
    //             {
    //                 name: "Song Name 1",
    //                 playing: false
    //             },
    //             {
    //                 name: "Welcome to Lonely The Beach",
    //                 playing: false
    //             },
    //             {
    //                 name: "Bridge Over Strong Hats",
    //                 playing: false
    //             },
    //             {
    //                 name: "Somewhere Over the Towel",
    //                 playing: false
    //             },
    //             {
    //                 name: "You Can't Giggle Through A Buffalo Herd",
    //                 playing: false
    //             },
    //         ]
    //     }
    // }
}
</script>

<style>

</style>