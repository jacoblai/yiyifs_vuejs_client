<template>
  <div class="container">
    <div class="large-12 medium-12 small-12 cell">
      <label>选择文件
        <input type="file" id="file" ref="file" v-on:change="handleFileUpload()"/>
      </label>
      <button v-on:click="submitFile()">上传文件</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      file: ''
    }
  },
  methods: {
    submitFile () {
      let formData = new FormData()
      formData.append('file', this.file)
      axios.post('http://localhost:9007/api/up',
        formData,
        {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        }
      ).then(function (res) {
        console.log(res.data, 'SUCCESS!!')
        alert(JSON.stringify(res.data))
      })
        .catch(function () {
          console.log('FAILURE!!')
        })
    },
    handleFileUpload () {
      this.file = this.$refs.file.files[0]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
