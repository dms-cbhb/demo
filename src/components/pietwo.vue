<template>
  <div id="pietwo" style="width:100%;height:550px"></div>
</template>

<script>
import echarts from "echarts";

export default {
  data() {
    return {
      pietwo: "",
      piedata: null
    };
  },
  props: {
    pietwoData: Array
  },
  watch: {
    pietwoData(data) {
      this.piedata = data;
      this.load();
    }
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      let _this = this;
      _this.pietwo = echarts.init(document.getElementById("pietwo"));

      var option = {
        title: {
          text: "天气情况统计",
          subtext: "虚构数据",
          left: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "horizontal",
          left: "center",
          bottom: "20",
          icon: "circle"
        },
        series: [
          {
            type: "pie",
            radius: "65%",
            center: ["50%", "50%"],
            selectedMode: "single",
            // data: [
            //   { value: 1548, name: "幽州" },
            //   { value: 535, name: "荆州" },
            //   { value: 510, name: "兖州" },
            //   { value: 634, name: "益州" },
            //   { value: 735, name: "西凉" }
            // ],
            data: _this.piedata,
            emphasis: {
              itemStyle: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: "rgba(0, 0, 0, 0.5)"
              }
            }
          }
        ]
      };

      _this.pietwo.setOption(option);
    }
  }
};
</script>

<style scoped></style>
