<template>
  <div id="app">
    <img src="./assets/logo.png" />
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <!-- 子组件 -->
    <counter-Vue :child ="tochild" :baby="baby" @getchild="getchiddata"></counter-Vue>
    <div v-html="msg"></div>
    <div v-text="msg"></div>
    <div>{{childdata}}儿子传过来的数据</div>
    <p :style="{fontSize:fontSize,color:color}">你是不是个猪猪</p>
    <div class="father">
      <ul ref="banner">
        <li v-for="item in imgarr" :key="item.key">
          <img :src='item.src' alt='zhaoubuda' />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import counterVue from './view/counter';
export default {
  name: "app",
  data() {
    return {
      msg: "<p>Welcome to Your Vue.js App</p>",
      isactive: true,
      tochild:'我是你爸爸',
      isboxstyle: "boxstyle",
      fontSize: "30px",
      color: "red",
      baby:"张雅洁",
      childdata:'',
      currentindex:0,
      imgarr: [
        {
          key: 1,
          src: require("./assets/icon1.jpg")
        },
        {
          key: 2,
         src: require("./assets/icon2.jpg")
        },
        {
           key:3,
         src: require("./assets/icon3.jpg")
        },
        {
           key:4,
         src: require("./assets/icon4.jpg")
        },
         {
          key: 5,
          src: require("./assets/icon1.jpg")
        },
      ]
    };
  },
  components:{
    counterVue
  },
  created(){
    this.$nextTick(()=>{
      this.start();
    })
  },
  methods: {
    change() {
      this.msg = "new name";
    },
    start(){
      this.timer=setInterval(()=>{
        this.next();
      },3000)
    },
    next(){
      this.currentindex++;
      if(this.currentindex > 4){
        this.currentindex = 1;
        this.$refs.banner.style.left=0+'px';
      }else{
        this.$refs.banner.style.left = -this.currentindex*600+'px';
      }
      
    },
    // 自定义事件获取子元素穿过来的参数
    getchiddata(data){
      this.childdata = data;
      console.log(data);
    }
  },
  computed: {},
  watch: {}
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
*{
  margin: 0;
  padding: 0;
}
.father{
  position:relative;
  width: 600px;
  height: 300px;
  margin: 0 auto;
  overflow: hidden;
  >ul{
    // transform: translateX(-600px);
    transition:left 2s;
    border: 1px solid red;
    position: relative;
    list-style: none;
    height: 300px;
    width: 3000px;
    text-align: center;
    float: left;
    margin: 0 auto;
    overflow: hidden;
    >li{
      // position: absolute;
      height: 300px;
      width: 600px;
      float: left;
      >img{
        display:block;
        height: 100%;
        width: 100%;
      }
    }
  }
}

.father:after{
  display: block;
  content: '';
  clear: both;
}

.active {
  font-size: 1px;
  color: aqua;
  background: #2c3e50;
}
.boxstyle {
  box-sizing: border-box;
  border: 2px solid red;
}
</style>



