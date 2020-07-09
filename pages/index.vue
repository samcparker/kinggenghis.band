<template>
<div>
    <video autoplay muted loop id="myVideo">
    <source src="~/assets/bg-video.mp4" type="video/mp4">
</video>


    <v-container fill-height fluid class="content text-center">
      <v-row 
      class="vrow"
      justify="center"
      align="center"
      style="height: 100%;" >
          <v-col height="100">
             <h1 :style="style">{{ getTitle }}</h1>
             <div>
                
                <!-- <p class="lead" :style="pstyle"><v-btn icon><v-icon large>mdi-play</v-icon></v-btn> other song</p>
                <p class="lead" :style="pstyle"><v-btn icon><v-icon large>mdi-play</v-icon></v-btn> other song</p>
                <p class="lead" :style="pstyle"><v-btn icon><v-icon large>mdi-play</v-icon></v-btn> other song</p>
                <p class="lead" :style="pstyle"><v-btn icon><v-icon large>mdi-play</v-icon></v-btn> other song</p>
                <p class="lead" :style="pstyle"><v-btn icon><v-icon large>mdi-play</v-icon></v-btn> other song</p> -->
                  <track-list></track-list>
               </div>
              
             </v-col>
          
      </v-row>
       
    </v-container>

</div>
</template>

<script>
import TrackList from '@/components/TrackList.vue';
export default {

  components: {
    TrackList
  },
  data: () => {
    return {
      title: "King Genghis",
      currentTitle: "",
      chars: "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890!\"£$%^&*()",
      finished: false
    }
  },
  computed: {
    getTitle() {
      return this.currentTitle;      
    },
    style() {
      if (this.finished) {
      return {
        color: "white",
      }
      }
      return {
        transitionDuration: "1s",
        color: "white",
      }

    },
    
    pstyle() {
      if (this.finished) {
      return {
        opacity: 1,
        fontSize: "40px"
      }
      }
      return {
        transitionDuration: "1s",
        opacity: 0,
        fontSize: "0px"
      }
    }
  },
  methods: {
    updateText() {

      for (var i = 0; i < this.currentTitle.length; i++) {
        if (Math.random() * 100 > 96) {
          // console.log(this.currentTitle);
          this.currentTitle = this.currentTitle.substring(0, i) + this.title[i] + this.currentTitle.substring(i + 1);
        }
        else if (this.currentTitle[i] != this.title[i]) {
          this.currentTitle = this.currentTitle.substring(0, i) + this.chars[Math.floor(Math.random() * this.chars.length)] + this.currentTitle.substring(i + 1);
        }

 
      }
    }
  },
  mounted: function () {
    this.$nextTick(function () {
                 this.currentTitle = "";
        for (var i = 0; i < this.title.length; i++) {
          this.currentTitle += this.chars[Math.floor(Math.random() * this.chars.length)];
        }
      // setTimeout(() => { 
      //   this.currentTitle = "poop"; 
      //   console.log(this.currentTitle)
      //   }, 3000);
      setInterval(() => { 
        if (this.title != this.currentTitle)  {
          this.updateText() ;
        } else {
          setTimeout(() => {this.finished = true}, 300)
        }}, 70);
    })
  }
}
</script>

<style>
p { 
  font-family: 'Courier New', Courier, monospace;
  font-size: 30px;
  transition-duration: 1s; 
  }

.vrow {
  transition-duration: 1s;
}
h1 {
  font-family: 'Courier New', Courier, monospace;
  font-size: 100px;
  transition-duration: 1s;
}
#myVideo {
  position: fixed;
  right:0;
  bottom: 0;
  min-width: 100%;
  min-height: 100%;
}

/* Add some content at the bottom of the video/page */
.content {
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  color: #f1f1f1;
  width: 100%;
  min-height: 100%;
  padding: 20px;
  overflow-y: auto;
}
</style>
