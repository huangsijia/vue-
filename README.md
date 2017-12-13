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
