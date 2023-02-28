# AILabel.js
背景：在前端开发过程中难免遇到针对图片的缩放平移；以及在图片上进行矢量数据、文本、标注的展示；如果你有上面的任何需求，恭喜你，找到组织了....<br/>
在此背景下，AILabel.js出生了

### 相关资料

npm下载地址：[https://www.npmjs.com/package/ailabel](https://www.npmjs.com/package/ailabel)<br/>
github地址:  [https://github.com/dingyang9642/AILabel](https://github.com/dingyang9642/AILabel)<br/>
api文档(待补充):  [https://dingyang9642.github.io/AILabel/#/](https://dingyang9642.github.io/AILabel/#/)<br/>


### 背景-功能

> 1. 解决图片浏览（无极缩放、平移）
> 2. 矢量数据、文本、标注展示
> 3. 矢量数据绘制、编辑
> 4. 标注形式：矩形、多边形、涂抹、折线、打点、文本text、标注marker

### 示例图
<img width="350" src="https://raw.githubusercontent.com/dingyang9642/AILabel/master/docs/files/point.gif"><img width="350" src="https://raw.githubusercontent.com/dingyang9642/AILabel/master/docs/files/polyline.gif"><img width="350" src="https://raw.githubusercontent.com/dingyang9642/AILabel/master/docs/files/rect.gif"><img width="350" src="https://raw.githubusercontent.com/dingyang9642/AILabel/master/docs/files/polygon.gif"><img width="350" src="https://raw.githubusercontent.com/dingyang9642/AILabel/master/docs/files/mask.gif">

### 示例Demo

  [- 要素](http://www.gdbox.vip/gdbox/demo/feature)<br/>
  [- 注记](http://www.gdbox.vip/gdbox/demo/marker)<br/>
  [- 文本](http://www.gdbox.vip/gdbox/demo/text)<br/>
  [- 绘制编辑](http://www.gdbox.vip/gdbox/demo/drawFeature)<br/>
  [- 矩形编辑](http://www.gdbox.vip/gdbox/demo/editRect)<br/>
  [- 要素hover](http://www.gdbox.vip/gdbox/demo/hover)<br/>
  [- 图像&缩略图&比例尺](http://www.gdbox.vip/gdbox/demo/img)<br/>

### get started

html\css\js部分
```javascript
    // 样式声明
    <style>
        #hello-map {
            width: 500px;         // 必须
            height: 400px;        // 必须
            position: relative;   // 必须
            border: 1px solid red;
            cursor: pointer;
        }
    </style>

    // 容器声明
    <div id="hello-map"></div>

    // js声明-容器声明（参数：zoom: 缩放比; {cx: cy:}：初始中心点位置；zoomMax、zoomMin：缩放的比例限制）
    const gMap = new AILabel.Map('hello-map', {zoom: 1080, cx: 0, cy: 0, zoomMax: 650 * 10, zoomMin: 650 / 10, autoPan: true, drawZoom: true});

    // 图片层实例\添加
    const gImageLayer = new AILabel.Layer.Image('img', '../../imgs/demo.jpeg', {w: 1080, h: 720}, {zIndex: 1});
    gMap.addLayer(gImageLayer);

    ***至此、已完成首个简单的hello-map的使用***
```

### 矢量数据(Feture)展示
```javascript
    // 常用样式声明
    const gFetureStyle = new AILabel.Style({strokeColor: '#0000FF'});

    // 矢量层实例\添加
    let gFeatureLayer = new AILabel.Layer.Feature('featureLayer', {zIndex: 2, transparent: true});
    gMap.addLayer(gFeatureLayer);

    // 矢量要素实例\添加
    const fea = new AILabel.Feature.Polygon('id', [
        {x: 10, y: 10},
        {x: 50, y: 10},
        {x: 40, y: 50},
        {x: 20, y: 60},
        {x: 10, y: 10}
    ], {name: '中国'}, gFetureStyle);
    gFeatureLayer.addFeature(fea);
```

### 文本数据(Text)展示
```javascript
    // 常用样式声明
    const gTextStyle = new AILabel.Style({strokeColor: '#0000FF'});

    // 文本层实例\添加
    let gTextLayer = new AILabel.Layer.Text('textLayer', {zIndex: 2});
    gMap.addLayer(gTextLayer);

    // 文本要素实例\添加
    const text = new AILabel.Text('id', {
        pos: {x: 100, y: 100},
        offset: {x: 0, y: 0},
        width: 100,
        text: '中国'
    }, gTextStyle);
    gTextLayer.addText(text);
```

### 标注数据(Marker)展示
```javascript
    // 不需要声明markerLayer标注图层，有且只有一个markerLayer，可通过gMap.mLayer来获取
    // marker对象实例\添加
    const marker = new AILabel.Marker('name-中国', {
        src: './marker.png',
        x: 0,
        y: 0,
        offset: {x: -32, y: -32}
    });
    // 注册监听事件删除标注
    marker.regEvent('click', function () {
        gMap.mLayer.removeMarker(this);
    });
    gMap.mLayer.addMarker(marker);
```

### 各类事件监听（mouse、hover、boundsChanged、resize等各类事件）
```javascript
// mouseDown：wxy => {}
// mouseMove：wxy => {}
// geometryEditing：(type, feature, newPoints) => {}
// geometryEditDone：(type, feature, newPoints) => {}
// geometryDrawDone：(type, points) => {}
// geometryRemove: (type, feature) => {} 【目前只针对点数据】
// featureHover：feature => {}
// featureSelected：feature => {}
// featureStatusReset：() => {}
// boundsChanged() => {}
// resize() => {}
gMap.events.on('mouseDown', xy => {console.log('xy');});
gMap.events.on('boundsChanged', () => {console.log('boundsChanged');});
gMap.events.on('featureHover', feature => {console.log(feature);});
...

```

### 矢量数据绘制、编辑（点、线、面、涂抹Mask）
```
    // 常用样式声明
    const gFetureStyle = new AILabel.Style({strokeColor: '#0000FF'});

    // 设置当前操作模式为‘drawRect’, 浏览状态对应mode为'pan'
    gMap.setMode('drawRect', gFetureStyle);

    // 矢量层实例\添加
    let gFeatureLayer = new AILabel.Layer.Feature('featureLayer', {zIndex: 2, transparent: true});
    gMap.addLayer(gFeatureLayer);

    // 绘制完成事件监听
    gMap.events.on('geometryDrawDone', function (type, points) {
        // 生成元素唯一标志（时间戳）
        const timestamp = new Date().getTime();
        // 元素添加展示
        let fea = new AILabel.Feature.Polygon(`feature-${timestamp}`, points, {
            name: '中国'
        }, gFetureStyle);
        gFeatureLayer.addFeature(fea);
    });
    // 因为自带编辑功能，故需要以下代码
    gMap.events.on('geometryEditDone', (type, activeFeature, points) => {
        activeFeature.update({points});
        activeFeature.show();
    });
```

如有其他需要，加入qq群：378301400
