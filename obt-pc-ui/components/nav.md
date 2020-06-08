# 导航栏

* 模板
```html
    <!-- js/components/header/index.html -->
    <div>
        <a v-for="(info,index) in obj" :key="index" :href="info.url" :class="{'bg_gold_line':active==info.sn}" @click="active=info.sn">{{info.name}}</a>
        <span v-show="loginMessage.empInfo.isAdmin==1" class="inline-block entry_mange bg_gold_line pointer white" @click="guanli">
            <span class="i18n" name="B025">进入管理端</span> &gt;
        </span>
    </div>
```
* 数据源

```html
    <!-- js/components/header/index.html -->
    obj:{
        'M_home':{
            name:this.$t('A003'),//'首页',
            url:'/corpConfig/qhhk/template/view/index1.html?enum=1&sel=0',
            show:true,
            sn:'0'
        },
        'M_10901':{
            name:this.$t('A017'),//国内机票
            url:'/corpConfig/qhhk/template/tk/book/flights.html?enum=3&noc=1&sel=1',
            show:false,
            sn:'1'
        },
        'M_10902':{
            name:this.$t('A018'),//'国际机票',
            url:'/corpConfig/qhhk/template/tkInter/tkInterNeedEdit.html?enum=3&noc=1&sel=4',
            show:false,
            sn:'4'
        },
        ...
    }

```