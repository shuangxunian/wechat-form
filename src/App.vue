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
          个人信息{{ myInfo ? '已添加' : '未添加' }}，当前一共添加{{ USERS.length }}个接收人
        </div>
        <div class="home-push">
          <el-button @click="build">生成</el-button>
        </div>
        <el-input
          style="margin-top:20px"
          type="textarea"
          :rows="2"
          placeholder="请输入内容"
          v-model="textarea">
        </el-input>
      </div>
      <div v-if="nowState === 1">
        <h3>功能选择</h3>
        <el-form label-position="left" :model="changeFun" label-width="170px">
          <el-form-item label="每日天气">
            <el-switch
              v-model="changeFun.weather"
              active-color="#13ce66"
              inactive-color="#ff4949">
            </el-switch>
          </el-form-item>
          <el-form-item label="下一休息日提醒">
            <el-switch
              v-model="changeFun.holidaytts"
              active-color="#13ce66"
              inactive-color="#ff4949">
            </el-switch>
          </el-form-item>
          <el-form-item label="金山每日一句">
            <el-switch
              v-model="changeFun.CIBA"
              active-color="#13ce66"
              inactive-color="#ff4949">
            </el-switch>
          </el-form-item>
          <el-form-item label="每日一言">
            <el-switch
              v-model="changeFun.oneTalk"
              active-color="#13ce66"
              inactive-color="#ff4949">
            </el-switch>
          </el-form-item>
          <el-form-item label="土味情话">
            <el-switch
              v-model="changeFun.earthyLoveWords"
              active-color="#13ce66"
              inactive-color="#ff4949">
            </el-switch>
          </el-form-item>
          <el-form-item label="朋友圈文案">
            <el-switch
              v-model="changeFun.momentCopyrighting"
              active-color="#13ce66"
              inactive-color="#ff4949">
            </el-switch>
          </el-form-item>
          <el-form-item label="毒鸡汤">
            <el-switch
              v-model="changeFun.poisonChickenSoup"
              active-color="#13ce66"
              inactive-color="#ff4949">
            </el-switch>
          </el-form-item>
          <el-form-item label="古诗古文">
            <el-switch
              v-model="changeFun.poetry"
              active-color="#13ce66"
              inactive-color="#ff4949">
            </el-switch>
          </el-form-item>
          <el-form-item label="星座运势">
            <el-switch
              v-model="changeFun.horoscope"
              active-color="#13ce66"
              inactive-color="#ff4949">
            </el-switch>
          </el-form-item>
          <el-form-item label="生日消息和节日消息">
            <el-switch
              v-model="changeFun.birthdayMessage"
              active-color="#13ce66"
              inactive-color="#ff4949">
            </el-switch>
          </el-form-item>
        </el-form>
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
          <el-form-item label="结果返回模板id" prop="CALLBACK_TEMPLATE_ID">
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
      <div  v-if="nowState === 2">
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
          </el-form-item>
          <el-form-item label="点击详情跳转页" prop="openUrl">
            <el-input v-model="getInfo.openUrl"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="nextTo3">下一步</el-button>
          </el-form-item>
        </el-form>
      </div>
      <div v-if="nowState === 3">
        <h3>专属节日提醒，已设置{{ getInfo.festivals.length }}个</h3>
        <el-form label-position="left" :model="thisFestival" :rules="rules" ref="thisFestivalRef" label-width="150px">
          <el-form-item label="节假日" prop="type">
            <el-select v-model="thisFestival.type" placeholder="请选择" style="width:220px">
              <el-option
                v-for="item in festivalOption"
                :key="item.value"
                :label="item.name"
                :value="item.value">
              </el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="名称" prop="name">
            <el-input v-model="thisFestival.name"></el-input>
          </el-form-item>
          <el-form-item label="日期" prop="date">
            <el-date-picker
              v-model="thisFestival.date"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="addFestival">添加</el-button>
            <el-button type="primary" @click="nextTo4">下一步</el-button>
          </el-form-item>
        </el-form>
      </div>
      <div v-if="nowState === 4">
        <h3>专属纪念日提醒，已设置{{ getInfo.customizedDateList.length }}个</h3>
        <el-form label-position="left" :model="mark" :rules="rules" ref="markRef" label-width="150px">
          <el-form-item label="名称" prop="name">
            <el-input v-model="mark.keyword"></el-input>
          </el-form-item>
          <el-form-item label="日期" prop="date">
            <el-date-picker
              v-model="mark.keyword"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="addMark">添加</el-button>
            <el-button type="primary" @click="allFinish">完成</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
    <div class="bottom">
      made by <el-link href="https://shuangxunian.github.io/" target="_blank">shuangxunian</el-link> | code <el-link href="https://github.com/shuangxunian/wechat-form" target="_blank">github</el-link>
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
      textarea: '',
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
      festivalOption: [
        { name: '阴历生日', value: '*生日' },
        { name: '阳历生日', value: '生日' },
        { name: '节日', value: '节日' }
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
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        horoscopeDateType: [
          { required: true, message: '获取运势的时间不能为空', trigger: 'blur' }
        ],
        openUrl: [
          { required: true, message: '详情页不能为空', trigger: 'blur' }
        ],
        type: [
          { required: true, message: '节假日不能为空', trigger: 'blur' }
        ],
        date: [
          { required: true, message: '日期不能为空', trigger: 'blur' }
        ]
      },
      getInfo: {},
      thisFestival: {},
      mark: {},
      USERS: [],
      changeFun: {}
    }
  },
  created() {
    this.refreshGetInfo()
    this.refreshthisFestival()
    this.refreshChangeFun()
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
    refreshthisFestival() {
      // "type": "生日", "name": "李四", "year": "1996", "date": "09-31"
      this.thisFestival = {
        type: '',
        name: '',
        date: '',
        year: ''
      }
    },
    refreshMark() {
      this.mark = {
        keyword: '',
        date: ''
      }
    },
    refreshChangeFun() {
      this.changeFun = {
        weather: true,
        holidaytts: true,
        CIBA: true,
        oneTalk: false,
        earthyLoveWords: false,
        momentCopyrighting: false,
        poisonChickenSoup: false,
        poetry: false,
        horoscope: false,
        birthdayMessage: true,
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
    nextTo3 () {
      this.$refs.getRef.validate((valid) => {
        if (valid) {
          this.$message.success('已保存')
          this.getInfo.horoscopeDate = this.getMD(this.getInfo.horoscopeDate)
          this.nowState = 3
        } else {
          return false
        }
      });
    },
    addFestival () {
      this.$refs.thisFestivalRef.validate((valid) => {
        if (valid) {
          const ymd = this.getYMD(this.thisFestival.date).split('-')
          this.thisFestival.year = ymd[0]
          this.thisFestival.date = ymd[1] + '-' + ymd[2]
          this.getInfo.festivals.push(this.thisFestival)
          this.refreshthisFestival()
        } else {
          return false
        }
      });
    },
    nextTo4 () {
      if (this.thisFestival.type || this.thisFestival.name || this.thisFestival.date) return this.$message.error('必须要保存当前数据才可进入下一步！')
      if (this.getInfo.festivals.length === 0) return this.$message.error('必须要有一个节假日！')
      this.nowState = 4
    },
    addMark () {
      this.mark.keyword = this.getYMD(this.mark.keyword)
      this.getInfo.customizedDateList.push(this.mark)
      this.refreshMark()
    },
    allFinish () {
      this.USERS.push(this.getInfo)
      this.refreshGetInfo()
      this.nowState = 0
    },
    build () {
      if (this.USERS.length === 0 || !this.userInfo.APP_ID) return this.$message.error('当前缺少必填数据，请检查！')
      const config = {
        APP_ID: this.userInfo.APP_ID,
        APP_SECRET: this.userInfo.APP_SECRET,
        IS_SHOW_COLOR: this.userInfo.isShowColor,
        CALLBACK_TEMPLATE_ID: this.userInfo.CALLBACK_TEMPLATE_ID,
        CALLBACK_USERS: [{
          name: "自己",
          id: this.userInfo.CALLBACK_USERS,
        }],
        USERS: this.USERS,
        SWITCH: this.changeFun
      }
      this.textarea = JSON.stringify(config)
      // this.nowState = 5
      // console.log(config)
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
    height: 680px;
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
  h3 {
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
