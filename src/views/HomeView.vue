<template>
    <div>
        <video autoplay muted loop id="background-video">
            <source src="@/assets/1be08bcd62b8d137e75589e8a3e9fe28.mp4" type="video/mp4">
        </video>
        <div class="overlay">
            <h1>专属菜谱生成器</h1>
            <p>Welcome to Our Site!</p>
        </div>

        <div class="button1">
            <button @click="goToLink">开始生成</button>
        </div>

        <div id="link">
            <router-link to="/about">关于我们</router-link><br>
            <router-link to="/resource">关于声明</router-link>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        goToLink() {
            this.$router.push('/function'); // Assuming you have a route named 'generate'
        }
    }
}
</script>

<style scoped>
body, html {
    height: 100%;
    margin: 0;
    overflow: hidden;  /* 防止滚动条 */
}

#background-video {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1; /* 视频在背景层 */
    object-fit: cover; /* 确保视频覆盖整个屏幕 */
}

.overlay {
    position: relative;
    z-index: 1; /* 确保在视频之上 */
    text-align: center;
    top: 50%;
    transform: translateY(-95%); /* 垂直居中 */
    color: #ff7300; /* 文本颜色 */
    font-size: 50px;
}

.button1 {
    line-height: 20px; /* 文本垂直居中 */
    position: relative;
    z-index: 1; /* 确保在视频之上 */
    top: 26%;
    transform: translateY(-80%);
    text-align: center;
}

button {
    background-color: #ff7300;
    padding: 20px 20px;
    font-size: 50px;
    cursor: pointer;
    border: none;
    border-radius: 5px;
    transition: background-color 0.3s ease;
}

button:hover {
    background-color: #ff9500;
    color: red;
}

#link {
    z-index: 2;
    position: fixed;
    top: 10px;
    left: 20px;
    font-size: 12px;
}

a {
    color: #ff7300;
    transition: color 0.3s ease;
}

a:hover {
    color: rgb(220, 48, 0);
}

a:active {
    color: aqua;
}
</style>