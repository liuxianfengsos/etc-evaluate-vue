<template>
    <div>
      <!--mypart1-->
      <div id="mypart1" v-show="showpart1">
        <h1> 测评介绍</h1>
          <p id="testnormal">
            职业测试:最主要就是看我们的职业定位。职业定位是自我定位和社会定位的统一，只有在了解自己和职业的基础上才能够给自己做准确定位。
            检视个人特质
            （一）欲望(Desires)) （做事的能力）在此人生阶段 ，你究竟要什么？
            （二）能力(Ability) 你擅长什么？（一般技术以及特别技术）
            （三）性格特质（气质、性质） (Temperament) （气质、性质）你是什么类型的人？在何种情况下有最佳表现？
            （四）资产(Assets) （有形与无形）你有什么比别人占优势的地方？
          </p>
        <p id="testnormal2">
          每个人群都需要定位，其目的是保证自己持续地发展。但是各个群体定位的重点不同：定位重点在于澄清自己有什么。过高或者过低估价自己，过于看重自己的文凭，或者看重自己的成绩，有的过于低估自己身上的潜质，所以，既需要认真地分析自己，又需要多了解社会需求，以求定位准确。在大多数情况下，正确的思路是，做你应该做的事，而不是做你喜欢做的事。
          测试依据编辑
          1.职业能力倾向具有相对广泛性
          智力的高低几乎影响人一切活动的效率，但这是一种间接的影响；职业能力倾向影响着一个人在某一职业领域中多种活动的效率，而专业知识技能则仅仅影响某一有限或具体的活动。?
          2.职业能力倾向具有相对稳定性
          职业能力倾向是相对稳定的，它不像人的智力水平一样很难改变，又不同于具体的专业知识技能那样容易通过强化训练而在短期内提高或由于遗忘而丧失。?
          3.职业能力倾向是一种潜能
          职业能力倾向表现为成功的可能性，而不是已有的水平。一个人的空间想像力强，我们可以预期他在许多与空间关系密切的活动领域中有取得成功的可能，但这仅是可能而已，这个人也许并没有机会实现他的优势。?
          测评种类编辑
          为了辅助职业测试，一般测试都通过电脑系统来测试的，我们只需要按照电脑的要求做题就好。《职业能力测评系统》主要包括的有： EQ情商测评、事业心测评、 沟通交流能力测评 、处理问题能力测评 、领导能力测评 、 创业潜力测评 、成功倾向测评、职业选择测评 、 工作压力测评、 工作态度测评 、职业满意度测评 、人际关系测评等； 科学全面的职业评测工具， 让我们在自身最擅长的职业里获取最成功的职场人生。
          测评优点编辑
          1、可以帮助职业 测评参测者根据自己的性格、能力来确定自己的职业生涯发展规划；
          2、帮助参测者者确定职业目标，尽可能的发挥出自己最大的潜能；
          3、多角度专业化的职业评测维度可以帮助测评者提高个人的工作技能，提高自己的职场竞争力；
          4、让用人单位合理的应用职业评测报告结果人岗匹配，达到企业和个人的利益最大化。
        </p>

        <p id="testdire">

          1、本测试共100题，作答时题目依次递进，可倒退重选；

          2、建议用时10-15分钟；

          3、测试完成后，10天内不允许重复作答。
        </p>
        <a-button block type="primary" :size="size" @click="testbegin">立即开始评测</a-button>
      </div>
      <!--mypart2-->
      <div id="mypart2" v-show="showpart2" v-bind:style="{'background-color': activeColor }">
       <!-- <p>第一题 ：每一道题的题干说明</p>

          <a-radio-group name="radioGroup" :defaultValue="1">
            <p><a-radio :value="1">A.xxxxxxxxxxxxxxxxxxxxxxxxxxx </a-radio></p>
            <p><a-radio :value="2">B.xxxxxxxxxxxxxxxxxxxxxxxxxxx </a-radio></p>
            <p> <a-radio :value="3">C.xxxxxxxxxxxxxxxxxxxxxxxxxxx </a-radio></p>
            <p>  <a-radio :value="4">D.xxxxxxxxxxxxxxxxxxxxxxxxxxx </a-radio></p>

          </a-radio-group>
        <div><button @click="nextone">下一题</button></div>-->
        <!--{{reqmsg}}-->
<!--<a-radio-group name="radioGroup" @change="onChange" :defaultValue="0"  v-bind:style="{'background-color': activeColor }">-->
        <a-radio-group name="radioGroup" ref="myvalueset" @change="onChange" :defaultValue="0"  v-bind:style="{'background-color': activeColor }">
        <a-card :bordered="false"  v-bind:style="{'background-color': activeColor }">

          <a-form >
            <a-col :md="24" :sm="24">
              第{{exameno}}题<a-form-item   :labelCol="{ span: 7 }" :wrapperCol="{ span: 15 }">
                <h3>{{reqmsg1.qtName}}</h3>
              </a-form-item>
            </a-col>
            <a-col :md="24" :sm="24">
              <a-form-item label="A" :labelCol="{ span: 7 }" :wrapperCol="{ span: 15 }" >
                <a-radio   :value="1">{{reqmsg1.opta}}</a-radio>
              </a-form-item>
            </a-col>
            <a-col :md="24" :sm="24">
              <a-form-item label="B" :labelCol="{ span: 7 }" :wrapperCol="{ span: 15 }">
                <a-radio  :value="2">{{reqmsg1.optb}} </a-radio>
              </a-form-item>
            </a-col>
            <a-col :md="24" :sm="24">
              <a-form-item label="C" :labelCol="{ span: 7 }" :wrapperCol="{ span: 15 }">
                <a-radio  :value="3">{{reqmsg1.optc}} </a-radio>
              </a-form-item>
            </a-col>
            <a-col :md="24" :sm="24">
              <a-form-item label="D" :labelCol="{ span: 7 }" :wrapperCol="{ span: 15 }">
                <a-radio  :value="4">{{reqmsg1.optd}} </a-radio>
              </a-form-item>
            </a-col>

            <a-form-item :wrapperCol="{ span: 12, offset: 5 }">
              <a-col :md="24" :sm="24">
                <a-form-item :wrapperCol="{ span: 12, offset: 5 }">
                  <a-button type="primary" v-show="shownext" @click="nextone" htmlType="submit">下一题</a-button>
                  <a-button type="primary" v-show="showsubmit" @click="examesubmit" htmlType="submit">提交答案</a-button>
                </a-form-item>
              </a-col>
            </a-form-item>
          </a-form>
        </a-card>
        </a-radio-group>
      </div>
      <!--mypart3-->
      <div id="mypart3" v-show="showpart3">
        <h1> 【测评报告简介】 </h1>
        <p id="testnorma3">
          为了使你能更好的使用本测评报告，请你仔细阅读本测评报告的所有内容。 本报告将为你 介绍在此次报告中提到的理论基础和相关名词以及为你解读属于你的测评报告结果。 通过 本测评，可以相对准确地帮助你了解你自身的性格特征与职业选择之间的匹配关系， 同时 也为你选择未来的职业发展方向提供一定的指导和参考依据。 ■ 本测试主要以霍兰德职业兴趣理论（Holland Vocational Interest Theory）为基础， 结合每种职业兴趣类型的性格特点，并根据中国职业划分的基本类型设计而成。 ■ 本测试主要从你的活动倾向性、你的职业能力评估以及你的职业性格倾向性这三个方面 来对你的职业兴趣类型进行测评。这三个方面的内容是相辅相成的， 当你想要从事某一职 业时，你不仅需要结合自身过去从事某活动的兴趣程度，也要考虑你是否已经具备了从事这 一职业的能力。 同时，职业的发展也不能忽视自身的职业性格倾向性，因此在本测试中有 一部分测试题是对你的职业性格进行测试。 通过这三个方面的测试，将有助于为你提供更 为准确的测评结果。
        </p>
        <a-button block type="primary" :size="size" @click="myanswersubmit">点击这里查看结果</a-button>
      </div>

    </div>

</template>
<script>
  import {getAction} from '@api/manage'
  import {postAction} from '@/api/manage'
  import pick from 'lodash.pick'
  import { validateDuplicateValue } from '@/utils/util'
  import JDate from '@/components/jeecg/JDate'
  import JDictSelectTag from "@/components/dict/JDictSelectTag"
  import * as Radio from 'ant-design-vue'

  export default {
    name: 'helloworld',
    data(){

      return {
        param:{'list':[]},
        i:1,
        index:0,
        exameno:1,
        myanswer:[],
        //answer:'',

        listlength:0,
        activeColor:'skyblue',
        showpart1: true,
        showpart2: false,
        showpart3:false,
        shownext:true,
        showsubmit:false,
        size: 'large',
        reqmsg: [],
        reqmsg1:{
          "id": "id",
          "qtName": "qtName2002",
          "opta": "opta2002",
          "optb": "optb2002",
          "optc": "optc2002",
          "optd": "optd2002",
          "mark": "mark2002",
          "answer":"1"
        },
        reqmsg2:[],
        validatorRules: {
          id: {rules: [
            ]},
          qtName: {rules: [
            ]},
          qtScore: {rules: [
            ]},
          dirId: {rules: [
            ]},
          diff: {rules: [
            ]},
          typeId: {rules: [
            ]},
          subId: {rules: [
            ]},
          opta: {rules: [
            ]},
          optb: {rules: [
            ]},
          optc: {rules: [
            ]},
          optd: {rules: [
            ]},
          opte: {rules: [
            ]},
          optf: {rules: [
            ]},
          optg: {rules: [
            ]},
          answer: {rules: [
            ]},
          mark: {rules: [
            ]},
          createTime: {rules: [
            ]},
        },
       url: {
         list: "/exam/etcQuestion/list",
          submit: "/exam/etcQuestion/add",
          mylist: "/exam/etcQuestion/list4exam",
         mysubmit: "exam/etcQuestion/mysubmit"
        }
      }
    },
    methods:{
      created() {
        //console.log("09090909090090909090909090");
        //this.loadData()
      },
    /* loadData(){
       getAction(this.url.mylist,null).then((res)=>{
          console.log("loading.................."+res);
          this.reqmsg=res;
          console.log(reqmsg.size);
        });
      },*/

      testbegin(){
        //alert("现在开始答题");
          this.showpart1 = !this.showpart1;
          this.showpart2 = !this.showpart2;

        getAction(this.url.mylist).then((res)=>{
          this.reqmsg=res.result;
          if(this.reqmsg.length>0){
            this.reqmsg1.id = this.reqmsg[this.index].id;
            this.reqmsg1.qtName = this.reqmsg[this.index].qtName;
            this.reqmsg1.opta = this.reqmsg[this.index].opta;
            this.reqmsg1.optb = this.reqmsg[this.index].optb;
            this.reqmsg1.optc = this.reqmsg[this.index].optc;
            this.reqmsg1.optd = this.reqmsg[this.index].optd;
            this.reqmsg1.mark = this.reqmsg[this.index].mark;
            this.reqmsg2.push(this.reqmsg1);
          }
        });

      },
      onChange(e){
        if(e.target.value=='1'){
          this.reqmsg1.answer = 'A';
        }else if(e.target.value=='2'){
          this.reqmsg1.answer = 'B';
        }else if(e.target.value=='3'){
          this.reqmsg1.answer = 'C';
        }else if(e.target.value=='4'){
          this.reqmsg1.answer = 'D';
        }else {
          this.reqmsg1.answer = 'E';
        }
       // console.log(`answer = ${e.target.value}`);
      },

      nextone(){
        //console.log("333333333333333333"+this.$refs.myvalueset.value);
        if(this.reqmsg1.answer  == 0 || this.reqmsg1.answer  == ''){
          alert('答案不能为空');
          return false
        }

        //this.myanswer.push({'id':this.reqmsg1.id,'an':this.answer})
        this.myanswer.push(this.reqmsg1);
        this.i = this.exameno;
        this.test1();
      },
      test1(){
        if(this.i>0){
          this.index = this.i;
        }
        if(this.exameno==9){
          this.shownext = !this.shownext;
          this.showsubmit = !this.showsubmit;
        }
        //this.$refs.myvalueset.value = 0;//有警告 忽略。
        getAction(this.url.mylist).then((res)=>{
          this.reqmsg=res.result;
          if(this.reqmsg.length>0){
            this.reqmsg1.id = this.reqmsg[this.index].id;
            this.reqmsg1.qtName = this.reqmsg[this.index].qtName;
            this.reqmsg1.opta = this.reqmsg[this.index].opta;
            this.reqmsg1.optb = this.reqmsg[this.index].optb;
            this.reqmsg1.optc = this.reqmsg[this.index].optc;
            this.reqmsg1.optd = this.reqmsg[this.index].optd;
            this.reqmsg1.mark = this.reqmsg[this.index].mark;
          }
          this.exameno = this.exameno+1;
        });

      },
      examesubmit(){
        this.showpart3 = !this.showpart3;
        this.showpart2 = !this.showpart2;
        this.param = {"list":this.myanswer};
        console.log(this.param);
        postAction(this.url.mysubmit,this.param).then((res)=>{

        });
      },
      myanswersubmit(){
        alert("系统维护中，请等待。");
      }


    }
  }
</script>

