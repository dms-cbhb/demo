<template>
  <div id="chart" style="width:100%;height:550px;"></div>
</template>

<script>
import echarts from "echarts";
export default {
  data() {
    return {
      chart: "",
      provRank: null,
      ydata: null
    };
  },
  props: {
    barData: Object
  },
  mounted() {
    // this.load();
  },
  watch: {
    barData(data) {
      this.provRank = data.provRank;
      this.ydata = data.ydata;
      this.load();
    }
  },
  methods: {
    load() {
      let _this = this;
      _this.chart = echarts.init(document.getElementById("chart"));

      var provRank = [
        "杭州",
        "北京",
        "南京",
        "青岛",
        "厦门",
        "宁波",
        "武汉",
        "广州",
        "上海",
        "济南"
      ];
      var option = {
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "shadow"
          },
          formatter: function(objs, index) {
            let obj = objs[0];
            return `${obj.name}<br/>${obj.marker}${obj.seriesName} : ${obj.value} 个`;
          }
        },
        grid: {
          top: "3%",
          left: "3%",
          right: "2%",
          bottom: "3%",
          containLabel: true
        },
        xAxis: {
          type: "value",
          axisTick: {
            show: false
          },
          axisLine: {
            show: false
          },
          axisLabel: {
            show: false
          },
          splitLine: {
            show: false
          }
        },
        yAxis: {
          type: "category",
          boundaryGap: true,
          inverse: true, //反向
          axisLine: {
            show: false
          },
          axisTick: {
            show: true,
            alignWithLabel: true
          },
          // axisLabel: {
          // margin: 18
          // formatter: function(value, index) {
          //   var ind = index + 1;
          //   if (ind == 1) {
          //     return "{a|" + value + "}";
          //   } else if (ind == 2) {
          //     return "{b|" + value + "}";
          //   } else if (ind == 3) {
          //     return "{c|" + value + "}";
          //   } else {
          //     return "{d|" + value + "}";
          //   }
          // }
          // },
          data: _this.provRank
        },
        series: [
          {
            name: "销售量",
            barWidth: 30,
            type: "bar",
            barCategoryGap: 90,
            label: {
              normal: {
                show: true,
                position: "insideRight",
                formatter: "{c}",
                textStyle: {
                  color: "#000"
                }
              }
            },
            // data: [110, 100, 85, 31, 21, 10, 15, 32, 50, 10],
            data: _this.ydata,
            itemStyle: {
              color: "lightblue"
            }
          }
        ]
      };
      _this.chart.setOption(option);
      window.addEventListener("resize", function() {
        _this.chart.resize();
      });
    }
  }
};
</script>

<style scoped></style>
