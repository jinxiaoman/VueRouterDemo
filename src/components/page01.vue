<template>
  <div class="hello">
    <h1>page01</h1>
    <span>这是简单的路由页面，无任何功能。</span>
    <div>
      <input v-model='message'>
      <p>{{message | reverseString}}</p>
    </div>
    <div>
      <textarea v-model="content" :maxlength="total"></textarea>
      <p>你还可以输入{{reduce}}</p>
    </div>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        message : '',
        total: 100,
        content: ''
      }
    },
    computed :{
      reduce (){
        return this.total - this.content.length
      }
    }
    ,
    filters : {
      reverseString (value) {
        if(!value) return '';
        value = value.split('').reverse().join('');
        return value
      }
    }
  }
</script>
