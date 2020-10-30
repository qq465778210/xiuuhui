<template>
    <div class="music-icon frosted-glass">
        <div class="music-container">
            <div
                class="play-pause"
                :style="{ 'animation-play-state': animationShow }"
                @click="togglePlay"
            >
                <img src="~@/assets/img/music.png" alt="" />
                <audio
                    id="music-player"
                    src="~@/assets/mp3/Test01.mp3"
                    :autoplay="isPlaying"
                    loop
                ></audio>
            </div>
            <div class="music-menu" @click="menuBtn">
                <img src="~@/assets/img/menu.png" alt="" />
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "MusicIcon",
    data() {
        return {
            // animationShow: "running",
            // isPlaying: true,
            animationShow: "paused",
            isPlaying: false,
            isMobile: false,
        };
    },
    mounted() {
        this.userDevice();
        this.initPlay();
    },
    methods: {
        //判断设备类型
        userDevice() {
            let flag = navigator.userAgent.match(
                /(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i
            );
            this.isMobile = flag;
            console.log(this.isMobile);
        },
        // 根据设备类型初始化播放状态
        initPlay() {
            this.isMobile ? this.pauseMusic() : this.playMusic();
        },
        //点击切换播放/暂停
        togglePlay() {
            this.animationShow == "running"
                ? this.pauseMusic()
                : this.playMusic();
        },
        //播放音乐
        playMusic() {
            var audio = document.querySelector("#music-player");
            if (!this.isPlaying) {
                audio.play();
                this.isPlaying = true;
                this.animationShow = "running";
            }
        },
        // 暂停音乐
        pauseMusic() {
            var audio = document.querySelector("#music-player");
            if (this.isPlaying) {
                audio.pause();
                this.isPlaying = false;
                // audio.currentTime = 0;
                this.animationShow = "paused";
            }
        },
        //跳转到音乐详情页
        menuBtn() {
            this.$router.push("/");
        },
    },
};
</script>

<style lang='scss' scoped>
.music-icon {
    height: 4rem;
    width: 4rem;
    position: fixed;
    top: 2rem;
    right: 2rem;
    border-radius: 2rem;
    box-shadow: 0 0 5px rgb(0, 0, 0, 0.4);
    transition: all 0.5s ease;
    overflow: hidden;
    .music-menu {
        opacity: 0;
    }
}
.music-icon:hover {
    height: 8rem;
    // width: 4rem;
    box-shadow: 0 0 10px rgb(224, 51, 138, 0.2);
    .music-menu {
        opacity: 1;
    }
}
.music-container {
    height: 8rem;
    width: 4rem;
    // padding: 0 0 0 5px;
    align-items: center;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
}
.play-pause {
    border-radius: 50%;
    height: 3.5rem;
    width: 3.5rem;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    // margin: 0 2px 0 0;
    animation: logo-rotate 10s linear infinite;
    filter: drop-shadow(0 0 2px rgba(0, 0, 0, 0.5));
    img {
        height: 80%;
        width: 80%;
    }
}
.play-pause:hover {
    filter: brightness(150%) drop-shadow(0 0 4px rgba(224, 51, 138, 0.5));
}
.music-menu {
    border-radius: 50%;
    height: 3.5rem;
    width: 3.5rem;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    filter: drop-shadow(0 0 2px rgba(0, 0, 0, 0.5));
    img {
        height: 80%;
        width: 80%;
    }
}
.music-menu:hover {
    filter: brightness(150%) drop-shadow(0 0 4px rgba(224, 51, 138, 0.5));
}
.frosted-glass {
    z-index: 10;
    // position: absolute;
    overflow: hidden; // 为防止效果不超出 content 的范围
    // background: url(~@/assets/logo.png) center;
    background-size: 100%;
}
.frosted-glass::after {
    content: "";
    background: url(~@/assets/img/4dfce2edfaaaffbdc6339399cc340997.png) center
        center / cover no-repeat fixed;
    filter: blur(4px) brightness(120%);
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: -2;
    margin: -30px; //为解决元素的边缘模糊的效果减弱
}

@keyframes logo-rotate {
    0% {
        transform: rotate(0);
    }
    50% {
        transform: rotate(180deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
</style>