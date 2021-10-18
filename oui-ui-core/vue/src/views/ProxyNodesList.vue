<template>
  <div>
    <a-row type="flex" justify="end">
      <a-button type="primary" icon="redo" @click="updateNodes()">
        更新节点
      </a-button>
    </a-row>
    <a-table :columns="columns" :data-source="data" bordered size="middle">
      <template slot="server" slot-scope="text">
        <a>{{ text }}</a>
      </template>
      <!-- <template slot="title" slot-scope="currentPageData"> Header </template> -->
      <!-- <template slot="footer" slot-scope="currentPageData"> Footer </template> -->
      <template slot="operation" slot-scope="text, record, index">
        <a-row
          type="flex"
          justify="space-around"
          style="margin-top: -0.75em; margin-bottom: -0.75em; font-size: 1.5em"
        >
          <span>{{ index }}</span>
          <a-icon>
            <icon-align-to-top />
          </a-icon>
          <a-icon type="caret-up" theme="filled" />
          <a-icon type="caret-down" theme="filled" />
          <a-icon>
            <icon-sharp-speed />
          </a-icon>
          <a-icon type="delete" />
          <a-icon type="edit" />
          <!-- <span v-if="record.editable">
          <a @click="() => save(record.key)">Save</a>
          <a-popconfirm title="Sure to cancel?" @confirm="() => cancel(record.key)">
            <a>Cancel</a>
          </a-popconfirm>
        </span>
        <span v-else>
          <a :disabled="editingKey !== ''" @click="() => edit(record.key)">Edit</a>
        </span> -->
        </a-row>
      </template>
    </a-table>
  </div>
</template>
<script>
import IconAlignToTop from "./icon/IconAlignToTop.vue";
import IconSharpSpeed from "./icon/IconSharpSpeed";
const columns = [
  {
    title: "服务器IP",
    dataIndex: "server",
    scopedSlots: { customRender: "server" },
  },
  {
    title: "端口",
    // className: "column-money",
    dataIndex: "port",
  },
  {
    title: "传输协议",
    dataIndex: "protocol",
  },
  {
    title: "国家",
    dataIndex: "country",
  },
  {
    title: "类型",
    dataIndex: "category",
  },
  {
    title: "描述",
    dataIndex: "description",
  },
  {
    title: "操作",
    dataIndex: "operation",
    scopedSlots: { customRender: "operation" },
  },
];

const data = [
  {
    key: "1",
    server: "103.137.61.12",
    port: "233",
    protocol: "vmess",
    country: "Luna",
    category: "buildin",
    description: "aslcdslncasndcasjdcjs",
  },
  {
    key: "2",
    server: "103.137.61.12",
    port: "443",
    protocol: "trojan",
    country: "Luna",
    category: "vip",
    description: "aslcds ncasnd asjdcjs",
  },
  {
    key: "3",
    server: "103.137.61.12",
    port: "443",
    protocol: "trojan",
    country: "Luna",
    category: "vip",
    description: "aslcds ncasnd asjdcjs",
  },
];

export default {
  components: {
    IconAlignToTop,
    IconSharpSpeed,
  },
  data() {
    return {
      data,
      columns,
    };
  },
  methods: {
    updateNodes() {
      console.log("update nodes");
    },
  },
};
</script>
<style>
th.column-money,
td.column-money {
  text-align: right !important;
}
</style>
