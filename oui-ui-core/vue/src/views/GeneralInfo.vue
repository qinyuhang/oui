<template>
  <div>
    <div style="background-color: #ececec; padding: 20px">
      <a-row :gutter="[{ xs: 8, sm: 16 }, 16]">
        <!-- xs sm md lg xl xxl -->
        <a-col
          :span="8"
          :xs="24"
          :md="12"
          :xl="8"
          v-for="card in cards1"
          :key="card.id"
        >
          <a-card
            :title="card.name"
            :bordered="false"
            :headStyle="{
              background: 'rgba(0, 0, 0, 0.15)',
              'font-weight': 'bold',
            }"
          >
            <a-descriptions v-if="card.id == 0" :column="1" :bordered="false">
              <a-descriptions-item
                v-for="item in sysinfo"
                :key="item[0]"
                :label="item[0]"
                >{{ item[1] }}
              </a-descriptions-item>
            </a-descriptions>
            <div v-if="card.id == 1">
              <a-card-grid
                style="width: 25%; text-align: center"
                v-for="i in 4"
                :key="i"
              >
                <a-icon style="font-size: 3em; color: forestgreen">
                  <icon-ethernet-port />
                </a-icon>
                <p>{{ i == 1 ? "W" : "L" }}AN{{ i }}</p>
              </a-card-grid>
            </div>
            <a-row v-if="card.id == 2" type="flex" justify="center">
              <a-col :span="6">
                <a-icon
                  style="font-size: 5em; float: right; padding-right: 8px"
                >
                  <icon-google></icon-google>
                </a-icon>
              </a-col>
              <a-col :span="6">
                <p>谷歌测试</p>
                <a-button type="primary" @click="ping('google.com')">
                  Ping
                </a-button>
              </a-col>
            </a-row>
          </a-card>
        </a-col>
      </a-row>
      <a-row :gutter="[{ xs: 8, sm: 16 }, 16]">
        <!-- xs sm md lg xl xxl -->
        <a-col
          :span="8"
          :xs="24"
          :md="12"
          :xl="8"
          v-for="card in cards2"
          :key="card.id"
        >
          <a-card
            :title="card.name"
            :bordered="false"
            :headStyle="{ 'font-weight': 'bold' }"
          >
            <div v-if="card.id == 0">
              <a-row type="flex" justify="space-around">
                <a-icon style="font-size: 100px; float: left">
                  <icon-router />
                </a-icon>
                <a-icon style="font-size: 100px; float: right">
                  <icon-world />
                </a-icon>
              </a-row>
              <a-row
                type="flex"
                justify="space-around"
                style="margin-bottom: -1em; padding-top: 1em"
              >
                <p>上行: 1024kb</p>
                <p>下行: 1024kb</p>
              </a-row>
            </div>
            <span v-if="card.id == 1" style="text-align: center">
              <p style="font-weight: bold">
                {{ workerMode }}
              </p>
              <div>
                [{{ remote.country }}]{{ remote.ip }}
                <span />
                {{ remote.ping }}
              </div>
            </span>
            <span v-if="card.id == 2" style="text-align: center">
              <p style="font-weight: bold">
                {{ clientNumber }}
              </p>
              <p>连接设备</p>
            </span>
          </a-card>
        </a-col>
      </a-row>
    </div>
  </div>
</template>

<script>
import IconEthernetPort from "./icon/IconEthernetPort";
import IconGoogle from "./icon/IconGoogle";
import IconRouter from "./icon/IconRouter";
import IconWorld from "./icon/IconWorld";
export default {
  components: {
    IconEthernetPort,
    IconGoogle,
    IconRouter,
    IconWorld,
  },
  data() {
    return {
      sysinfo: [],
      cards1: [
        { id: 0, name: "设备信息" },
        { id: 1, name: "接口状态" },
        { id: 2, name: "FQ检测" },
      ],
      cards2: [
        { id: 0, name: "网络连接状态" },
        { id: 1, name: "工作模式" },
        { id: 2, name: "客户端数目" },
      ],
      clientNumber: "??",
      workerMode: "??模式",
      remote: {
        country: "Luna",
        ip: "0.0.0.0",
        ping: "-1ms",
      },
    };
  },
  timers: {
    update: { time: 2000, autostart: true, immediate: true, repeat: true },
  },
  methods: {
    update() {
      this.$system
        .getInfo()
        .then(
          ({
            hostname,
            model,
            system,
            release,
            kernel,
            localtime,
            uptime,
            memory,
          }) => {
            this.sysinfo = [
              // [this.$t("Hostname"), hostname],
              ["设备名称", model],
              ["设备的ID", 233333],
              ["系统版本", release.description],
              // [this.$t("home.Architecture"), system],
              // [this.$t("home.Firmware Version"), release.revision],
              // [this.$t("home.Kernel Version"), kernel],
              //[
              //  this.$t("home.Local Time"),
              //  new Date(localtime * 1000).toString(),
              //],
              //[this.$t("Uptime"), "%t".format(uptime)],
            ];
          }
        );

      this.clientNumber = 23333;
      this.workerMode = "智能模式";
      this.remote = {
        ip: "171.151.161.131",
        country: "美国",
        ping: "83ms",
      };
    },
    ping(url) {
      console.log("ping " + url);
    },
  },
  computed: {},
};
</script>
