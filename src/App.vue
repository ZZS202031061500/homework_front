<template>
  <div id="app">
    <div class="box">
      <textarea v-model="text" class="before" placeholder="没嘴吗，说话"></textarea>
      <button @click="sendText">转换</button>
<!--      <hr>-->
<!--      <h4>你看看你说的是什么gb</h4>-->
      <textarea v-model="result" class="before"></textarea>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  components: {},
  data () {
    return {
      text: '',
      result: ''
    }
  },
  methods: {
    async sendText () {
      const sentences = this.text.split('\n')
      console.log(sentences)
      this.result = sentences.join('\n')
      const { data: result } = await axios.post('http://localhost:8081/text/upload', JSON.stringify(sentences), {
        headers: {
          'Content-Type': 'application/json;charset=UTF-8'
        }
      })
      this.result = result.join('\n')
    }
  }
}
</script>

<style lang="less">
* {
  outline: none;
  margin: 0;
  padding: 0;
  border-radius: 20px;
  padding: 20px;
  box-sizing: border-box;
}

.box {
  margin: 100px auto;
  width: 1000px;
  height: 500px;
  //background-color: pink;
  line-height: 500px;

  textarea {
    position: relative;
    top: 100px;
    display: inline-block;
    width: 400px;
    height: 300px;
    background-color: #cccc;
    border-radius: 20px;
    padding: 20px;
    box-sizing: border-box;
  }

  button {
    margin: 0 20px;
    display: inline-block;
    width: 100px;
    height: 300px;
    background-color: red;
    position: relative;
    top: -43px;
  }
}
</style>
