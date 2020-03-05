<template>
    <div>{{testData}}</div>
</template>

<script>
  import {getAction} from '@api/manage'

  export default {
    name: 'Helloworld',
    data(){
      return {
        testData:"",
        url:"/test/jeecgDemo/helloworld"
      }
    },
    methods:{
      loadData(){
        getAction(this.url).then((res)=>{
          this.testData=res;
        })
      }
    },
    created() {
      this.loadData();
    }
  }
</script>

<style scoped>

</style>