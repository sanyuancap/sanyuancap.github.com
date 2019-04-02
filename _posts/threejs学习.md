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

