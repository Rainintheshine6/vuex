<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <h2>{{child}}</h2>
    <h3>{{baby}}</h3>
    <div>{{newdata}}</div>
  </div>
</template>
<script>
export default {
  name: "counter",
  props: ["child", "baby"],
  data() {
    return {
      msg: "我是counter",
      newdata: ""
    };
  },
  created() {
    this.newdata = this.$props.child + "我是props传的值";
  },
  mounted(){
    this.$emit('getchild',this.name);
  },
  methods: {},
  computed: {},
  watch: {}
};
</script>

<style lang="scss">
</style>



