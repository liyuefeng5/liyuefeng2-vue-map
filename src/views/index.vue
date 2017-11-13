<template>
  <div id="container">
  </div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted(){
  	this.map();
  },
  methods:{
  	map(){

  		var map = new BMap.Map("container");          // 创建地图实例  
		var point = new BMap.Point(116.344196,39.963113);  // 创建点坐标  
		map.centerAndZoom(point, 15);                 // 初始化地图，设置中心点坐标和地图级别  
		map.enableScrollWheelZoom(true);     //开启鼠标滚轮缩放
		var marker = new BMap.Marker(point);
		map.addOverlay(marker);             //开启标注
		var opts = {
                width : 250,     // 信息窗口宽度
                height: 80,     // 信息窗口高度
                title : "信息窗口" , // 信息窗口标题
                enableMessage:true//设置允许信息窗发送短息
              };
		 var content = '北京中数'           //开启窗口
            map.addOverlay(marker);               // 将标注添加到地图中
            addClickHandler(content,marker);
		 function addClickHandler(content,marker){
            marker.addEventListener("mouseover",function(e){
              openInfo(content,e)}
            );
          };
          function openInfo(content,e){
            var p = e.target;
            var point = new BMap.Point(p.getPosition().lng, p.getPosition().lat);
            var infoWindow = new BMap.InfoWindow(content,opts);  // 创建信息窗口对象
            map.openInfoWindow(infoWindow,point); //开启信息窗口
          };
		//向地图添加控件
          var scaleControl = new BMap.ScaleControl({anchor:BMAP_ANCHOR_BOTTOM_LEFT});
		      scaleControl.setUnit(BMAP_UNIT_IMPERIAL);
		      map.addControl(scaleControl);
		      var navControl = new BMap.NavigationControl({anchor:BMAP_ANCHOR_TOP_LEFT,type:BMAP_NAVIGATION_CONTROL_LARGE});
		      map.addControl(navControl);
		      var overviewControl = new BMap.OverviewMapControl({anchor:BMAP_ANCHOR_BOTTOM_RIGHT,isOpen:true});
		      map.addControl(overviewControl);
		  },
  }
}
</script>

<style scoped>
		html{height:100%}  
        body{height:100%;margin:0px;padding:0px}  
        #container{height: 500px;width: 100%;}  
</style>
