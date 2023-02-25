<script>
export default{
  data(){
    return{
      msg: 'Vite + Vue',
      name:"Ken",
      myId:"111" ,
      myId2:"v2" ,
      imgUrl:"https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png",  
      attrId:"id",
      mouseEvent:"click",
      watchMsg:"Init watchMsg",
      myUser:{
        name:"Ken",
        age:18
      },
      cssStyle:{
        active:true,
        fontsize:true
      },
      isError:false,      
      styleObj:{
        color:"red",
        fontSize:"20px"
      }
    }
  },computed:{
    //不可用箭頭函式
    //只要msg內容改變就會重新執行
   reverseStr(){
   // console.log("reverseStr");
     return this.msg.split('').reverse().join('');
    },
    //計算屬性有get set
    testCmpMethod:{
      get(){
        //console.log("testMethod");
        return "testMethod";
      },
      set(myvalue){//一般不用
       // console.log(`testMethod:${myvalue}`);
      }
    },
    classObjCmp(){
      return {
        active:this.cssStyle.active&&!this.isError,
        fontsize:this.cssStyle.fontsize
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
    },showLog(){
      console.log("showLog:"+this.styleObj.color);
    }
  } ,  
  //當watchMsg 改變時會觸發
  //可呼叫非同步函式
  //一個改變會引響其他屬性
  watch:{
      watchMsg:{
        immediate:true,//立即執行
        handler(newVal,oldVal){
          console.log(`watchMsg:${newVal}`);
        }
      },
      //深度監聽
    // myUser:{
    //   handler(newVal,oldVal){
    //     console.log(`myUser:${newVal.name}`);
    //   },
    //   //物件的所有屬性都監聽
    //   deep:true
    // }
    "myUser.name":{//只會監聽myUser.name
      handler(newVal,oldVal){
        console.log(`myUser:${newVal}`);
      },
      //物件的所有屬性都監聽
      deep:true
    }
    }
}

</script>

<template>  
    <div>
      <!--可用javaScript-->
        <h1>{{msg.split('').reverse().join('')  }}</h1>
      
        <p>{{ watchMsg }}</p>
        <p>{{ name }}</p>
    </div>
    <button @click="watchMsg='watchMsg Good'">Change Watch Msg</button>
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
    <!--數據雙向綁定-->
    <input type="text" v-model="watchMsg">
    <button @click="myUser.name='Iris'">changeUser</button>
    <!--CSS綁定-->
    <p class="active">active!</p>
    <!--也一個active的類別樣式 是否啟用-->
    <p :class="cssStyle">active!</p>
    <button @click="cssStyle.active = !cssStyle.active">isActivie</button>
    <!--可與class 樣式 一同時用-->
    <button @click="cssStyle.fontsize = !cssStyle.fontsize">FontSize</button>
    <p :class="classObjCmp">classObjCmp</p>
    <button @click="isError = !isError">isError</button>
    <!--綁定Style物件-->
    <p :style="styleObj">styleObj</p>
    <button @click="styleObj.color='blue'">styleObj</button>
    <button @click="showLog">TestLog</button>
</template>

<style >

.fontsize{
  font-size: 2em;
}
.active{
  color:blueviolet;
}
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
