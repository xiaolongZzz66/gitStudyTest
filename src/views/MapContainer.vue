<template>
  <div class="home_div">
    <div class="map-title">
      <h3>JSAPI Vue3地图组件示例</h3>
    </div>
    <div id="container"></div>
  </div>
</template>
<script>
// 新版本需要加jscode
window._AMapSecurityConfig = {
  securityJsCode: "30322e34b1a987d1b29026a450bc835d",
};
import AMapLoader from "@amap/amap-jsapi-loader";
import { shallowRef } from "@vue/reactivity";
export default {
  name: "mapcomtaint",
  setup() {
    const map = shallowRef(null);
    return {
      map,
    };
  },
  create() {},
  methods: {
    ininMap() {
      AMapLoader.load({
        key: "bb22c2b1e7a58db6707669a57c1c2b62", //设置您的key
        version: "2.0",
        plugins: ["AMap.ToolBar", "AMap.Driving", "'AMap.Driving'"],
        AMapUI: {
          version: "1.1",
          plugins: [],
        },
        Loca: {
          version: "2.0.0",
        },
      })
        .then((AMap) => {
          // 创建地图对象实例
          this.map = new AMap.Map("container", {
            viewMode: "3D",
            terrain: true, //地形图开启
            pitch: 55, // 地图俯仰角度，有效范围 0 度- 83 度
            zoom: 5,
            zooms: [2, 22],
            center: [105.602725, 37.076636],
          });

          // 创建多个点标记
          let positionArr = [
            [113.357224, 34.977186],
            [114.555528, 37.727903],
            [112.106257, 36.962733],
          ];
          for (let item of positionArr) {
            let marker = new AMap.Marker({
              position: [item[0], item[1]],
            });
            this.map.add(marker);
          }

          // 路线规划
          var driving = new AMap.Driving({
            // 驾车路线规划策略，AMap.DrivingPolicy.LEAST_TIME是最快捷模式
            policy: AMap.DrivingPolicy.LEAST_TIME,
          });
          var startLngLat = [116.379028, 39.865042];
          var endLngLat = [116.427281, 39.903719];
          driving.search(startLngLat, endLngLat, function (status, result) {
            // 未出错时，result即是对应的路线规划方案
            console.log("search--------------------", status, result);
          });

          // 创建折线实例
          // 折线的节点坐标数组，每个元素为 AMap.LngLat 对象
          var path = [
            new AMap.LngLat(116.368904, 39.913423),
            new AMap.LngLat(116.382122, 39.901176),
            new AMap.LngLat(116.387271, 39.912501),
            new AMap.LngLat(116.398258, 39.9046),
          ];
          var polyline = new AMap.Polyline({
            path: path,
            borderWeight: 9, // 线条宽度，默认为 1
            strokeColor: "red", // 线条颜色
            lineJoin: "round", // 折线拐点连接处样式
          });
          // 将折线添加至地图实例
          this.map.add(polyline);

          // 信息窗体
          var content = [
            "<div><b>高德软件有限公司</b>",
            "电话 : 010-84107000   邮编 : 100102",
            "地址 : 北京市望京阜通东大街方恒国际中心A座16层</div></div>",
          ];
          // 创建 infoWindow 实例
          var infoWindow = new AMap.InfoWindow({
            content: content.join("<br>"), //传入 dom 对象，或者 html 字符串
          });
          // 打开信息窗体
          infoWindow.open(this.map);


        })
        .catch((e) => {
          console.log(e);
        });
    },
    // 测试冲突1，都有改动
    test() {},
    addMarker() {},
    // 测试冲突2,都有改动
    test2() {},
    // 测试冲突3,只有本账户有新增，另一个账户没有新增
    test3() {},
  },
  mounted() {
    //DOM初始化完成进行地图初始化
    this.ininMap();
  },
};
</script>
<style scope>
.home_div {
  height: 100%;
  width: 100%;
  padding: 0px;
  margin: 0px;
  position: relative;
}
#container {
  height: 100%;
  width: 100%;
  padding: 0px;
  margin: 0px;
}
.map-title {
  position: absolute;
  z-index: 1;
  width: 100%;
  height: 50px;
  background-color: rgba(27, 25, 27, 0.884);
}
h3 {
  position: absolute;
  left: 10px;
  z-index: 2;
  color: white;
}
</style>
