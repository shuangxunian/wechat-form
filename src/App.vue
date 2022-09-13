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
            <el-button type="primary" plain @click="refreshGetInfo();nowState = 2">添加</el-button>
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
      <div v-if="nowState === 2">
        <el-form label-position="left" :model="getInfo" :rules="rules" ref="getRef" label-width="170px">
          <el-form-item label="名字" prop="name">
            <el-input v-model="getInfo.name"></el-input>
          </el-form-item>
          <el-form-item label="ID" prop="id">
            <el-input v-model="getInfo.id"></el-input>
          </el-form-item>
          <el-form-item label="模板ID" prop="useTemplateId">
            <el-input v-model="getInfo.useTemplateId"></el-input>
          </el-form-item>
          <el-form-item label="所在省份" prop="province">
            <el-input v-model="getInfo.province"></el-input>
          </el-form-item>
          <el-form-item label="所在城市" prop="city">
            <el-input v-model="getInfo.city"></el-input>
          </el-form-item>
          <el-form-item label="星座运势（阳历生日）" prop="horoscopeDate">
            <el-date-picker
              v-model="getInfo.horoscopeDate"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
            <!-- <el-input v-model="getInfo.horoscopeDate"></el-input> -->
          </el-form-item>
          <el-form-item label="获取运势的时间" prop="horoscopeDateType">
            <el-select v-model="getInfo.horoscopeDateType" placeholder="请选择" style="width:220px">
              <el-option
                v-for="item in horoType"
                :key="item.name"
                :label="item.name"
                :value="item.name">
              </el-option>
            </el-select>
            <!-- <el-input v-model="getInfo.horoscopeDateType"></el-input> -->
          </el-form-item>
          <el-form-item label="点击详情跳转页" prop="openUrl">
            <el-input v-model="getInfo.openUrl"></el-input>
          </el-form-item>
          <el-form-item>
            <!-- <el-button type="primary" @click="submitForm('getRef')">立即创建</el-button> -->
            <el-button type="primary" @click="next">下一步</el-button>
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
      horoType: [
        { name: '今日' },
        { name: '明日' },
        { name: '本周' },
        { name: '本月' },
        { name: '今年' }
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
        ],
        name: [
          { required: true, message: '名字不能为空', trigger: 'blur' }
        ],
        id: [
          { required: true, message: 'id不能为空', trigger: 'blur' }
        ],
        useTemplateId: [
          { required: true, message: '模板id不能为空', trigger: 'blur' }
        ],
        province: [
          { required: true, message: '所在省份不能为空', trigger: 'blur' }
        ],
        city: [
          { required: true, message: '所在城市不能为空', trigger: 'blur' }
        ],
        horoscopeDate: [
          { required: true, message: '星座运势不能为空', trigger: 'blur' }
        ],
        horoscopeDateType: [
          { required: true, message: '获取运势的时间不能为空', trigger: 'blur' }
        ],
        openUrl: [
          { required: true, message: '详情页不能为空', trigger: 'blur' }
        ]
      },
      getInfo: {},
      USERS: []
    }
  },
  methods: {
    refreshGetInfo() {
      this.getInfo = {
        name: '',
        id: '',
        useTemplateId: '',
        province: '',
        city: '',
        horoscopeDate: '',
        horoscopeDateType: '',
        openUrl: 'https://shuangxunian.github.io/',
        festivals: [],
        customizedDateList: []
      }
    },
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
    getYMD (inputDate) {
      const date = new Date(inputDate)
      let y = date.getFullYear()
      let m = date.getMonth() + 1
      m = m < 10 ? ('0' + m) : m
      let d = date.getDate()
      d = d < 10 ? ('0' + d) : d
      return y + '-' + m + '-' + d
    },
    getMD (inputDate) {
      const date = new Date(inputDate)
      let m = date.getMonth() + 1
      m = m < 10 ? ('0' + m) : m
      let d = date.getDate()
      d = d < 10 ? ('0' + d) : d
      return m + '-' + d
    },
    next () {
      this.$refs.getRef.validate((valid) => {
        if (valid) {
          this.$message.success('已保存')
          this.getInfo.horoscopeDate = this.getMD(this.getInfo.horoscopeDate)
          this.nowState = 3
        } else {
          return false
        }
      });
    }
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
