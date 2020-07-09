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

             <h1 class="hidden-sm-and-up xs">{{ getTitle }}</h1>
             <h1 class="hidden-xs-only">{{ getTitle }}</h1>

             <div class="mt-10">
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
      chars: "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890!\"£$%^&*()@'#~;:><.,?`¬¥¢¡¤¶ µ¼½¾",
      finished: false,
      titles: ["King Genghis", "Genghis King", "Ging Kenghis"]
    }
  },
  computed: {
    getTitle() {
      return this.currentTitle;      
    },
  
  },
  methods: {
    updateText() {

      for (var i = 0; i < this.currentTitle.length; i++) {
        var rand = Math.random() * 1000;
        if (rand > 995) {
          this.currentTitle = this.currentTitle.substring(0, i) + String.fromCharCode(Math.floor(Math.random() * 5000 + 200)) + this.currentTitle.substring(i + 1);
        }
        else if (rand > 900) {
          // console.log(this.currentTitle);
          this.currentTitle = this.currentTitle.substring(0, i) + this.title[i] + this.currentTitle.substring(i + 1);
        }
        else if (this.currentTitle[i] != this.title[i]) {
          // this.currentTitle = this.currentTitle.substring(0, i) + this.chars[Math.floor(Math.random() * this.chars.length)] + this.currentTitle.substring(i + 1);
          this.currentTitle = this.currentTitle.substring(0, i) + String.fromCharCode(Math.floor(Math.random() * 5000 + 200)) + this.currentTitle.substring(i + 1);
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
          this.updateText() ;
}, 100);
  var selected = 0;
setInterval(() => {
  this.title = this.titles[selected];
  selected ++;
  selected = selected % this.titles.length;
}, 10000);
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
.xs {
  font-size: 95px;

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
