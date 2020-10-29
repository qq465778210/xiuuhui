<template>
    <div class="music-icon frosted-glass">
        <div class="play-pause">
            <img src="~@/assets/img/music.png" alt="" />
        </div>
        <div class="music-menu"></div>
    </div>
</template>

<script>
export default {
    name: "MusicIcon",
};
</script>

<style lang='scss' scoped>
.music-icon {
    height: 3rem;
    width: 3rem;
    position: fixed;
    top: 2rem;
    right: 2rem;
    border-radius: 50%;
    box-shadow: 0 0 10px rgb(0, 0, 0, 0.4);
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
    filter: blur(4px) brightness(90%);
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: -1;
    margin: -30px; //为解决元素的边缘模糊的效果减弱
}
</style>