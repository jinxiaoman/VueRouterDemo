<template>
  <div class="hello">
    <h1>page01</h1>
    <span>这是简单的路由页面，无任何功能。</span>
    <!--计算属相，翻转一切-->
    <h3>翻转吧</h3>
    <div>
      <input v-model='message'>
      <p>{{message | reverseString}}</p>
    </div>
    <!--检测文字输入-->
    <h3>输入吧，超过200算我输</h3>
    <div>
      <textarea v-model="content" :maxlength="total"></textarea>
      <p>你还可以输入{{reduce}}</p>
    </div>
    <!--赛足球，计算多个数据？、-->
    <h3>赛足球</h3>
    <div>
      <h1>比赛时间{{time}}s</h1>
      <h2>直播播报{{result}}</h2>
      <div>
        <p>中国队进球数：{{team.china}}</p>
        <button @click="team.china++">点击中国队进一球</button>
        <p>韩国队进球数：{{team.korea}}</p>
        <button @click="team.korea++">点击韩国队进一球</button>
      </div>
  </div>
    <p>一.computed前面说了是适用于对多数据变动进行监听，然后来维护一个状态，就是返回一个状态
      <br>
      二.watch是对一个数据监听，在数据变化时，会返回两个值 ，一个是value(当前值)，二个是oldvalue是变化前的值，我们可以通过这些变化也可以去维护一个状态，但是不符合场景，主要用于什么地方呢？主要用于监听一个数据来进行复杂的逻辑操作
      <br>
      <b>watch方法,data添加result：双方僵持</b>
      <!--watch : {-->
      <!--time (value,oldval) {-->
      <!--if(value<90){-->
      <!--if(this.team.china>this.team.korea){-->
      <!--this.result =  '中国队领先'-->
      <!--}else if(this.team.china<this.team.korea){-->
      <!--this.result =  '韩国队领先'-->
      <!--}else{-->
      <!--this.result =  '双方僵持'-->
      <!--}-->
      <!--}else{-->
      <!--if(this.team.china>this.team.korea){-->
      <!--this.result =  '中国队赢'-->
      <!--}else if(this.team.china<this.team.korea){-->
      <!--this.result =  '韩国队赢'-->
      <!--}else{-->
      <!--this.result =  '平局'-->
      <!--}-->
      <!--}-->
      <!--},-->
      <!--team (value,oldval){-->
      <!--if(this.time<90){-->
      <!--if(value.china>value.korea){-->
      <!--this.result =  '中国队领先'-->
      <!--}else if(value.china<value.korea){-->
      <!--this.result =  '韩国队领先'-->
      <!--}else{-->
      <!--this.result =  '双方僵持'-->
      <!--}-->
      <!--}else{-->
      <!--if(value.china>value.korea){-->
      <!--this.result =  '中国队赢'-->
      <!--}else if(value.china<value.korea){-->
      <!--this.result =  '韩国队赢'-->
      <!--}else{-->
      <!--this.result =  '平局'-->
      <!--}-->
      <!--}-->
    </p>
  </div>
</template>
<script>
  export default {
    created () {
      let time =  setInterval(()=>{
        this.time++
        if(this.time == 90){
          clearInterval(time)
        }
      },1000)
    },
    data () {
      return {
        message : '',
        total: 100,
        content: '',
        time : 0,
        team : {
          china : 0,
          korea : 0
        }
      }
    },
//    计算
    computed :{
//      输入长度
      reduce (){
        return this.total - this.content.length
      },
//      计算足球？
      result () {
        if(this.time<90){
          if(this.team.china>this.team.korea){
            return '中国队领先'
          }else if(this.team.china<this.team.korea){
            return '韩国队领先'
          }else{
            return '双方僵持'
          }
        }else{
          if(this.team.china>this.team.korea){
            return '中国队赢'
          }else if(this.team.china<this.team.korea){
            return '韩国队赢'
          }else{
            return '平局'
          }
        }
      }
    },
//    翻转数组
//    单对单的数据过滤,可以进行传参，同方法，但不同参，非常适用
    filters : {
      reverseString (value) {
        if(!value) return '';
        value = value.split('').reverse().join('');
        return value
      }
    }
  }
</script>
