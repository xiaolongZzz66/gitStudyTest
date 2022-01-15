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
        securityJsCode:'30322e34b1a987d1b29026a450bc835d',
    }
import AMapLoader from "@amap/amap-jsapi-loader"
import { shallowRef } from '@vue/reactivity'
export default {
    name:"mapcomtaint",
    setup(){
        const map = shallowRef(null);
        return{
            map,
        }

    },
    create(){

    },
    methods:{
        ininMap(){
            AMapLoader.load({
                key:'bb22c2b1e7a58db6707669a57c1c2b62',  //设置您的key
                version:"2.0",
                plugins:['AMap.ToolBar','AMap.Driving'],
                AMapUI:{
                    version:"1.1",
                    plugins:[],

                },
                Loca:{
                    version:"2.0.0"
                },
            }).then((AMap)=>{
                this.map = new AMap.Map("container",{
                    viewMode:"3D",
                    zoom:5,
                    zooms:[2,22],
                    center:[105.602725,37.076636],
                });
                let positionArr = [
                    [113.357224,34.977186],
                    [114.555528,37.727903],
                    [112.106257,36.962733],
                    [109.830097,31.859027],
                    [116.449181,39.98614],
                ];
                for(let item of positionArr){
                    let marker = new AMap.Marker({
                        position:[item[0],item[1]],
                    });
                    this.map.add(marker);
                }


            }).catch(e=>{
                console.log(e);
            })
        },
        addMarker(){
            
        }
    },
    mounted(){
        //DOM初始化完成进行地图初始化
        this.ininMap();
    }
}
</script>
<style scope>
    .home_div{
        height: 100%;
        width: 100%;
        padding: 0px;
        margin: 0px;
        position: relative;
    }
    #container{
        height: 100%;
        width: 100%;
        padding: 0px;
        margin: 0px;
    }
    .map-title{
         position:absolute;
         z-index: 1;
         width: 100%;
         height: 50px;
         background-color: rgba(27, 25, 27, 0.884);

    }
    h3{
        position:absolute;
        left: 10px;
        z-index: 2;
        color: white;
    }



</style>