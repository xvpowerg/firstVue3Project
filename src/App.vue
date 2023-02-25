<script>
export default{
  data(){
    return{
      msg: 'Vite + Vue',
      name:"Ken",
      msg:"Hello World",
      myId:"111" ,
      myId2:"v2" ,
      imgUrl:"https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png",  
      attrId:"id",
      mouseEvent:"click"
    }
  },computed:{
    //不可用箭頭函式
    //只要msg內容改變就會重新執行
   reverseStr(){
    console.log("reverseStr");
     return this.msg.split('').reverse().join('');
    },
    //計算屬性有get set
    testCmpMethod:{
      get(){
        console.log("testMethod");
        return "testMethod";
      },
      set(){
        console.log("testMethod");
      }
    }

  },
  methods:{//不可用箭頭函式
    //只要呼叫就會重新執行
    changeName(){
      this.name = "Lucy"
    },
    testMethod(){
      console.log("testMethod");
    }
  }
}

</script>

<template>  
    <div>
      <!--可用javaScript-->
        <h1>{{msg.split('').reverse().join('')  }}</h1>
      
        <p>{{ msg }}</p>
        <p>{{ name }}</p>
    </div>
    <!--內容用html方式顯示-->
    <h1 v-html="msg"></h1>
    <!--綁定屬性內容-->
    <img v-bind:src="imgUrl" alt="google logo">
    <!--綁定屬性內容縮寫-->
    <p :id="myId">sss</p>   
    <!--可使用JavaScript-->
    <p :id="()=>{return myId;}">sss</p>   
    <button @click="changeName">Change Name</button>
    <!--動態屬性 屬性類型為變數-->
    <p :[attrId]="myId2">BBB</p>
    <!--動態事件 事件類型為變數-->
    <button @[mouseEvent]="changeName">Change Name</button>
    <!--計算屬性-->
    <p>{{ reverseStr }}</p>
    <p>{{ reverseStr }}</p>
    <!--方法-->
    <p>{{ testMethod() }}</p>
    <p>{{ testMethod() }}</p>
    <!--計算屬性 get set-->
    <p>{{ testCmpMethod }}}</p>
</template>

<style >
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
#v2{
  color:red;
}
</style>
