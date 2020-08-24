## vue启不来
    npm rebuild node-sass
    npm install babili-webpack-plugin --save-dev
## 想念vue无数坑洞总结
    @function pxToRem($px) {
        @return $px/11/2+rem;
    }
## 华为兼容性处理
    cnpm install --save-dev babel-polyfill
    
## vue的css
      <style lang="sass-loader">
          @import "../../assets/home";
      </style>
      <style lang="scss" scoped="" type="text/css">
          @import "../../assets/skin";
      </style>
## vue获取地址to.query.后缀=true
    beforeEnter: (to, from, next) => {
          Public.API_GET({
                url: 'checkMemberBank',
                success: (result) => {
                if(!result.isSuccess){
                    Toast({
                    message: result.message,
                    position: 'bottom',
                    duration: 2000
                    });
                    return
                }
                  //是否开通存管
                  if(result.data.kaitong){
                    to.query.cunguan=true
                  }else{
                    to.query.cunguan=false
                  }
                  if (result.data.bind) {
                    next();
                  } else {
                    next({ path: '/home',query: to.query});
                  }
                }
            });
        }
    
## vue传参
    window.Hub.mobile = result.data.mobile;
    this.mobile = window.Hub.mobile
    
## 表单验证错误
    this.errors.errors
## 跳转
    this.$router.push({
        path: '/index'
    });
    
    this.$router.push({ path: '/home/bank/rechargeResult',query: {"success":true,"amount":this.$parent.sendData.amount} });
    
    this.$route.query.tradeNo
    
    
    path: '/invest/fina/:id',
    console.log(this.$route.params.id)
    
## 跳转带参数，以及取参数
    this.$router.push({ path:"/index/forget",query:{"fromCenter":true}});
    this.$route.query.fromCenter
    
## 上传到github
    git clone https://github.com/CKTim/BlueTooth.git（https://github.com/CKTim/BlueTooth.git替换成你之前复制的地址）
    这个步骤以后你的本地项目文件夹下面就会多出个文件夹，该文件夹名即为你github上面的项目名，如图我多出了个Test文件夹，我们把本地项目文件夹下的所有文件（除了新多出的那个文件夹不用），其余都复制到那个新多出的文件夹下，接着继续输入命令 cd Test，进入Test文件夹
    git add .        （注：别忘记后面的.，此操作是把Test文件夹下面的文件都添加进来）
    git commit  -m  "提交信息"  （注：“提交信息”里面换成你需要，如“first commit”）
    git push -u origin master   （注：此操作目的是把本地仓库push到github上面，此步骤需要你输入帐号和密码）
    git push -u git@github.com:huangsijia/my-project.git master

    
## a页面input输入结束，点击链接跳转到b页面，返回a页面值没有保留,a页面链接加上save方法，页面加载处，添加获取
    save(){
        try {
            localStorage.setItem('amount',this.amount)
        } catch (error) {
            sessionStorage.setItem('amount',this.amount)
        }
    }
    mounted:function(){
        var last = null;
        try {
            last = localStorage.getItem('amount')
        } catch (error) {
            last = sessionStorage.getItem('amount')
        }
        if(last){
            this.amount = last;
            try {
                localStorage.removeItem('amount')
            } catch (error) {
                sessionStorage.removeItem('amount')
            }
        }
    }
## 反编译带html的
    v1方法{{{rh}}}
    v2方法v-html
## css只在当前页面使用scoped=""
 //<style lang="scss" scoped="" type="text/css">
    
## index.js 跨域 proxyTable加内容https://vuejs-templates.github.io/webpack/proxy.html
dev: {
    env: require('./dev.env'),
    port: 4399,
    autoOpenBrowser: true,
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    proxyTable: {
      '**/wd_api/**': {
        target: 'http://www.a.com',
        changeOrigin: true
      }
    },
    // CSS Sourcemaps off by default because relative paths are "buggy"
    // with this option, according to the CSS-Loader README
    // (https://github.com/webpack/css-loader#sourcemaps)
    // In our experience, they generally work as expected,
    // just be aware of this issue when enabling this option.
    cssSourceMap: false
  }
## 下拉加载数据https://github.com/metafizzy/infinite-scroll
    <ul class="person leftRight" v-infinite-scroll="loadMore" infinite-scroll-disabled="loading" infinite-scroll-distance="10">
    loadMore() {
                    if (this.initLock) {
                        return
                    }
                    if (!this.hasNext) {
                        return
                    }
                    this.loading = true;
                    this.$public.API_GET({
                        url: 'getInviteDetail',
                        data: {
                            offset: this.offset,
                            max: this.max
                        },
                        success: (result) => {
                            for (var item in result.data) {
                                this.list.push(result.data[item])
                            }
                            this.offset += this.max;
                            this.loading = false;
                            if (result.data.length < this.max) {
                                this.hasNext = false
                            }
                        }
                    });
                },
                initData(finishFun) {
                    this.offset = 0;
                    this.max = 10;
                    this.hasNext = true;
                    this.list = [];
                    this.loadEnd = false;
                    this.$public.API_GET({
                        url: 'getInviteDetail',
                        data: {
                            offset: this.offset,
                            max: this.max
                        },
                        success: (result) => {
                            this.loadEnd = true
                            this.list = result.data;
                            this.offset += this.max;
                            if (result.data.length < this.max) {
                                this.hasNext = false
                            }
                            this.initLock = false
                            if (typeof(finishFun) == "function") {
                                finishFun()
                            }
                        }
                    });
                }
## 离开此页面之前的方法
    beforeRouteLeave: function(to, from, next) {
			$(document.body).removeClass("htmlBg");
			next();
		}
## body下加入div
    addFooter(id, schedule) {
      var packet = Vue.extend({
        data: function() {
          return {
            text: "立即加入"
          };
        },
        methods: {
          joinBtnFun() {
            location.hash = "/invest/pay/" + id;
          }
        },
        template: `<div class="joinBtn" @click="joinBtnFun"><div class="btn btnBottom">{{this.text}}</div></div>`
      });
      var packetIntance = new packet({
        el: document.createElement("div")
      });

      document.body.appendChild(packetIntance.$el);
    }
  }
  
  ## 跨域
	  dev: {
	    env: require('./dev.env'),
	    port: 4398,
	    autoOpenBrowser: true,
	    assetsSubDirectory: 'static',
	    assetsPublicPath: '/',
	    proxyTable: {
	      '**/wd_api/**': {
		// target: 'http://10.0.1.33:8686/',
		target: 'https://www.bxjr.com/',
		changeOrigin: true
	      }
	    },
	    // CSS Sourcemaps off by default because relative paths are "buggy"
	    // with this option, according to the CSS-Loader README
	    // (https://github.com/webpack/css-loader#sourcemaps)
	    // In our experience, they generally work as expected,
	    // just be aware of this issue when enabling this option.
	    cssSourceMap: false
	  }
## 同级参数不显示
	this.$router.push({ name: 'address',params: {"name":item.name} });
	取：this.$route.params.name

## 自定义指令
	//html 
	<div v-pin:true.bottom.right='pinned' class="card">爱
	    <button @click="pinned = !pinned">叮嘱</button>
	</div>
	// js
	Vue.directive("pin",function(el,binding){
	    var pinned = binding.value
	    var position = binding.modifiers;
	    var warnning = binding.arg;
	    console.log(warnning)
	    if(pinned){
		el.style.position="fixed";
		for(var key in position){
		    if(position[key]){
			el.style[key]="10px"
		    }
		}
		if (warnning === 'true'){
		    el.style.background = 'yellow'
		}        
	    }else{
		el.style.position='static'
	    }
	})

## 混合 mixins
	var mixinsFun = {
	    methods:{
		show() {
		    this.visible = true;
		},
		hide(){
		    this.visible = false;
		}
	    },
	    data:function(){
		return{
		    visible: false
		}
	    }
	}


	Vue.component('popup',{
	    template:`
	    <div>
		<button @mouseenter="show" @mouseleave="hide">
		    会显示吗？
		</button>
		<span v-if="visible">显示了</span>
	    </div>
	    `,
	    mixins:[mixinsFun],
	    // 会直接覆盖mixins里的定义
	    data: function () {
		return {
		    visible: true
		}
	    }
	})
	Vue.component('tooltip', {
	    template: `
	    <div>
		<button @click="show">
		    点击了
		</button>
		<div v-if="visible">
		    <p @click="hide">关闭</p>
		    <h1>title</h1>
		    <span>sewghew任何事吉尔吉</span>
		</div>
	    </div>
	    `,
	    mixins: [mixinsFun]
	})


## 插槽slots 用name来指定不同插槽
	<div id="app">
		<panel>
		    <div slot="title">我是标题</div>
		    <div slot="content">我是内容我是内容我是内容我是内容我是内容</div>
		    <div slot="footer">我是footer</div>
		</panel>
	</div>
	<template id="panel-tpl">
		<div class="panel">
		    <div class="title">
			<slot name="title">title</slot>
		    </div>
		    <div class="content">
			<slot name="content">content</slot>
		    </div>
		    <div class="footer">
			<slot name="footer">footer</slot>
		    </div>
		</div>
	</template>
	
## 关于vue中iconfont字体图标显示乱码处理
	字体编码后前四位是Unicode编码，想使用字符串来传递的话,只要将 “&#xe64b;” 改为 “\ue64b” 即可

## app h5交互
	 安卓：window.GetAppMethd.share();
	 iOS：window.webkit.messageHandlers.share.postMessage();
	 微信登录：
	 1、点击告诉app微信登录，调用app方法 wechatLogin
	 2、app成功后传token给h5
	 2、或者 app给h5code,h5调用后台接口
	 3、请求trade接口，判断支付宝支付还是微信支付，调用不同的app方法，app返回结果后，调用h5 的payValue方法，如果app返回成功调用后台的”支付状态查询“接口，显示支付成功或者支付失败）
	 4、window['app调用方法名'] = (result) => {
          this.本地方法名(result)
        }
