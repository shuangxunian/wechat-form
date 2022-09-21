# wechat
这个项目是辅助[wechat-public-account-push](https://github.com/wangxinleo/wechat-public-account-push)项目生成个人信息的配套文件，使用请[点此](https://shuangxunian.github.io/wechat-form/)，有bug在群里艾特霜序廿即可，使用方法如下：

## 添加个人信息：

![](https://api2.mubu.com/v3/document_image/a33e14f4-5707-4676-8eed-ba03737495b9-3807603.jpg)

## 选择你所需的功能：

![](https://api2.mubu.com/v3/document_image/0d5f227c-95ec-41a5-a03c-359ee82c6435-3807603.jpg)

我的建议是如上，你选了过多的功能会导致：
  - 文字过长不能全部展示
  - 代码运行耗时增加，github和gitee均有限时
  - 容易运行出错

## 下滑，添加你的个人信息，然后点击创建：

![](https://api2.mubu.com/v3/document_image/75028b5b-359b-4290-ab33-5bbe64c5b5b1-3807603.jpg)

其中：
  - APP_ID对应的是测试号信息中appID对应的字符串，APP_SECRET对应的是图片中appsecret对应的字符串
  ![](https://api2.mubu.com/v3/document_image/5939f011-faa9-4f04-b13c-7df78fc05353-3807603.jpg)
  - 文字颜色指的是用户收到的文字颜色，如果用了emoji，一定要选黑色
  - 结果返回模板，自己的id，如果不填写就没有回调，如果填写了每次发送成功就会发给你一条消息，其中的结果返回模板要选择你创建的回调模板的id，自己的id要填写自己扫完码在测试号二维码中的自己的id，模板在原来的仓库均有我们给设计好的，直接拿过来复制粘贴就行。
  ![](https://api2.mubu.com/v3/document_image/28c73a12-3313-4787-a9a9-be67dc86ba2f-3807603.jpg)
  ![](https://api2.mubu.com/v3/document_image/86ddc14d-1f57-4b58-8abb-8f31c9864261-3807603.jpg)

## 添加接收人信息：
- 名字：为你称呼你女朋友的昵称
- ID：为你女朋友扫完码所生成的字符串，要用你女朋友对应的id！
![](https://api2.mubu.com/v3/document_image/28c73a12-3313-4787-a9a9-be67dc86ba2f-3807603.jpg)
- 模板ID：为你想给女朋友发的模板，要用你发给女朋友的模板！
![](https://api2.mubu.com/v3/document_image/86ddc14d-1f57-4b58-8abb-8f31c9864261-3807603.jpg)
- 所在省份：写到省
- 所在城市：写到市、县，建议先[点此](https://github1s.com/wangxinleo/wechat-public-account-push/blob/HEAD/src/store/index.js)，然后点击左侧的放大镜按钮搜索一下是否有你女朋友的所在地
![](https://api2.mubu.com/v3/document_image/d79260b3-b4f7-4628-8ee8-f5eea33415eb-3807603.jpg)
- 星座运势（阳历生日）
- 获取运势的时间
- 点击详情跳转页，默认是作者博客，这个由于微信要求，必须要填，这个可以换成任何一个**合法的，可以访问的**链接

## 节假日提醒
这个凭自己想法添加就好，有几点需要注意的：
- 请不要和我们的关键字用相同的英文
- 生日时，name填写想要展示的名字，你可以填“美丽可爱亲亲老婆”
- 节日时，name填写相应展示的节日，你可以填“被搭讪纪念日”

## 纪念日提醒
- 这里的名称指暴露给测试号的模板字段，填什么就暴露什么, 请注意不要和README的出参表中的字段重复，如：

![](https://api2.mubu.com/v3/document_image/ccaa0e0e-75da-434f-85c4-8af6e0659e98-3807603.jpg)

和此对应：

![](https://api2.mubu.com/v3/document_image/6c1770bb-4fc1-4c7f-adb1-2a5346da3459-3807603.jpg)

## end
有问题请先自己搜索[原文档](https://github.com/wangxinleo/wechat-public-account-push)，如果还不能解决请到群里提问

