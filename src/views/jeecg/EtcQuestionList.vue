<template>
  <a-card :bordered="false">
    <!-- 查询区域 -->
    <div class="table-page-search-wrapper">
      <a-form layout="inline" @keyup.enter.native="searchQuery">
        <a-row :gutter="24">

        </a-row>
      </a-form>
    </div>
    <!-- 查询区域-END -->
    
    <!-- 操作按钮区域 -->
    <div class="table-operator">
      <a-button @click="handleAdd" type="primary" icon="plus">新增</a-button>
      <a-button type="primary" icon="download" @click="handleExportXls('etc_question')">导出</a-button>
      <a-upload name="file" :showUploadList="false" :multiple="false" :headers="tokenHeader" :action="importExcelUrl" @change="handleImportExcel">
        <a-button type="primary" icon="import">导入</a-button>
      </a-upload>
      <a-dropdown v-if="selectedRowKeys.length > 0">
        <a-menu slot="overlay">
          <a-menu-item key="1" @click="batchDel"><a-icon type="delete"/>删除</a-menu-item>
        </a-menu>
        <a-button style="margin-left: 8px"> 批量操作 <a-icon type="down" /></a-button>
      </a-dropdown>
    </div>

    <!-- table区域-begin -->
    <div>
      <div class="ant-alert ant-alert-info" style="margin-bottom: 16px;">
        <i class="anticon anticon-info-circle ant-alert-icon"></i> 已选择 <a style="font-weight: 600">{{ selectedRowKeys.length }}</a>项
        <a style="margin-left: 24px" @click="onClearSelected">清空</a>
      </div>

      <a-table
        ref="table"
        size="middle"
        bordered
        rowKey="id"
        :columns="columns"
        :dataSource="dataSource"
        :pagination="ipagination"
        :loading="loading"
        :rowSelection="{fixed:true,selectedRowKeys: selectedRowKeys, onChange: onSelectChange}"
        
        @change="handleTableChange">

        <template slot="htmlSlot" slot-scope="text">
          <div v-html="text"></div>
        </template>
        <template slot="imgSlot" slot-scope="text">
          <span v-if="!text" style="font-size: 12px;font-style: italic;">无此图片</span>
          <img v-else :src="getImgView(text)" height="25px" alt="图片不存在" style="max-width:80px;font-size: 12px;font-style: italic;"/>
        </template>
        <template slot="fileSlot" slot-scope="text">
          <span v-if="!text" style="font-size: 12px;font-style: italic;">无此文件</span>
          <a-button
            v-else
            :ghost="true"
            type="primary"
            icon="download"
            size="small"
            @click="uploadFile(text)">
            下载
          </a-button>
        </template>

        <span slot="action" slot-scope="text, record">
          <a @click="handleEdit(record)">编辑</a>

          <a-divider type="vertical" />
          <a-dropdown>
            <a class="ant-dropdown-link">更多 <a-icon type="down" /></a>
            <a-menu slot="overlay">
              <a-menu-item>
                <a-popconfirm title="确定删除吗?" @confirm="() => handleDelete(record.id)">
                  <a>删除</a>
                </a-popconfirm>
              </a-menu-item>
            </a-menu>
          </a-dropdown>
        </span>

      </a-table>
    </div>

    <etcQuestion-modal ref="modalForm" @ok="modalFormOk"></etcQuestion-modal>
  </a-card>
</template>

<script>

  import { JeecgListMixin } from '@/mixins/JeecgListMixin'
  import EtcQuestionModal from './modules/EtcQuestionModal'
  import {filterMultiDictText} from '@/components/dict/JDictSelectUtil'

  export default {
    name: "EtcQuestionList",
    mixins:[JeecgListMixin],
    components: {
      EtcQuestionModal
    },
    data () {
      return {
        description: 'etc_question管理页面',
        // 表头
        columns: [
          {
            title: '#',
            dataIndex: '',
            key:'rowIndex',
            width:60,
            align:"center",
            customRender:function (t,r,index) {
              return parseInt(index)+1;
            }
          },
          {
            title:'试题题目',
            align:"center",
            dataIndex: 'qtName'
          },
          {
            title:'题目分数',
            align:"center",
            dataIndex: 'qtScore'
          },
          {
            title:'外键引自DIRECTION',
            align:"center",
            dataIndex: 'dirId_dictText'
          },
          {
            title:'试题难度,分别是:1 简单,2 中等,3 困难',
            align:"center",
            dataIndex: 'diff'
          },
          {
            title:'引用自QT_TYPE',
            align:"center",
            dataIndex: 'typeId_dictText'
          },
          {
            title:'引自SUBJECT',
            align:"center",
            dataIndex: 'subId_dictText'
          },
          {
            title:'选项A',
            align:"center",
            dataIndex: 'opta'
          },
          {
            title:'选项B',
            align:"center",
            dataIndex: 'optb'
          },
          {
            title:'选项C',
            align:"center",
            dataIndex: 'optc'
          },
          {
            title:'选项D',
            align:"center",
            dataIndex: 'optd'
          },
          {
            title:'选项E',
            align:"center",
            dataIndex: 'opte'
          },
          {
            title:'选项F',
            align:"center",
            dataIndex: 'optf'
          },
          {
            title:'选项G',
            align:"center",
            dataIndex: 'optg'
          },
          {
            title:'答案',
            align:"center",
            dataIndex: 'answer'
          },
          {
            title:'标记,表示当前试题是否被选中',
            align:"center",
            dataIndex: 'mark'
          },
          {
            title:'创建时间',
            align:"center",
            dataIndex: 'createTime',
            customRender:function (text) {
              return !text?"":(text.length>10?text.substr(0,10):text)
            }
          },
          {
            title: '操作',
            dataIndex: 'action',
            align:"center",
            scopedSlots: { customRender: 'action' }
          }
        ],
        url: {
          list: "/exam/etcQuestion/list",
          delete: "/exam/etcQuestion/delete",
          deleteBatch: "/exam/etcQuestion/deleteBatch",
          exportXlsUrl: "/exam/etcQuestion/exportXls",
          importExcelUrl: "exam/etcQuestion/importExcel",
        },
        dictOptions:{},
      }
    },
    computed: {
      importExcelUrl: function(){
        return `${window._CONFIG['domianURL']}/${this.url.importExcelUrl}`;
      }
    },
    methods: {
      initDictConfig(){
      }
    }
  }
</script>
<style scoped>
  @import '~@assets/less/common.less';
</style>