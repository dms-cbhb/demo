<template>
  <div id="pie" style="width:100%;height:550px"></div>
</template>

<script>
import echarts from "echarts";

export default {
  data() {
    return {
      pie: "",
      echartData: null
    };
  },
  props: {
    pieData: Array
  },
  watch: {
    pieData(data) {
      this.echartData = data;
      this.load();
    }
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      let _this = this;
      _this.pie = echarts.init(document.getElementById("pie"));

      let bgColor = "#fff";
      let title = "总量";
      let color = [
        "#0E7CE2",
        "#FF8352",
        "#E271DE",
        "#F8456B",
        "#00FFFF",
        "#4AEAB0"
      ];
      // let echartData = [
      //   {
      //     name: "A类",
      //     value: "3720"
      //   },
      //   {
      //     name: "B类",
      //     value: "2920"
      //   },
      //   {
      //     name: "C类",
      //     value: "2200"
      //   },
      //   {
      //     name: "D类",
      //     value: "1420"
      //   }
      // ];

      let formatNumber = function(num) {
        let reg = /(?=(\B)(\d{3})+$)/g;
        return num.toString().replace(reg, ",");
      };
      let total = _this.echartData.reduce((a, b) => {
        return a + b.value * 1;
      }, 0);

      var option = {
        // backgroundColor: bgColor,
        // 图的颜色
        color: color,
        legend: {
          orient: "horizontal",
          left: "center",
          bottom: "20",
          icon: "circle"
        },
        // tooltip: {
        //   trigger: "item"
        // },
        title: [
          {
            text: "{name|" + title + "}\n{val|" + formatNumber(total) + "}",
            top: "center",
            left: "center",
            textStyle: {
              rich: {
                name: {
                  fontSize: 14,
                  fontWeight: "normal",
                  color: "#666666",
                  padding: [10, 0]
                },
                val: {
                  fontSize: 20,
                  fontWeight: "bold",
                  color: "#333333"
                }
              }
            }
          }
        ],

        series: [
          {
            type: "pie",
            radius: ["45%", "60%"],
            center: ["50%", "50%"],
            data: _this.echartData,
            hoverAnimation: false,
            itemStyle: {
              normal: {
                borderColor: bgColor,
                borderWidth: 2
              }
            },
            labelLine: {
              normal: {
                length: 25,
                length2: false
              }
            },
            label: {
              normal: {
                color: "#000",
                formatter: `{d}%`
                // padding: [0, -100, 25, -100]
              }
            }
          }
        ]
      };
      _this.pie.setOption(option);
    }
  }
};
</script>

<style scoped></style>
