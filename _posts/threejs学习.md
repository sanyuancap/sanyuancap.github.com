# three.js学习

## WebGL是什么

WebGL（全写Web Graphics Library）是一种**3D**绘图协议，这种绘图技术标准允许把**JavaScript和OpenGL ES 2.0**结合在一起，通过增加OpenGL ES 2.0的一个JavaScript绑定，WebGL可以为**HTML5 Canvas**提供硬件3D加速渲染

## WebGL API

三角形是最小平面单位。

 - gl.POINTS
 - gl.LINES
 - gl.TRAIANGLE

## 绘制流程

1. 获取定点坐标（所有三角形的顶点）

三维软件导出，或者框架生成。

存储在显存，方便GPU更快读取。

2. 图源装配（画出一个个三角形）

顶点着色器

3. 光栅化（生成偏远，即一个个像素点）

片元着色器

## three.js

为webgl封装的库

html直接引入

## 模板
```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <style>canvas { width: 100%; height: 100% }</style>
    <script src="js/three.js"></script>
</head>
<body>
    <script>
        //创建一个场景，场景内一开始是不包含任何内容的
        var scene = new THREE.Scene();
        //创建一个相机，这里选择的是透视相机
        var camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
        //创建一个渲染器，处理绘制工作
        var renderer = new THREE.WebGLRenderer();
        //配置绘制区域为浏览器内部显示区域
        renderer.setSize(window.innerWidth, window.innerHeight);
        //把用来绘制内容的元素节点添加到html中
        document.body.appendChild(renderer.domElement);
        //创建一个立方体，这里是长宽高各为1
        var geometry = new THREE.CubeGeometry(1,1,1);
        //为立方体创建材质，这里选择基础材质，基础材质不受光照影响
        var material = new THREE.MeshBasicMaterial({color: 0x00ff00});
        //根据立方体与所选材质生成一个网格mesh，也可以理解为物体对象，它包含了一个可绘制的物体的所有信息
        var cube = new THREE.Mesh(geometry, material); 
        //把立方体对象添加到场景中
        scene.add(cube);
        //设定相机的坐标
        camera.position.z = 5;
        //开始渲染
        function render() {
            requestAnimationFrame(render);
            cube.rotation.x += 0.01;
            cube.rotation.y += 0.01;
            renderer.render(scene, camera);
        }
        render();
    </script>
</body>
</html>
```

## 重点

1. WebGL与canvas：
WebGL是3D绘图协议，它提供的api可以开启GPU加速，可以更好的渲染3D场景及元素。canvas普通的接口只能用cpu来绘制，更适合绘制2d场景。

2. WebGL绘制过程包括以下三步：
1、获取顶点坐标
2、图元装配（即画出一个个三角形）
3、光栅化（生成片元，即一个个像素点）

3. three.js基本结构：
场景，摄像机，光源，物体对象，渲染器。

4. 摄像机中的正交摄像机与透视摄像机区别：
1：可视范围的调整方式不同，正交相机是通过前后左右上下的距离范围来控制的，透视相机是通过视角以及前后距离来控制的
2：透视相机会有近大远小效应，正交相机不会。

5. 相机的up,lookAt,position：
up是相机正上方的朝向，lookAt是相机要观察的方向，position是相机的位置坐标

6. 常见的光源：环境光，点光源，平行光
环境光：场景中的所有物体都会被应用该光源，不用考虑摆放位置
点光源：从一个点向四面八方发射的光源，物体投影会根据相对点光源位置变化而变化
平行光：类似太阳光，可看做从一个平面发射出来的光。

7. 实现鼠标与场景内物体交互的方法及原理：
方法：使用raycaster，且需要鼠标的屏幕坐标转换为threejs标准坐标来使用，标准坐标范围为[-1,1],也就是做一个线性映射。
原理：以相机位置为出发点经过鼠标位置发出射线，判断该射线是否与某物体相交。

8. 世界坐标系：
世界坐标系是以屏幕中心为原点，且采用右手坐标系，X轴方向向右，Y轴向上，Z轴朝着屏幕前的自己。


