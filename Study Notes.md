1、OpenLayers 3 之 动态点扩散效果

   当某个地方发生一些事情之后，如果我们添加一个静态点在地图上，并不能引起注意，那我们可以放置一个动态的点，类似于在水中投入一个石头，水波扩散的效果，象征发生的事件有一定的影响区域，那么，我们如何利用 OpenLayers3 做出这样的效果呢？我们要实现的效果如下图，之前雅安发生过地震，我们在雅安放置一个这样的点，表示雅安发生了地震。
   
   ol.Overlay
   
   首先，创建一个 DIV 元素，将其形状限制为圆形，并使用 CSS3 为其赋予动画：
   
   首先，创建一个 DIV 元素，将其形状限制为圆形，并使用 CSS3 为其赋予动画：

HTML 元素

<div id="css_animation"></div>

CSS3 动画及其样式

<style>
    #css_animation{
        height:50px; 
        width:50px;
        border-radius: 25px; 
        background: rgba(255, 0, 0, 0.9);

        transform: scale(0);
        animation: myfirst 3s;      
        animation-iteration-count: infinite;
    }

    @keyframes myfirst{
        to{
            transform: scale(2);
            background: rgba(0, 0, 0, 0);
        }
    }
  </style>
  
  接下来，我们创建一个 overlay 实例，将这个 HTML 元素添加到 overlay 中：

    var point_div = document.getElementById("css_animation");
    var point_overlay = new ol.Overlay({
        element: point_div,
        positioning: 'center-center'
    });
map.addOverlay(point_overlay);
point_overlay.setPosition([11468382.41282299,3502038.887913635]);
我们来解释这段代码：首先，var point_div = document.getElementById("css_animation");获得具有动画效果的HTML元素；然后将其赋予 overlay 的 element 参数，overlay 还有一个参数是 positioning: 'center-center'，表示 HTML 元素相对于 overlay 的定位点的方位，”center-center” 表示元素中心对准定位点中心；最后 map.addOverlay(point_overlay); 将 overlay 添加到地图中，此时的 overlay 是不可见的，最后一行：point_overlay.setPosition([11468382.41282299,3502038.887913635]);设置了 overlay 可见元素（也就是具有动画的元素）的位置，这样动画元素就设置到相应的点了。

这样，我们就实现了原来文章开头的效果。
