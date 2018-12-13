<template>
    <div class="test">
        <div id="myechart" style="width:800px;height: 800px;"></div>
    </div>
</template>
<script>
 import '../../node_modules/_echarts@4.2.0-rc.2@echarts/map/js/china.js'
 import '../../node_modules/_echarts@4.2.0-rc.2@echarts/map/js/province/shanxi.js' // 引入中国地图数据
  import shanxijson from '../../node_modules/_echarts@4.2.0-rc.2@echarts/map/json/province/shanxi.json'
 export default {
    name: "echarts",
    props: ["userJson"],
    data() {
      return {
        mapList: [ "山西"]
      }
    },
    mounted() {
      this.getDownMap();
    },

    methods: {
      getDownMap() {
        // let that = this;
        let chart = this.$echarts.init(document.getElementById("myechart"));
        let name = "山西";
        let option = {

          geo: {
            map: name,
            roam: true,//控制地图的缩放
            layoutCenter: ['30%', '30%'],//地图的位置
            layoutSize: 500,//地图的大小
            label: {
              normal: {
                show: true,
                textStyle: {
                  color: '#8b4513',//地区颜色
                  fontSize: 15
                }
              },
              emphasis: {
                textStyle: {
                  color: 'red'//浮动在某个地区的字体颜色
                }
              }
            },
            itemStyle: {
              normal: {
                borderColor: 'red',//每个区之间边框的颜色
                borderWidth: 1,
                areaColor: {//背景色
                  type: 'radial',
                 x: 0.5,
                  y: 0.5,
                  r: 0.8,
                  colorStops: [{
                    offset: 0,
                    color: 'green' // 0% 处的颜色
                  }, {
                    offset: 1,
                    color: 'yellow' // 100% 处的颜色
                  }],
                  globalCoord: false // 缺省为 false
                },
               /* shadowColor: 'rgba(128, 217, 248, 1)',
                shadowOffsetX: -2,
                shadowOffsetY: 2,
                shadowBlur: 10*/
              },
              emphasis: {
                areaColor: 'yellow',//鼠标浮动在某个地区显示的颜色
                borderWidth: 0
              }
            },
          },
          series: [
            {
              type: 'effectScatter',
              coordinateSystem: 'geo',
              data:[{
                "name": "山西",
                "coordinates":[0,0]
              }]
            },

          ]
        };

      
        //下面的name需要为“内蒙古”，而不是具体点击的市
        this.$echarts.registerMap(name,shanxijson);
        chart.setOption(option);

      }
    }
  }
</script>
<style>


</style>


