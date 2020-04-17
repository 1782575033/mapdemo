<template>
  <div>
    <Header />
    <Search v-if="userdata" :userdata="userdata" @search="search" />
    <LocationCart v-if="cardshow" :mapdata="mapdata" />
    <div id="container"></div>
  </div>
</template>
<script type="text/javascript" src="https://webapi.amap.com/maps?v=1.4.15&key=d8770b51ad1eca779dcb8f98bb6ced51"></script> 
<script>
var map = null;
import Header from "../components/Header";
import Search from "../components/Search";
import LocationCart from "../components/LocationCart";
export default {
  data() {
    return {
      mapdata: [],
      userdata: [],
      cardshow: false
    };
  },
  components: {
    Header,
    Search,
    LocationCart
  },
  created() {
    this.$axios({
      methods: "get",
      url: "http://www.mocky.io/v2/5e87e6c731000024303f4780"
    }).then(res => {
      if (res.status === 200) {
        this.userdata = res.data.data;
        console.log(this.userdata);
      }
    });
  },
  mounted() {
    this.setCenter(116.481181, 39.989792);
  },
  methods: {
    getLoc() {
      this.$axios({
        methods: "get",
        url: "http://www.mocky.io/v2/5e87e70031000025303f4781"
      }).then(res => {
        if (res.status === 200) {
          this.mapdata = res.data.data;
          console.log(this.mapdata);
          this.setCenter(this.mapdata[0].lng, this.mapdata[0].lat, null);
          this.mapdata.forEach((item,index) => {
            this.addMark(item.lng, item.lat, item.location,index);
          });
        }
      });
    },
    setCenter(lng, lat) {
      map = new AMap.Map("container", {
        zoom: 15, //级别
        center: [lng, lat] //中心点坐标
        //viewMode: "3D" 使用3D视图
      });
    },
    addMark(lng, lat, content,index) {
      var infoWindow = new AMap.InfoWindow({
        //创建信息窗体
        isCustom: false, //使用自定义窗体
        content: `<div>${content}</div>`, //信息窗体的内容可以是任意html片段
        offset: new AMap.Pixel(16, -45)
      });
      var onMarkerClick = function(e) {
        infoWindow.open(map, e.target.getPosition()); //打开信息窗体
        //e.target就是被点击的Marker
      };
      let content2 = `<div class="pos-tip"><i class="iconfont icon-weizhi1 "></i><span>${index+1}</span><div>`;
      var marker = new AMap.Marker({
        position: [lng, lat], //位置
         content: content2,  // 自定义点标记覆盖物内容
        offset: new AMap.Pixel(-17, -42) // 相对于基点的偏移位置
      });
      map.add(marker); //添加到地图
      marker.on("click", onMarkerClick); //绑定click事件
    },
    search() {
      this.cardshow = true;
      this.getLoc();
    }
  }
};
</script>
<style>
#container {
  min-width: 600px;
  min-height: calc(100vh - 66px);
}
.pos-tip{
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}
.pos-tip i{
  position: absolute;
  display: inline-block;
  font-size: 30px!important;
  color: #2878d2;
}
.pos-tip span{
  display: inline-block;
  top: -11px;
  font-size: 12px;
  position: absolute;
  color: #2878d2;
}
</style>