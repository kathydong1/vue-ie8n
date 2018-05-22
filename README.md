使用 vue-i18n 切换中英文
vue-i18n 仓库地址：https://github.com/kazupon/vue-i18n

兼容性：

支持 Vue.js 2.x 以上版本

 

安装方法：（此处只演示 npm）

npm install vue-i18n
 

使用方法：

1、在 main.js 中引入 vue-i18n （前提是要先引入 vue）

import VueI18n from 'vue-i18n'

Vue.use(VueI18n)
 

2、准备本地的翻译信息

复制代码
const messages = {
    zh: {
      message: {
        hello: '好好学习，天天向上！'
      }
    },
    en: {
      message: {
        hello: 'good good study, day day up!'
      }
    }
}
复制代码
 

3、创建带有选项的 VueI18n 实例

const i18n = new VueI18n({
    locale: 'en', // 语言标识
    messages
})
 

4、把 i18n 挂载到 vue 根实例上

const app = new Vue({
    router,
    i18n,
    ...App
}).$mount('#app')
 

5、在 HTML 模板中使用

<div id="app">
    <h1 style="font-size: 16px; text-align: center;">{{ $t("message.hello") }}</h1>
  </div>
 

查看运行效果：



我们刚才选定的语言标识是 “en” 英语，现在改成 “zh” 中文，并查看效果

const i18n = new VueI18n({
    locale: 'zh', // 语言标识
    messages
})


这样就可以轻松实现国际化了，实际开发中，页面内容肯定是很多的，我们可以把对应语言的信息保存为不同的 json对象

复制代码
const i18n = new VueI18n({
    locale: 'en',  // 语言标识
    messages: {
        'zh': require('./common/lang/zh'),
        'en': require('./common/lang/en')
    }
})
复制代码
zh.js

复制代码
// 注意：一定是 exports，不是 export，否则会报错，报错信息是下列的中的内容不是 string
module.exports = {
    message: {
        title: '运动品牌'
    },
    placeholder: {
        enter: '请输入您喜欢的品牌'
    },
    brands: {
        nike: '耐克',
        adi: '阿迪达斯',
        nb: '新百伦',
        ln: '李宁'
    }
}
复制代码
en.js

复制代码
module.exports = {
    message: {
        title: 'Sport Brands'
    },
    placeholder: {
        enter: 'Please type in your favorite brand'
    },
    brands: {
        nike: 'Nike',
        adi: 'Adidas',
        nb: 'New Banlance',
        ln: 'LI Ning'
    }
}
复制代码
接下来，在HTML 模板中使用，要特别注意在 js 中的国际化写法

复制代码
// HTML
<div id="app">
    <div style="margin: 20px;">
      <h1>{{$t("message.title")}}</h1>
      <input style="width: 300px;" class="form-control" :placeholder="$t('placeholder.enter')">
      <ul>
        <li v-for="brand in brands">{{brand}}</li>
      </ul>
    </div>
</div>

// JS
data () {
    return {
      brands: [this.$t('brands.nike'), this.$t('brands.adi'), this.$t('brands.nb'), this.$t('brands.ln')]
    }
 },
