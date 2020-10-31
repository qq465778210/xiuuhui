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
    </div>
</template>

<script>
export default {
    name: "MusicControler",
    props: ["musicInfo"],
    data() {
        return {
            nowPlaying: this.musicInfo,
        };
    },
    model: {
        prop: "value",
    },
    created() {
        console.log(this.nowPlaying.name);
    },
    mounted() {},
    watch: {
        musicInfo() {
            this.nowPlaying = this.musicInfo;
        },
    },
    methods: {
        testAudio() {
            const audioContext = new AudioContext();
            async function play() {
                const res = await fetch("http://localhost:8080/mp3/Test01.mp3");
                const arraybuffer = await res.arrayBuffer();
                const audioBuffer = await audioContext.decodeAudioData(
                    arraybuffer
                );
                const source = audioContext.createBufferSource();
                source.connect(audioContext.destination); //连接上实例
                source.buffer = audioBuffer;
                source.start();
            }
            return play();
        },
        audioPlayer() {
            const AudioContext =
                window.AudioContext || window.webkitAudioContext;
            const audioContext = new AudioContext();
        },
        last() {
            console.log("lastClick");
            this.$emit("lastMusic");
        },
        togglePlay() {},
        next() {
            console.log("nextClick");
            this.$emit("nextMusic");
        },
    },
};
</script>

<style lang='scss' scoped>
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