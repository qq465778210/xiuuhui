<template>
    <div class="home">
        <music-icon></music-icon>
        <header class="header">
            <div id="top-logo">
                <img
                    src="@/assets/img/02bb004345d2c2e19ac5b247ce9e70f2.jpg"
                    alt=""
                />
            </div>
            <div id="top-title">
                <span id="title01">灰灰的个人小站</span>
                <hr />
                <span id="title02">www.xiuuhui.com</span>
            </div>
        </header>
        <nav class="navlist">
            <div><router-link to="#">MUSIC</router-link></div>
            <div><router-link to="#">MUSIC</router-link></div>
            <div><router-link to="#">MUSIC</router-link></div>
            <div><router-link to="#">MUSIC</router-link></div>
        </nav>
        <footer id="bottom-footer">
            <div>
                <hr />
                <span
                    >This is a simple website for person study, thanks NvZ make
                    the base web style for me.</span
                >
            </div>
            <div>
                <hr />
                <span
                    ><a href="http://beian.miit.gov.cn/"
                        >赣ICP备 2020011012号</a
                    ></span
                >
                <span>Copyright © 2020-2020 huihui.xiong.</span>
            </div>
            <audio autoplay="autoplay">
                <source src="@/assets/mp3/onj001.mp3" type="audio/mpeg" />
            </audio>
        </footer>
    </div>
</template>

<script>
// @ is an alias to /src
import MusicIcon from "components/common/MusicIcon";

export default {
    name: "Home",
    components: {
        MusicIcon,
    },
    data() {
        return {
            publicPath: process.env.BASE_URL,
        };
    },
};
</script>

<style lang="scss" scoped>
.home {
    width: 100%;
    height: 100%;
    padding: 100px 0 10px;
    background: url(~@/assets/img/4dfce2edfaaaffbdc6339399cc340997.png)
        no-repeat center;
    background-size: cover;
    position: fixed;
}
.header {
    width: 100vw;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-flow: column;
}
#top-logo {
    height: 30vh;
    width: 30vh;
    min-height: 100px;
    min-width: 100px;
    max-height: 200px;
    max-width: 200px;
    border-radius: 50%;
    padding: 10px;
    margin: 0 0 20px 0;
    overflow: hidden;
    background-color: rgb(255, 255, 255, 0.2);
    // display: flex;
    // justify-content: center;
    // align-items: center;
    box-shadow: 0 0 4px rgb(0, 0, 0, 0.5);
    filter: drop-shadow(0 0 4px rgb(0, 0, 0, 0.5));
    // animation: logo-rotate 10s linear infinite;
    img {
        border-radius: 50%;
        height: 100%;
        width: 100%;
    }
}
#top-title {
    // display: flex;
    // justify-content: center;
    // align-items: center;
    color: #fff;
    width: 100vw;
    margin: 0 0 20px 0;
    #title01 {
        font-family: W03;
        font-size: 36px;
    }
    hr {
        width: 70%;
        margin: 5px auto;
        border: 0;
        border-bottom: 1px solid #fff;
        border-image: linear-gradient(to right, #fff2, #ffff, #fff2) 1 8 1;
    }
    #title02 {
        font-family: W03;
        font-size: 10px;
    }
}
.navlist {
    // display: grid;
    margin: 0 0 20px 0;
    width: 30%;
    height: 220px;
    max-width: 220px;
    margin-left: auto;
    margin-right: auto;
    div {
        transition: all 0.5s ease;
        width: 100%;
        max-height: 40px;
        min-height: 10px;
        margin-top: 15px;
        text-decoration: none;
        border-radius: 2px;
        filter: drop-shadow(0 0 2px rgb(0, 0, 0, 1));
        a {
            display: block;
            width: 100%;
            line-height: 28px;
        }
    }
    div:hover {
        a {
            color: rgba(224, 51, 138, 0.5);
        }
        background-color: #fff;
    }
}
#bottom-footer {
    padding: 4px 10px;
    background-color: #04202c80;
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 12;
    div {
        color: #858585;
        font-size: 10px;
        letter-spacing: 1.5px;
        line-height: 16px;
        text-align: center;
        span {
            line-height: 24px;
            margin: 0 10px;

            a {
                color: #858585;
            }
        }
    }
    hr {
        border: 0;
        border-bottom: 1px dashed #858585;
    }
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
