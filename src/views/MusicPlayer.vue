<template>
    <div class="music-player">
        <h2>Music Player</h2>
        <button @click="testAudio()">播放</button>
    </div>
</template>

<script>
export default {
    name: "MusicPlayer",
    data() {
        return {};
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
    },
};
</script>

<style lang='scss' scoped>
</style>