<template>
  <div>
    <el-button type="primary" style="float: right; margin-right: 10px;" @click="test">test</el-button>
    我是首页
  </div>
</template>

<script>
  var Hexo = require('hexo')

  export default {
    data () {
      return {}
    },

    methods: {
      test () {
        // '/Users/gaoyoubo/code/node/blog.mspring.org'
        var sysConfig = this.$store.state.Hexo.sysConfig
        var hexo = new Hexo(sysConfig.path, {})
        hexo.init().then(function () {
          hexo.call('generate', {}).then(function () {
            hexo.call('deploy', {}).then(function () {
              debugger
              console.log(arguments)
            }).catch(function (err) {
              this.$notify.error({
                message: 'Deploy执行失败，' + err
              })
              return hexo.exit(err)
            })
          }).catch(function (err) {
            this.$notify.error({
              message: 'Generate执行失败，' + err
            })
            return hexo.exit(err)
          })
        })
      }
    },

    beforeDestroy () {
    },

    components: {}
  }
</script>
