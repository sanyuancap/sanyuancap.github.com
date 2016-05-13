

var drawLineArray = [cc.p(tempBottomPosX,-100),cc.p(tempTopPosX,1060)];
var drawNode = new cc.DrawNode();//创建draw对象，画点，线段，多边形
this.addChild(drawNode);              //加入Layer层
drawNode.clear();                      //清除节点缓存
drawNode.ctor();                       //构造函数
drawNode.drawCardinalSpline(drawLineArray, 0.5, 50, 2, cc.color(255, 255, 255, 255));    //曲线
//参数说明:
//congfig:点数组
//tension:张力
//segments:段落
//lineWidth:线条宽度
//color:颜色
// draw.drawCardinalSpline(vertices4, 0.5, 100, 2, cc.color(255, 255, 255, 255));

drawNode.drawCubicBezier(origin, control1, control2, destination, segments, lineWidth, color)  //画三次贝塞尔曲线
//drawNode.drawCubicBezier(cc.p(s.width - 250, 40), cc.p(s.width - 70, 100), cc.p(s.width - 30, 250), cc.p(s.width - 10, s.height - 50),10,1, cc.color(0, 1, 0, 1));
drawNode.drawQuadBezier(origin, control, destination, segments, lineWidth, color)          //画二次贝塞尔曲线 参考三次贝塞尔曲线


//for test
var drawNode = new cc.DrawNode();//创建draw对象，画点，线段，多边形
this.addChild(drawNode);              //加入Layer层
drawNode.clear();                      //清除节点缓存
drawNode.ctor();                       //构造函数
drawNode.drawQuadBezier(
    cc.p(100,100),
    cc.p(300,800),
    cc.p(500,100),
    10, 2, cc.color(255,255,255,255));


    