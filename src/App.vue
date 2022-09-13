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
        <el-form label-position="left" :model="userInfo" :rules="rules" ref="userRef" label-width="150px">
          <el-form-item label="APP_ID" prop="APP_ID">
            <el-input v-model="userInfo.APP_ID"></el-input>
          </el-form-item>
          <el-form-item label="APP_SECRET" prop="APP_SECRET">
            <el-input v-model="userInfo.APP_SECRET"></el-input>
          </el-form-item>
          <el-form-item label="文字颜色" prop="isShowColor">
            <el-select v-model="userInfo.isShowColor" placeholder="请选择">
              <el-option
                v-for="item in showcolor"
                :key="item.value"
                :label="item.name"
                :value="item.value">
              </el-option>
            </el-select>
            <!-- <el-input v-model="userInfo.isShowColor"></el-input> -->
          </el-form-item>
          <el-form-item label="结果返回模板" prop="CALLBACK_TEMPLATE_ID">
            <el-input v-model="userInfo.CALLBACK_TEMPLATE_ID"></el-input>
          </el-form-item>
          <el-form-item label="自己的id" prop="CALLBACK_USERS">
            <el-input v-model="userInfo.CALLBACK_USERS"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="submitForm('userRef')">立即创建</el-button>
          </el-form-item>
        </el-form>
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
      getuser: [],
      showcolor: [
        { name: '黑色', value: false },
        { name: '彩色', value: true }
      ],
      userInfo: {
        APP_ID: '',
        APP_SECRET: '',
        isShowColor: true,
        CALLBACK_TEMPLATE_ID: '',
        CALLBACK_USERS: ''
      },
      rules: {
        APP_ID: [
          { required: true, message: 'APP_ID不能为空', trigger: 'blur' }
        ],
        APP_SECRET: [
          { required: true, message: 'APP_SECRET不能为空', trigger: 'blur' }
        ],
        FESTIVALS_LIMIT: [
          { required: true, message: 'FESTIVALS_LIMIT不能为空', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.$message.success('添加成功')
          this.myInfo = 1
          this.nowState = 0
        } else {
          return false
        }
      });
    },
  }
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
    overflow: auto;
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
