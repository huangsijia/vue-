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
    
## 跳转带参数，以及取参数
    this.$router.push({ path:"/index/forget",query:{"fromCenter":true}});
    this.$route.query.fromCenter
