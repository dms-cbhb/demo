<template>
  <div>
    <div ref="round" style="width:100%;height:350px"></div>
  </div>
</template>

<script>
import echarts from "echarts";
export default {
  name: "round",
  data() {
    return {
      round: "",
      pieData: null
    };
  },
  props: {
    roundData: Object
  },
  mounted() {
    // this.loadchart();
  },
  watch: {
    roundData(data) {
      console.log(data);
      this.pieData = data.pieData;
      this.loadchart();
    }
  },
  methods: {
    loadchart() {
      let _this = this;
      _this.round = echarts.init(this.$refs.round);

      var option = {
        tooltip: {
          trigger: "item",
          formatter: "{b}: {c} ({d}%) "
        },
        legend: {
          orient: "horizontal",
          left: "center",
          bottom: "20",
          icon: "circle"
          // data: ["直接访问", "邮件营销", "联盟广告", "视频广告", "搜索引擎"]
        },
        series: [
          {
            name: "访问来源",
            type: "pie",
            radius: ["50%", "70%"],
            avoidLabelOverlap: false,
            label: {
              show: true,
              position: "outside",
              formatter: function(val) {
                return "111";
              }
            },
            emphasis: {
              label: {
                show: true,
                fontSize: "30",
                fontWeight: "bold"
              }
            },
            labelLine: {
              show: false
            },
            // data: [
            //   { value: 335, name: "直接访问" },
            //   { value: 310, name: "邮件营销" },
            //   { value: 234, name: "联盟广告" },
            //   { value: 135, name: "视频广告" },
            //   { value: 1548, name: "搜索引擎" }
            // ]
            data: _this.pieData
          }
        ]
      };
      _this.round.setOption(option);

      window.addEventListener("resize", function() {
        _this.round.resize();
      });
    }
  }
};
</script>

<style></style>
