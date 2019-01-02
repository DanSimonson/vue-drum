
<template>
  <div class="home">
    <div id="drum-machine">
      <h1 class="clear-text">{{title}}</h1>
      <div id="soundboard">
        <div id="keyContainer">
          <div
            class="drum-pad"
            v-for="k in keys"
            :key="k.keyCode"
            :id="k.keyCode"
            @click="playMe(k.keyCode, k.soundName)"
          >
            <audio class="clip" :src="k.audio" :id="letter(k.keyCode).toUpperCase()"></audio>
            <span>{{k.keyName}}</span>
          </div>
        </div>
        <div id="display">{{display}}</div>
      </div>
      <Footer/>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
//@ is an alias to /src
//import HelloWorld from "@/components/HelloWorld.vue";
import Footer from "@/components/Footer.vue";
export default {
  name: "home",
  components: {
    //HelloWorld
    Footer
  },
  data() {
    return {
      title: "Drum Machine",
      display: "Sound",
      keys: [
        {
          keyCode: 81,
          keyName: "Q",
          soundName: "clap",
          audio: new Audio(
            "https://res.cloudinary.com/dmglopmul/video/upload/v1546375973/projectPhotos/vue-sounds/clap.wav"
          )
        },
        {
          keyCode: 87,
          keyName: "W",
          soundName: "hihat",
          audio: new Audio(
            "https://res.cloudinary.com/dmglopmul/video/upload/v1546375990/projectPhotos/vue-sounds/hihat.wav"
          )
        },
        {
          keyCode: 69,
          keyName: "E",
          soundName: "kick",
          audio: new Audio(
            "https://res.cloudinary.com/dmglopmul/video/upload/v1546375999/projectPhotos/vue-sounds/kick.wav"
          )
        },
        {
          keyCode: 65,
          keyName: "A",
          soundName: "openhat",
          audio: new Audio(
            "https://res.cloudinary.com/dmglopmul/video/upload/v1546376070/projectPhotos/vue-sounds/openhat.wav"
          )
        },
        {
          keyCode: 83,
          keyName: "S",
          soundName: "boom",
          audio: new Audio(
            "https://res.cloudinary.com/dmglopmul/video/upload/v1546375952/projectPhotos/vue-sounds/boom.wav"
          )
        },
        {
          keyCode: 68,
          keyName: "D",
          soundName: "ride",
          audio: new Audio(
            "https://res.cloudinary.com/dmglopmul/video/upload/v1546376078/projectPhotos/vue-sounds/ride.wav"
          )
        },
        {
          keyCode: 90,
          keyName: "Z",
          soundName: "snare",
          audio: new Audio(
            "https://res.cloudinary.com/dmglopmul/video/upload/v1546376089/projectPhotos/vue-sounds/snare.wav"
          )
        },
        {
          keyCode: 88,
          keyName: "X",
          soundName: "tom",
          audio: new Audio(
            "https://res.cloudinary.com/dmglopmul/video/upload/v1546376112/projectPhotos/vue-sounds/tom.wav"
          )
        },
        {
          keyCode: 67,
          keyName: "C",
          soundName: "tink",
          audio: new Audio(
            "https://res.cloudinary.com/dmglopmul/video/upload/v1546376102/projectPhotos/vue-sounds/tink.wav"
          )
        }
      ]
    };
  },
  methods: {
    letter: key => {
      return String.fromCharCode(key);
    },
    playMe: function(keyCode, keyName) {
      const key = this.keys.find(key => {
        return key.keyCode === keyCode;
      });
      console.log(key);
      key.audio.currentTime = 0;
      key.audio.play();
      let displayMe = document.getElementById("display");
      displayMe.textContent = keyName;
    },
    playSound: function(e) {
      const key = this.keys.find(key => {
        return key.keyCode === e.keyCode;
      });
      key.audio.currentTime = 0;
      //e.target.firstElementChild.play();
      key.audio.play();
      let soundName = "";
      switch (e.keyCode) {
        case 81:
          soundName = "clap";
          break;
        case 87:
          soundName = "hihat";
          break;
        case 69:
          soundName = "kick";
          break;
        case 65:
          soundName = "openhat";
          break;
        case 83:
          soundName = "boom";
          break;
        case 68:
          soundName = "ride";
          break;
        case 90:
          soundName = "snare";
          break;
        case 88:
          soundName = "tom";
          break;
        case 67:
          soundName = "tink";
          break;
        default:
          soundName = "no valid name";
      }
      let displayMe = document.getElementById("display");
      displayMe.textContent = soundName;
    }
  },
  mounted() {
    window.addEventListener("keydown", this.playSound);
  }
};
</script>
<style scoped lang='scss'>
@import "../../public/styles.scss";
#drum-machine {
  display: flex;
  flex-direction: column;
  align-content: center;
  text-align: center;
  vertical-align: center;
  color: $Red;
}

#soundboard {
  display: flex;
  flex-direction: row;
  max-width: 600px;
  margin: 0 auto;
  background: rgba(0, 0, 0, 0.3);
  border-radius: 10px;
  border: 1px solid #888;
  box-shadow: -5px -5px #888;
}
#keyContainer {
  /*width: 400px;*/
  max-width: 400px;
  margin: 0 -15px;
  /*border: 5px solid green;*/
}
.drum-pad {
  border: 1px solid $Red;
  border-radius: 10px;
  cursor: pointer;
  width: 85px;
  height: 85px;
  margin: 10px;
  display: inline-block;
  position: relative;
  transition: all 0.5s ease-out;
}
.drum-pad:hover {
  background: $White;
  color: black;
}
.drum-pad:active {
  background: $Blue;
  color: black;
}
.drum-pad > span {
  font-size: 2.4rem;
  font-weight: 400;
  display: block;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.clear-text {
  font-family: "Ubuntu", sans-serif;
  color: #999;
  background-color: #91877b;
  background: rgba(0, 0, 0, 0.3);
  text-shadow: 0 1px 0 rgba(255, 255, 255, 0.8);
  border-radius: 10px;
  border: 1px solid #888;
  margin: 15px auto;
  border-radius: 4px;
  padding: 10px;
}

.playing {
  transform: scale(1.1);
  border-color: #ffc600;
  box-shadow: 0 0 1rem #ffc600;
}

@media (min-width: 590px) {
  #display {
    display: flex;
    width: 200px;
    flex-direction: column;
    justify-content: center;
    align-content: center;
    font-size: 2.5rem;
  }
}
@media (max-width: 590px) {
  .drum-pad > span {
    font-size: 1rem;
  }
  .drum-pad {
    width: 45px;
    height: 45px;
  }

  #display {
    width: 50%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
    font-size: 2rem;
    margin: 0 5px 0 5px;
  }
}
/* javascript 30*/
.keys {
  display: flex;
  flex: 1;
  min-height: 100vh;
  align-items: center;
  justify-content: center;
}

.key {
  border: 0.4rem solid black;
  border-radius: 0.5rem;
  margin: 1rem;
  font-size: 1.5rem;
  padding: 1rem 0.5rem;
  transition: all 0.07s ease;
  width: 10rem;
  text-align: center;
  color: white;
  background: rgba(0, 0, 0, 0.4);
  text-shadow: 0 0 0.5rem black;
}

.playing {
  transform: scale(1.1);
  border-color: #ffc600;
  box-shadow: 0 0 1rem #ffc600;
}

kbd {
  display: block;
  font-size: 4rem;
}

.sound {
  font-size: 1.2rem;
  text-transform: uppercase;
  letter-spacing: 0.1rem;
  color: #ffc600;
}
</style>
