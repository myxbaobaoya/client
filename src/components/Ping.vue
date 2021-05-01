<template>
    <div class="container" id="Ping">
    </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Ping',
  data() {
    return {
      msg: 'Hello!',
    };
  },
  methods: {
    getMessage() {
      const path = 'http://localhost:5000/ping';
      axios.get(path)
        .then((res) => {
          this.msg = res.data;
        })
        .catch((error) => {
          // eslint-disable-next-line
          console.error(error);
        });
    },

  },
  created() {
    this.getMessage();
  },
};
</script>

<style>
.btn{
    width: 220px;
    height:250px;
    margin-left: 20px;
    margin-right:950px;
    margin-top:250px;
    background: url("../../src/assets/upload.jpg") no-repeat;
    border-style: none;
}
.uploadtext{
    width: 2rem;
    height:3rem;
    font-size:3rem;
    margin-left: 20px;
    margin-right:800px;
    margin-top:100px;
    border-style: none;
    color:#191919;
    z-index:9999
}
h1{
  font-weight: normal;
}
</style>
