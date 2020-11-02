<template>
    <div id="music-controler">
        <div id="progress-bar"></div>
        <div class="music-controler-container">
            <div id="music-info">
                <div id="music-cover"></div>
                <div id="music-name">{{ nowPlaying.name }}</div>
            </div>
            <div id="music-control">
                <!-- <div id="play-mode" @click="playMode">顺序</div> -->
                <div id="last" @click="last">上一首</div>
                <div id="play-pause" @click="togglePlay">播放/暂停</div>
                <div id="next" @click="next">下一首</div>
                <!-- <div id="volume" @click="volume">音量</div> -->
            </div>
        </div>
        <div id="getStatus" @click="getStatus">获取音频状态</div>
        <!-- <div>{{ nowPlaying }}</div>
        <div>{{ status }}</div> -->
    </div>
</template>

<script>
import audio from "@/assets/js/audio.js";

const audioCtx = new audio.AudioContext();
let audioCtxSource;

let test = 0;
function testFunc() {
    //  setTimeout(() => {
    test = 1;
    // }, 0);
    // return;
}
testFunc();
console.log(test);

export default {
    name: "MusicControler",
    props: ["musicInfo"],
    data() {
        return {
            nowPlaying: this.musicInfo,
            status: "",
        };
    },
    created() {
        console.log(this.nowPlaying.name);
        // const AudioContext = window.AudioContext || window.webkitAudioContext;
        // this.audioContext = new AudioContext();
    },
    mounted() {
        // audio.text();
        // console.log(audio.audioContext);
        // console.log(this.audioContext);
        this.initAudio()
            .then((result) => {
                console.log(result);
                result.start();
            })
            .catch((err) => {
                console.log("获取歌曲失败");
            });
    },
    updated() {
        console.log(this.nowPlaying.path);
    },
    watch: {
        musicInfo() {
            this.nowPlaying = this.musicInfo;
        },
    },
    methods: {
        getStatus() {
            this.status = audioCtx.state;
        },
        async initAudio() {
            console.log(audioCtx);
            let path = `http://localhost:8080${this.nowPlaying.path}`;
            // async function getData() {
            //     try {
            //         console.log("获取成功");
            //         const res = await fetch(path);
            //         return res;
            //     } catch (err) {
            //         console.log("获取失败" + err);
            //     }
            // }

            const res = await fetch(path);
            const arraybuffer = await res.arrayBuffer();
            const audioBuffer = await audioCtx.decodeAudioData(arraybuffer);
            const source = audioCtx.createBufferSource();

            // const gainNode = audioCtx.createGain();
            // source.connect(gainNode);
            // gainNode.gain.value = 0.1;//音量调节

            source.connect(audioCtx.destination); //连接上实例
            source.buffer = audioBuffer;
            audioCtxSource = source;

            return source;
        },
        audioPlayer() {
            // const AudioContext =
            //     window.AudioContext || window.webkitAudioContext;
            if (audioContext.state === "closed") {
                const audioContext = new AudioContext();
            }
        },
        last() {
            console.log("lastClick");
            this.$emit("lastMusic");
        },
        togglePlay() {
            // audio.text();
            console.log(audioCtx.state);
            // if (audioCtx.state === "running") {
            //     audioCtx.suspend().then(function () {
            //         // susresBtn.textContent = "Resume context";
            //         console.log("暂停音乐");
            //         console.log(audioCtx.state);
            //     });
            // } else if (audioCtx.state === "suspended") {
            //     audioCtx.resume().then(function () {
            //         // susresBtn.textContent = "Suspend context";
            //         console.log("恢复音乐");
            //         console.log(audioCtx.state);
            //     });
            // } else {
            // this.initAudio()
            //     .then((result) => {
            //         console.log(result);
            //         result.start();
            //     })
            //     .catch((err) => {
            //         console.log("获取歌曲失败");
            //     });
            // audioCtxSource && audioCtxSource.start();
            // }
        },
        next() {
            console.log("nextClick");
            this.$emit("nextMusic");
            // audioCtxSource.start();
            // console.log(audioCtxSource.start);
        },
    },
};
</script>

<style lang='scss' scoped>
#getStatus:hover {
    text-shadow: 0 0 2px #fff8;
    background-color: #fff2;
}
.music-controler-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    // padding: 0 20%;
    div {
        overflow: hidden;
        height: 40px;
        line-height: 40px;
        text-shadow: 0 0 4px #0008;
    }
}
#music-info {
    display: grid;
    grid-template-columns: 1fr 4fr;
    padding: 0 0 0 0;
    div {
        transition: all 0.5s ease;
    }
    div:hover {
        text-shadow: 0 0 2px #fff8;
        background-color: #fff2;
    }
}
// #music-name {
//     transition: all 0.5s ease;
// }
#music-control {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    padding: 0 20%;
    grid-column-gap: 20px;
    div {
        transition: all 0.5s ease;
    }
    div:hover {
        text-shadow: 0 0 2px #fff8;
        background-color: #fff2;
    }
}
#last {
    cursor: pointer;
}
#play-pause {
    cursor: pointer;
}
#next {
    cursor: pointer;
}
</style>