<template>
  <div class="app">
    <div class="header">
      <h1>信息生成</h1>
    </div>
    <div class="body">
      <div v-if="nowState === 0">
        <el-row>
          <el-col :span="8">
            个人信息
          </el-col>
          <el-col :span="16">
            <el-button type="primary" plain @click="nowState = 1">{{ myInfo ? '修改' : '添加'}}</el-button>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="8">
            接收人信息
          </el-col>
          <el-col :span="16">
            <el-button type="primary" plain>添加</el-button>
          </el-col>
        </el-row>
        <div class="info">
          个人信息{{ myInfo ? '已添加' : '未添加' }}，当前一共添加{{ getuser.length }}个接收人
        </div>
        <div class="home-push">
          <el-button>生成</el-button>
        </div>
      </div>
      <div v-if="nowState === 1">

      </div>
    </div>
    <div class="bottom">
      made by shuangxunian | code github
    </div>

  </div>
</template>

<script>

export default {
  name: 'app',
  components: {
  },
  data () {
    return {
      nowState: 0,
      myInfo: 0,
      getuser: []
    }
  },
  methods: {}
}
</script>

<style lang="less" scoped>
.app {
  width: 500px;
  height: 800px;
  margin-top: 60px;
	margin: auto;
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
  line-height: 40px;
  .body {
    .home-push {
      margin-top: 30px;
      text-align: center;
    }
    .info {
      margin-top: 20px;
    }
  }
  h1 {
    text-align: center;
  }
  .el-row {
    margin-top: 10px;
  }
  .bottom {
    width: 100%;
    text-align: center;
    position: absolute;
    bottom: 0
  }
}
</style>
