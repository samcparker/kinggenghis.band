<template>
  <div >
        <play-track ref="audioTrack" v-on:play="trackPlay" v-for="(track, index) in tracks" :key="index" :name="track.name" :playing="track.playing" :id="index"></play-track>
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
            this.$refs.audioTrack.forEach(element => {
                element.stop();
            })
        }

    },
    data: () => {
        return {
            tracks: [
                {
                    name: "mao's great famine",
                    playing: false
                },
                {
                    name: "Push, Push, Push!",
                    playing: false
                },
                {
                    name: "Welcome to Lonely The Beach",
                    playing: false
                },
                {
                    name: "Bridge Over Strong Hats",
                    playing: false
                },
                {
                    name: "Somewhere Over the Towel",
                    playing: false
                },
                {
                    name: "You Can't Giggle Through A Buffalo Herd",
                    playing: false
                },
            ]
        }
    }
}
</script>

<style>

</style>