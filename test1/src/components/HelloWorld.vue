<template>
  <div class="echarts">
    <div id="mapChart" style="width:800px;height: 800px;"></div>
  </div>
</template>
<script>
  //import echarts from "echarts";
  //   import '../../node_modules/echarts/map/js/world.js'
  import '../../node_modules/_echarts@4.2.0-rc.2@echarts/map/js/china.js'
  import '../../node_modules/_echarts@4.2.0-rc.2@echarts/map/js/province/hebei.js' // 引入中国地图数据
  import shijiazhuang from '../../static/json/130100.json'


  export default {
    name: "echarts",
    props: ["userJson"],
    data() {
      return {
        mapList: [ "石家庄"]
      }
    },
    mounted() {
      this.getDownMap();
    },

    methods: {
      getDownMap() {
        let that = this;
        let chart = that.$echarts.init(document.getElementById("mapChart"));
        let name = "河北";
        let option = {

          geo: {
            map: name,
            roam: true,
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
                "name": "长安",
                "coordinates":[0,0]
              }]
            },

          ]
        };

        //下面的事件需要写在上面的getDownMap()里
        chart.on('click', function(params){
         //点击事件写在这里面
          console.log("6666")
        })
        //下面的name需要为“内蒙古”，而不是具体点击的市
        that.$echarts.registerMap(name,shijiazhuang);
        chart.setOption(option);

      }
    }
  }
</script>
