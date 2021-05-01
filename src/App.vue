<template>
  <div id="app">
        <vue-particles
        color="#ffffff"
        :particleOpacity="0.7"
        linesColor="#ffffff"
        :particlesNumber="80"
        shapeType="circle"
        :particleSize="5"
        :linesWidth="2"
        :lineLinked="true"
        :lineOpacity="0.4"
        :linesDistance="150"
        :moveSpeed="3"
        :hoverEffect="true"
        hoverMode="grab"
        :clickEffect="true"
        clickMode="push"
      >
      </vue-particles>
      <div >
        <h1 class="title" style="position: relative;">Comment System</h1>
        <input type="button" class="btn" v-on:click="clickLoad">
        <input type="file" id="files" ref="refFile" style="display: none "
               multiple="multiple" v-on:change="fileLoad">
        <p class = "uploadText" style="position: relative;" >uploadFile</p>
        <el-tooltip class="item" effect="light"
                    content="兼容历史版本" placement="right-start" style="position: relative;">
          <i class="el-icon-question"></i>
        </el-tooltip>
      </div>
  </div>
</template>

<script>
import Ping from './components/Ping';
// eslint-disable-next-line import/first
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Ping,
  },
  data() {
  },
  methods: {
    getMessage() {
      const that = this;
      // 对应 Python 提供的接口，这里的地址填写下面服务器运行的地址，本地则为127.0.0.1，外网则为 your_ip_address
      const path = 'http://127.0.0.1:5000/app';
      axios.get(path).then((response) => {
        // 这里服务器返回的 response 为一个 json object，可通过如下方法需要转成 json 字符串
        // 可以直接通过 response.data 取key-value
        // 坑一：这里不能直接使用 this 指针，不然找不到对象
        const msg = response.data.msg;
        // 坑二：这里直接按类型解析，若再通过 JSON.stringify(msg) 转，会得到带双引号的字串
        that.serverResponse = msg;

        window.console.log(`Success ${response.status}, ${response.data}, ${msg}`);
      }).catch((error) => {
        window.console.log(`Error${error}`);
      });
    },
    clickLoad() {
      this.$refs.refFile.dispatchEvent(new MouseEvent('click'));
    },
    fileLoad() {
      const trainFile = this.$refs.refFile.files[0];
      const resultFile = this.$refs.refFile.files[1];
      const reader = new FileReader();
      reader.readAsText(trainFile);
      // eslint-disable-next-line func-names
      reader.onload = function () {
        window.console.log(this.result);
      };
      const param = new FormData();
      param.append('filetrain', trainFile);
      param.append('fileresult', resultFile);
      const config = {
        headers: { 'Content-Type': 'multipart/form-data' },
      };
      axios.post('http://127.0.0.1:5000/app', param, config).then((response) => {
        window.console.log(response.data);
      }).catch((error) => {
        window.console.log(`Error${error}`);
      });
    },
    created() {
      this.getMessage();
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#particles-js {
    background-image: url("./assets/sky.jpg");
    background-size: cover;
    height: 100%;
    width: 100%;
    position: absolute;
    overflow: hidden;
    z-index:0
  }
.btn{
    width: 230px;
    height:230px;
    margin-left: 30px;
    margin-right:950px;
    margin-top:170px;
    background: url("./assets/upload.jpg") no-repeat;
    border-style: none;
    position: relative;
}
.uploadText{
    width: 2rem;
    height:3rem;
    font-size:3rem;
    margin-left: 200px;
    margin-right:500px;
    margin-top: -20px;
    border-style: none;
    color:#191919;
}
.title{
    width: 80rem;
    height:3rem;
    font-size:5rem;
    top: 6rem;
    margin-top: -0.5%;
    border-style: none;
    color: rgba(58, 71, 125, 0.91);
    left:5%
  }
</style>
