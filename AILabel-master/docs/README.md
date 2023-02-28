# 概述
在前端开发过程中难免遇到针对图片的缩放平移；以及在图片上进行矢量数据、文本、标注的展示； 如果你有上面的任何需求，恭喜你，找到组织了....在此背景下，AILabel.js诞生了

--------
## 特性
> 1. 多类型要素展示：图片/矢量数据/文本/标注
> 2. 高效绘图：canvas矢量数据绘制
> 3. 使用方便简单 ✨✨✨✨✨

## 名词解释
1. zoom：容器宽代表的实际距离宽
2. 实际坐标系：要素或实体代表的实际坐标值所在的坐标系
3. 屏幕标注系：用来展示的坐标系
4. ...

## 授权
....

--------
# 快速入门
[快速入门](https://dingyang9642.github.io/AILabel/#/texts/abstract)<br/>

--------
# 示例图片

<img width="350" src="https://raw.githubusercontent.com/dingyang9642/AILabel/master/docs/files/point.gif"><img width="350" src="https://raw.githubusercontent.com/dingyang9642/AILabel/master/docs/files/polyline.gif"><img width="350" src="https://raw.githubusercontent.com/dingyang9642/AILabel/master/docs/files/rect.gif"><img width="350" src="https://raw.githubusercontent.com/dingyang9642/AILabel/master/docs/files/polygon.gif"><img width="350" src="https://raw.githubusercontent.com/dingyang9642/AILabel/master/docs/files/mask.gif">


## 示例demo
<h5>综合示例</h5>

  [- 绘制编辑](http://www.gdbox.vip/gdbox/demo/drawFeature)<br/>

<h5>其他示例</h5>

  [- 要素](http://www.gdbox.vip/gdbox/demo/feature)<br/>
  [- 注记](http://www.gdbox.vip/gdbox/demo/marker)<br/>
  [- 文本](http://www.gdbox.vip/gdbox/demo/text)<br/>
  [- 矩形编辑](http://www.gdbox.vip/gdbox/demo/editRect)<br/>
  [- 要素hover](http://www.gdbox.vip/gdbox/demo/hover)<br/>
  [- 图像&缩略图&比例尺](http://www.gdbox.vip/gdbox/demo/img)<br/>

--------
# AILabel.Map
## 实例化
```javascript
// js: 伪代码
const gMap = new AILabel.Map(containerId, config);
// js: demo【gMap将作为后续使用的容器实例，不再进行重复实例操作】
const gMap = new AILabel.Map('map', {zoom: 640, cx: 0, cy: 0, zoomMax: 650 * 10, zoomMin: 650 / 10,  autoPan: true, drawZoom: true});
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|containerId|Dom容器id|是|--|string|
|config|其他配置项|是|--|Config|

<h4>Config</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|zoom|初始缩放级别|是|--|number|
|cx|初始中心点坐标x|是|--|number|
|cy|初始中心点坐标y|是|--|number|
|zoomMax|缩放最大级别|否|无极|number|
|zoomMin|缩放最小级别|否|无极|number|
|autoPan|绘制过程中是否禁止自动平移|否|true|bool|
|drawZoom|绘制过程中是否禁止滑轮缩放|否|true|bool|
|autoFeatureSelect|默认是否双击选中feature|否|true|bool|

## 事件
AILabel.Map支持各类事件监听。
```javascript
// js: 伪代码
gMap.events.on(eventType, callback);
// js: demo
gMap.events.on('mouseDown', xy => {console.log('xy');});
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|eventType|如下|是|--|string|
|callback|mouseDown：wxy => {}<br/>mouseMove：wxy => {}<br/>geometryEditing：(type, feature, newPoints) => {}<br/>geometryEditDone：(type, feature, newPoints) => {}<br/>geometryDrawDone：(type, points) => {}<br/>featureHover：feature => {}<br/>featureWillSelected：feature => {}<br/>featureSelected：feature => {}<br/>featureStatusReset：() => {}<br/>boundsChanged() => {}<br/>resize() => {}|是|--|function|

## 快捷键
|快捷键|作用|其他
|---|---|---|
|ctrl_z|绘制过程中撤销操作|--|

## addLayer
给gMap实例上添加图层。
```javascript
// js: 伪代码
const gFeatureLayer = new AILabel.Layer.Feature(layerId, config); // 请参考AILabel.Layer.Feature【此处不做赘述】
gMap.addLayer(gFeatureLayer); // 图层添加
```

## removeLayer
给gMap实例上移除图层。
```javascript
// js: 伪代码
const gFeatureLayer = new AILabel.Layer.Feature(layerId, config); // 请参考AILabel.Layer.Feature【此处不做赘述】
gMap.addLayer(gFeatureLayer); // 图层添加
gMap.removeLayer(gFeatureLayer); // 图层移除
```

## getAllLayers
获取gMap实例上所有图层。
```javascript
gMap.getAllLayers(); // 返回[](layer)
```

## getZoom
获取gMap实例当前缩放zoom值。
```javascript
gMap.getZoom();
```

## setZoom
设置gMap实例zoom值。
```javascript
gMap.setZoom(zoom);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|zoom|缩放值|是|--|number|

## zoomIn
gMap实例放大。
```javascript
gMap.zoomIn(num);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|num|越大代表缩放的范围越大|否|6|number|

## zoomOut
gMap实例缩小。
```javascript
gMap.zoomOut(num);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|num|越大代表缩放的范围越大|否|6|number|

## setMode
gMap实例设置当前模式，同时可设置当前style样式。
```javascript
gMap.setMode(mode[, gStyle]);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|mode|'pan': 浏览模式<br/>'drawRect': 矩形绘制<br/>'drawPolygon': 多边形绘制<br/>'drawPoint':  绘制点<br/>'drawPolyline': 多段线绘制<br/>'drawMask': 涂抹绘制<br/>'clearMask': 涂抹清除<br/>'banMap': 禁止平移缩放|是|--|string|
|gStyle|AILabel.Style|否|--|参考AILabel.Style|

## getMode
获取gMap实例当前模式。
```javascript
gMap.getMode();
```

## setCenter
gMap实例设置中心点坐标。
```javascript
gMap.setCenter(cx, cy);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|cx|x坐标|是|--|number|
|cy|y坐标|是|--|number|

## centerAndZoom
gMap实例设置中心点坐标并且缩放至指定值。
```javascript
gMap.centerAndZoom(center, zoom);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|center|中心点坐标|是|--|object|
|zoom|缩放值|是|--|number|

## getCenter
获取中心点。
```javascript
gMap.getCenter();
```

## getScreenCenter
获取屏幕中心点坐标。
```javascript
gMap.getScreenCenter();
```

## tipLayer.showTips
编辑tip提示开关
```javascript
gMap.tipLayer.showTips(); // 打开tip提示
```

## tipLayer.hideTips
编辑tip提示开关
```javascript
gMap.tipLayer.hideTips(); // 关闭tip提示
```

## resize
gMap实例resize【此方法不建议使用】。
```javascript
gMap.resize(w, h);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|w|宽度|是|--|number|
|h|高度|是|--|number|

## destroy
gMap实例销毁。
```javascript
gMap.destroy();
```

--------
# AILabel.Layer.Image
## 实例化
图像层实例化。
```javascript
const imageLayer = new AILabel.Layer.Image(layerId, src, size, config);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|layerId|实例图层唯一标志id|是|--|string|
|src|图像src|是|--|string|
|size|图像原始宽高|是|--|图片大小，如{w: 100, h: 100}|
|config|其他配置项|否|--|Config|

<h4>Config</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|zIndex|同css中zIndex|否|2|number|
|grid|辅助网格配置项|否|false|Grid|

<h4>Grid</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|rowCount|行数|是|--|number|
|columnCount|列数|是|--|number|
|color|网格颜色-十六进制|否|#000000|string|

## update
图像层相关更新【暂时只支持辅助网格更新】。
```javascript
const imageLayer = new AILabel.Layer.Image(layerId, src, size, config);
imageLayer.update({grid: Grid});
imageLayer.update({grid: false}); // 删除网格
```

## renew
刷新。
```javascript
const imageLayer = new AILabel.Layer.Image(layerId, src, size, config);
imageLayer.renew();
```

--------
# AILabel.Layer.Feature
## 实例化
矢量数据层【矢量数据点/线/面展示层】。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|layerId|实例图层唯一标志id|是|--|string|
|config|其他配置项|否|--|Config|

<h4>Config</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|opacity|透明度0-1|否|1|number|
|zIndex|同css中zIndex|否|2|number|

## addFeature
添加矢量要素。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle); // 参考AILabel.Feature.Polygon【此处不再赘述】
gFeatureLayer.addFeature(feature);
```

## getFeatureById
通过要素id获取指定要素。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle); // 参考AILabel.Feature.Polygon【此处不再赘述】
gFeatureLayer.addFeature(feature);
// 根据id获取feature
const fea = gFeatureLayer.getFeatureById(featureId);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|featureId|feature对象唯一标志id|是|--|string|

## removeAllFeatures
删除当前要素层上所有要素。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle); // 参考AILabel.Feature.Polygon【此处不再赘述】
gFeatureLayer.addFeature(feature);
// 获取当前矢量层上所有矢量对象
gFeatureLayer.removeAllFeatures();
```

## removeFeature
删除要素。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle); // 参考AILabel.Feature.Polygon【此处不再赘述】
gFeatureLayer.addFeature(feature);
// 删除指定feature
gFeatureLayer.removeFeature(feature);
```

## removeFeatureById
通过要素id删除指定要素。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle); // 参考AILabel.Feature.Polygon【此处不再赘述】
gFeatureLayer.addFeature(feature);
// 通过要素id删除指定要素
gFeatureLayer.removeFeatureById(featureId);
```

## removeFeaturesByIds
通过要素id集合删除指定要素集合。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle); // 参考AILabel.Feature.Polygon【此处不再赘述】
gFeatureLayer.addFeature(feature);
// 删除feature集合
const featureIds = [featureId];
gFeatureLayer.removeFeaturesByIds(featureIds);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|featureIds|feature对象唯一标志ids|是|--|array|

## removeFeaturesByProperty
通过要素属性数据删除要素。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, {name: '中国'}, gStyle); // 参考AILabel.Feature.Polygon【此处不再赘述】
gFeatureLayer.addFeature(feature);

const properties = [{key: 'name', value: '中国'}];
gFeatureLayer.removeFeaturesByProperty(properties);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|properties|待删除要素的属性数据集合|是|--|array|

## getAllFeatures
返回当前要素层上所有要素。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle); // 参考AILabel.Feature.Polygon【此处不再赘述】
gFeatureLayer.addFeature(feature);

const allFeatures = gFeatureLayer.getAllFeatures(); // 返回所有要素数据
```

--------
# AILabel.Layer.Mask
## 实例化
涂抹层【用于涂抹数据展示、绘制及擦除】。
```javascript
const gMaskLayer = new AILabel.Layer.Mask(layerId, config);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|layerId|实例图层唯一标志id|是|--|string|
|config|其他配置项|否|--|Config|

<h4>Config</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|opacity|透明度0-1|否|1|number|
|zIndex|同css中zIndex|否|2|number|

## addMaskAction
添加涂抹Action【Action定义请往下看】。此处建议参考demo: http://www.gdbox.vip/gdbox/demo/drawFeature
```javascript
// MaskAction分3类【imgMask、drawAction、clearAction】
gMaskLayer.addMaskAction(MaskAction);
```

<h4>MaskAction分类</h4>

|参数|说明|类型|
|---|---|---|
|imgMask|图片Action，主要适应场景为后端储存的涂抹数据（比如rle数据）需要转换为png透明格式图片形式返回（原则上和标注样本图片的大小保持一致），这样前端就可以有效避免像素级数据循环处理，至于原因，你懂的，不再赘述|imgMask: 下方定义|
|drawMask|绘制Action，适应场景为用户绘制结束后，AILabel会通过gMap.events.on('geometryDrawDone', params => {})返回此类型Action给业务方，业务方可根据具体场景决定对其是否添加附加属性，然后通过addMaskAction方法进行添加即可|drawMask: 下方定义|
|clearMask||clearMask: 下方定义|

<h4>imgMask</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|key|当前action唯一标识|是|--|string|
|name|此参数进行action归类使用，在最终数据处理时会把同一name的action进行合并处理|是|--|string|
|type|当时image时，此处固定为'imgMask'|是|--|string|
|image|image对象,canvas:drawImage支持的image类型即可，此处需要注意的点：当后端返回image-url时，需要在new Image():onload之后进行addMaskAction(imgMaskAction)操作|是|--|object|

<h4>drawMask</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|key|当前action唯一标识|是|--|string|
|name|此参数进行action归类使用，在最终数据处理时会把同一name的action进行合并处理|是|--|string|
|type|当时image时，此处固定为'drawMask'|是|--|string|
|segments|涂抹绘制轨迹图形集|是|--|Segment[]: 定义继续往下看|

<h4>clearMask</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|key|当前action唯一标识|是|--|string|
|type|当时image时，此处固定为'clearMask'|是|--|string|
|segments|涂抹擦除轨迹图形集|是|--|Segment[]: 定义继续往下看|

<h4>Segment</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|type|当前图形类型，目前支持circle、polygon|是|--|string|
|point|type='circle'有效，圆圈中心点{x:--,y:--}|是|--|object|
|radius|type='circle'有效，圆圈半径|是|--|number|
|points|type='polygon'有效，多边形顶点集合|是|--|point[]|
|color|图形十六进制填充色，在action-type='clearMask'时无效|是|--|string|

## setRoi
设置感兴趣区域，业务方需求可能会要求对图片以外区域不展示涂抹数据，此方法就是为了解决这种问题而设置的。
```javascript
// 设置图片区域为感兴趣区
gMaskLayer.setRoi([
   {
       x: - imgWidth / 2,
       y: imgHeight / 2
   }, {
       x:  imgWidth / 2,
       y: imgHeight / 2
   }, {
       x:  imgWidth / 2,
       y: -imgHeight / 2
   }, {
       x: - imgWidth / 2,
       y: -imgHeight / 2
   }
]);
```

## getMaskActionsWithPixels
获取rle格式数据，AILabel会对所有的actions按照name属性进行分类，然后进行合并处理，最终按照name属性区别产生对应的rle压缩数据；
```javascript
// 按标签获取rle数据
gMaskLayer.getMaskActionsWithPixels(width, height);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|width|需要获取rle区域大小宽度，一般来说，设置成imgWidth即可|是|--|number|
|height|需要获取rle区域大小宽度，一般来说，设置成imgHeight即可|是|--|number|


--------
# AILabel.Layer.Marker
## 实例化
marker标注层为系统内置图层，可通过gMap.mLayer进行获取。

## addMarker
添加标注对象。
```javascript
const marker = new AILabel.Marker(markerId, config); // 参考AILabel.Marker【此处不再赘述】
// 添加
gMap.mLayer.addMarker(marker);
```

## removeMarker
删除标注。
```javascript
const marker = new AILabel.Marker(markerId, config); // 参考AILabel.Marker【此处不再赘述】
gMap.mLayer.addMarker(marker);
// 删除
gMap.mLayer.removeMarker(marker);
```

## removeMarkerById
通过标注id删除指定标注。
```javascript
const marker = new AILabel.Marker(markerId, config); // 参考AILabel.Marker【此处不再赘述】
gMap.mLayer.addMarker(marker);
// 删除指定marker
gMap.mLayer.removeMarkerById(markerId);
```

## removeMarkersByIds
通过标注id集合删除指定标注集合。
```javascript
const marker = new AILabel.Marker(markerId, config); // 参考AILabel.Marker【此处不再赘述】
gMap.mLayer.addMarker(marker);
gMap.mLayer.removeMarkerById(markerId);
const markerIds = [markerId];
// 删除marker集合
gMap.mLayer.removeMarkersByIds(markerIds);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|markerIds|marker对象唯一标志ids|是|--|array|

## getAllMarkers
返回当前标注层上所有标注对象。
```javascript
const marker = new AILabel.Marker(markerId, config); // 参考AILabel.Marker【此处不再赘述】
gMap.mLayer.addMarker(marker);
gMap.mLayer.removeMarkerById(markerId);
// 获取所有markers
const allMarkers = gMap.mLayer.getAllMarkers(); // 返回所有标注数据
```

## getMarkerById
通过标注id获取指定标注对象。
```javascript
const marker = new AILabel.Marker(markerId, config); // 参考AILabel.Marker【此处不再赘述】
gMap.mLayer.addMarker(marker);
gMap.mLayer.removeMarkerById(markerId);
// 获取指定marker
const mar = gMap.mLayer.getMarkerById(markerId);
```

## addMarkers
添加标注对象集合。
```javascript
const marker = new AILabel.Marker(markerId, config); // 参考AILabel.Marker【此处不再赘述】
const marker2 = new AILabel.Marker(markerId2, config2); // 参考AILabel.Marker【此处不再赘述】
// 添加marker集合
gMap.mLayer.addMarkers([marker, marker2]);
```

## removeMarkers
移除标注对象集合。
```javascript
const marker = new AILabel.Marker(markerId, config); // 参考AILabel.Marker【此处不再赘述】
const marker2 = new AILabel.Marker(markerId2, config2); // 参考AILabel.Marker【此处不再赘述】
gMap.mLayer.addMarkers([marker, marker2]);
// 移除marker集合
gMap.mLayer.removeMarkers([marker, marker2]);
```

## removeAllMarkers
删除当前标注层上所有标注对象。
```javascript
const marker = new AILabel.Marker(markerId, config); // 参考AILabel.Marker【此处不再赘述】
const marker2 = new AILabel.Marker(markerId2, config2); // 参考AILabel.Marker【此处不再赘述】
gMap.mLayer.addMarkers([marker, marker2]);
// 删除所有markers
gMap.mLayer.removeAllMarkers();
```

--------
# AILabel.Layer.Text
## 实例化
文本图层
```javascript
const textLayer = new AILabel.Layer.Text(layerId, config);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|layerId|实例图层唯一标志id|是|--|string|
|config|其他配置项|否|--|Config|

<h4>Config</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|zIndex|同css中zIndex|否|2|number|

## addText
添加文本对象。
```javascript
const textLayer = new AILabel.Layer.Text(layerId, config);
const text = new AILabel.Text(textId, config, gStyle); // 参考AILabel.Text【此处不做赘述】
// 添加text对象
textLayer.addText(text);
```

## removeText
删除文本。
```javascript
const textLayer = new AILabel.Layer.Text(layerId, config);
const text = new AILabel.Text(textId, config, gStyle); // 参考AILabel.Text【此处不做赘述】
textLayer.addText(text);
// 删除text
textLayer.removeText(text);
```

## getTextById
通过文本id获取指定文本对象。
```javascript
const textLayer = new AILabel.Layer.Text(layerId, config);
const text = new AILabel.Text(textId, config, gStyle); // 参考AILabel.Text【此处不做赘述】
textLayer.addText(text);
// 获取指定text
textLayer.getTextById(textId);
```

## removeTextById
通过文本id删除指定文本。
```javascript
const textLayer = new AILabel.Layer.Text(layerId, config);
const text = new AILabel.Text(textId, config, gStyle); // 参考AILabel.Text【此处不做赘述】
textLayer.addText(text);
// 删除指定text
textLayer.removeTextById(textId);
```

## removeTextsByIds
通过文本id集合删除指定文本集合。
```javascript
const textLayer = new AILabel.Layer.Text(layerId, config);
const text = new AILabel.Text(textId, config, gStyle); // 参考AILabel.Text【此处不做赘述】
textLayer.addText(text);
// 删除text集合
textLayer.removeTextsByIds([textId]);
```

## addTexts
添加文本对象集合。
```javascript
const text = new AILabel.Text(textId, config, gStyle); // 参考AILabel.Text【此处不做赘述】
const text2 = new AILabel.Text(textId2, config, gStyle); // 参考AILabel.Text【此处不做赘述】
// 添加文本集合
textLayer.addTexts([text, text2]);
```

## removeTexts
删除文本对象集合。
```javascript
const text = new AILabel.Text(textId, config, gStyle); // 参考AILabel.Text【此处不做赘述】
const text2 = new AILabel.Text(textId2, config, gStyle); // 参考AILabel.Text【此处不做赘述】
textLayer.addTexts([text, text2]);
// 删除文本集合
textLayer.removeTexts([text, text2]);
```

## getAllTexts
返回当前文本层上所有文本对象。
```javascript
const text = new AILabel.Text(textId, config, gStyle); // 参考AILabel.Text【此处不做赘述】
const text2 = new AILabel.Text(textId2, config, gStyle); // 参考AILabel.Text【此处不做赘述】
textLayer.addTexts([text, text2]);
// 获取所有text集合
const allTexts = textLayer.getAllTexts(); // 返回所有文本数据
```

## removeAllTexts
删除当前文本层上所有文本对象。
```javascript
const text = new AILabel.Text(textId, config, gStyle); // 参考AILabel.Text【此处不做赘述】
const text2 = new AILabel.Text(textId2, config, gStyle); // 参考AILabel.Text【此处不做赘述】
textLayer.addTexts([text, text2]);
// 清空text文本对象
textLayer.removeAllTexts();
```

--------
# AILabel.Feature.Point
要素数据：点。
## 实例化
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
// 实例化点
const feature = new AILabel.Feature.Point(featureId, point, data, gStyle, options);
gFeatureLayer.addFeature(feature);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|featureId|要素id|是|--|string|
|point|要素空间数据，如[{x: y:}|是|--|Point|
|data|要素属性数据，可通过实例.data属性获取|是|--|object|
|gStyle|要素样式|是|--|参考AILabel.Style|
|options|其他配置项|否|--|Option|

<h4>Option</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|radius|实际坐标系下半径【随图形缩放会进行相应缩放】，如果不设置，则会应用传入style样式进行显示，即不会随图形缩放而缩放|否|--|number|

## show
点要素显示。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Point(featureId, point, data, gStyle);
gFeatureLayer.addFeature(feature);
// 隐藏
feature.hide();
// 展示
feature.show();
```

## hide
点要素隐藏。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Point(featureId, point, data, gStyle);
gFeatureLayer.addFeature(feature);
// 隐藏
feature.hide();
```

## update
点要素更新。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Point(featureId, point, data, gStyle);
gFeatureLayer.addFeature(feature);
// 更新
feature.update(options);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|options|更新数据配置项|是|--|Option|

<h4>Option</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|point|待更新空间数据|是|--|Point|
|data|待更新属性数据|是|--|object|
|style|待更新样式数据|是|--|AILabel.Style|

## isCaught
判断点是否在捕捉容限内。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Point(featureId, point, data, gStyle);
gFeatureLayer.addFeature(feature);

feature.isCaught(wxy); // return false;
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|wxy|{x:, y: }|是|--|object|

--------
# AILabel.Feature.Polyline
要素数据：多段线。
## 实例化
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
// 实例化多段线
const feature = new AILabel.Feature.Polyline(featureId, points, data, gStyle, options);
gFeatureLayer.addFeature(feature);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|featureId|要素id|是|--|string|
|points|要素空间数据，如[{x: y:}, {x: y:}, {x: y:}]，长度不能低于2个|是|--|array|
|data|要素属性数据，可通过实例.data属性获取|是|--|object|
|gStyle|要素样式|是|--|参考AILabel.Style|
|options|其他配置项|否|--|Option|

<h4>Option</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|width|实际坐标系下宽度【随图形缩放会进行相应缩放】，如果不设置，则会应用传入style样式进行显示，即不会随图形缩放而缩放|否|--|number|

## show
多段线要素显示。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polyline(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);
// 隐藏
feature.hide();
// 展示
feature.show();
```

## hide
多边形要素隐藏。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polyline(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);
// 隐藏
feature.hide();
```

## update
多段线要素更新。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polyline(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);
// 更新
feature.update(options);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|options|更新数据配置项|是|--|Option|

<h4>Option</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|points|待更新空间数据|是|--|Point[]|
|data|待更新属性数据|是|--|object|
|style|待更新样式数据|是|--|AILabel.Style|

## active
设置feature选中【建议用户尽量避免使用】。
```javascript
const feature = new AILabel.Feature.Polyline(featureId, points, data, gStyle);
// 设置feature选中
feature.active();
```

## deActive
取消feature选中【建议用户尽量避免使用】。
```javascript
const feature = new AILabel.Feature.Polyline(featureId, points, data, gStyle);
// 取消feature选中
feature.deActive();
```

## getBounds
获取feature最小外接矩形。
```javascript
const feature = new AILabel.Feature.Polyline(featureId, points, data, gStyle);
// 获取feature最小外接矩形
feature.getBounds();
```

## isCaught
判断点是否捕捉到当前多段线。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polyline(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);

feature.isCaught(wxy); // return false;
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|wxy|{x:, y: }|是|--|object|

--------
# AILabel.Feature.Rect
要素数据：矩形。
## 实例化
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
// 实例化矩形形
const feature = new AILabel.Feature.Rect(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|featureId|要素id|是|--|string|
|points|要素空间数据，如[{x: y:}, {x: y:}, {x: y:}]，长度按顺序固定4个|是|--|array|
|data|要素属性数据，可通过实例.data属性获取|是|--|object|
|gStyle|要素样式|是|--|参考AILabel.Style|

## show
矩形要素显示。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Rect(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);
// 隐藏
feature.hide();
// 展示
feature.show();
```

## hide
矩形要素隐藏。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Rect(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);
// 隐藏
feature.hide();
```

## update
矩形要素更新。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Rect(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);
// 更新
feature.update(options);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|options|更新数据配置项|是|--|Option|

<h4>Option</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|points|待更新空间数据，固定长度为4的{x:, y: }|是|--|Point[]|
|data|待更新属性数据|是|--|object|
|style|待更新样式数据|是|--|AILabel.Style|

## active
设置feature选中【建议用户尽量避免使用】。
```javascript
const feature = new AILabel.Feature.Rect(featureId, points, data, gStyle);
// 设置feature选中
feature.active();
```

## deActive
取消feature选中【建议用户尽量避免使用】。
```javascript
const feature = new AILabel.Feature.Rect(featureId, points, data, gStyle);
// 取消feature选中
feature.deActive();
```

## isCaught
判断点是否在当前要素内。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Rect(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);

feature.isCaught(wxy); // return false;
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|wxy|{x:, y: }|是|--|object|

--------

# AILabel.Feature.Polygon
要素数据：多边形。
## 实例化
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
// 实例化多边形
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|featureId|要素id|是|--|string|
|points|要素空间数据，如[{x: y:}, {x: y:}, {x: y:}]，长度不能低于3个|是|--|array|
|data|要素属性数据，可通过实例.data属性获取|是|--|object|
|gStyle|要素样式|是|--|参考AILabel.Style|

## show
多边形要素显示。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);
// 隐藏
feature.hide();
// 展示
feature.show();
```

## hide
多边形要素隐藏。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);
// 隐藏
feature.hide();
```

## update
多边形要素更新。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);
// 更新
feature.update(options);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|options|更新数据配置项|是|--|Option|

<h4>Option</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|points|待更新空间数据|是|--|Point[]|
|data|待更新属性数据|是|--|object|
|style|待更新样式数据|是|--|AILabel.Style|

## active
设置feature选中【建议用户尽量避免使用】。
```javascript
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle);
// 设置feature选中
feature.active();
```

## deActive
取消feature选中【建议用户尽量避免使用】。
```javascript
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle);
// 取消feature选中
feature.deActive();
```

## getBounds
获取feature最小外接矩形。
```javascript
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle);
// 获取feature最小外接矩形
feature.getBounds();
```

## isCaught
判断点是否在当前要素内。
```javascript
const featureLayer = new AILabel.Layer.Feature(layerId, config);
const feature = new AILabel.Feature.Polygon(featureId, points, data, gStyle);
gFeatureLayer.addFeature(feature);

feature.isCaught(wxy); // return false;
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|wxy|{x:, y: }|是|--|object|

--------
# AILabel.Marker
## 实例化
实例标注对象。
```javascript
const marker = new AILabel.Marker(markerId, config);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|markerId|标注id|是|--|string|
|config|更新数据配置项|是|--|Config|

<h4>Config</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|src|图标src|否|--|string|
|x|标注位置|否|--|number|
|y|标注位置|否|--|number|
|offset|标注图标展示偏移量，如{x:, y:}|否|--|object|

## update
标注对象更新。
```javascript
const marker = new AILabel.Marker(markerId, config);
// 更新标注信息
marker.update(options);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|options|更新数据配置项|是|--|Option|

<h4>Option</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|src|待更新图标src|否|--|string|
|x|待更新标注位置|否|--|number|
|y|待更新标注位置|否|--|number|
|offset|待更新标注图标展示偏移量，如{x:, y:}|否|--|object|

## regEvent
标注对象事件注册，目前仅支持click事件。
```javascript
const marker = new AILabel.Marker(markerId, config);
// 注册click事件监听
marker.regEvent('click', function () {
    gMap.mLayer.removeMarker(this); // this指向当前标注对象
});
```

## showInfo
展示marker信息。
```javascript
// 待实现
```

--------
# AILabel.Text
## 实例化
实例文本对象。
```javascript
const text = new AILabel.Text(textId, config, gStyle);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|textId|文本id|是|--|string|
|config|配置项|是|--|Config|
|gStyle|文本样式|是|--|AILabel.Style|

<h4>Config</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|text|展示文本，可为'空字符串'|是|--|string|
|pos|标注位置，如{x: , y:}|是|--|object|
|visible|是否可见|否|true|bool|
|width|文本宽度|否|默认|number|
|maxWidth|最大宽度|否|默认|number|
|wrap|是否自动换行|否|false|bool|
|offset|偏移量，如{x: , y:}|否|{x: 0, y: 0}|object|

## update
更新文本对象。
```javascript
const text = new AILabel.Text(textId, config, gStyle);
// 更新
text.update(options);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|options|更新数据配置项|是|--|Option|

<h4>Option</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|text|展示文本，可为'空字符串'|是|--|string|
|pos|标注位置，如{x: , y:}|是|--|object|
|visible|是否可见|否|true|bool|
|width|文本宽度|否|默认|number|
|maxWidth|最大宽度|否|默认|number|
|offset|偏移量，如{x: , y:}|否|{x: 0, y: 0}|object|

## setText
设置文本内容。
```javascript
const text = new AILabel.Text(textId, config, gStyle);
// 更新设置文本
text.setText('new-text');
```

## setPosition
设置文本位置。
```javascript
const text = new AILabel.Text(textId, config, gStyle);
// 更新文本对象位置
text.setPosition(x, y);
```

--------
# AILabel.Control.EagleMap
控件：缩略图，支持两种缩略图形式，一种是纯网格形式，另一种是图像形式；
## 实例化
```javascript
const eagleControl = new AILabel.Control.EagleMap(eagleMapId, options);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|eagleMapId|缩略图id|是|--|string|
|options|配置项|是|--|Option|

<h4>Option</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|container|缩略图容器id|否|在gMap主容器|string|
|postion|缩略图位置，与container互斥|否|{right: 10, bottom: 10}|object|
|type|缩略图类型'default'/'grid'|否|default|string|
|image|type为default时有效【建议与imageLayer保持一致】|是|--|Image|
|grid|线段是否虚线|否|--|Grid|
|size|大小，如{width: 200,height: 150}|否|{width: 200,height: 150}|object|

<h4>Image</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|src|路径|是|--|string|
|width|图像原始宽|是|--|number|
|height|图像原始高|是|--|number|

<h4>Grid</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|rowCount|行数|是|--|number|
|columnCount|列数|是|--|number|
|color|网格颜色-十六进制|否|#000000|string|

--------
# AILabel.Control.Scale
控件：比例尺，展示当前缩放比例尺【目前展示形式待丰富】。
## 实例化
```javascript
const scaleControl = new AILabel.Control.Scale(scaleId, options);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|scaleId|比例尺控件id|是|--|string|
|options|配置项|是|--|Option|

<h4>Option</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|postion|所处位置|否|{left: 10, top: 10}|object|

--------
# AILabel.Style
设置样式对象。
## 实例化
```javascript
const gTextStyle = new AILabel.Style(config);
```
<h4>Params</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|config|配置项|是|--|Config|

<h4>Config</h4>

|参数|说明|是否必填|默认|类型|
|---|---|---|---|---|
|strokeColor|画笔颜色|否|'#00DD00'|string|
|opacity|透明度0-1|否|1|number|
|lineWeight|线宽|否|1|number|
|fillColor|填充色|否|'#00DD00'|string|
|lineDash|线段是否虚线|否|false|bool|
|bgColor|背景色|否|'#ffffff'|string|
|fontSize|字体大小|否|13|number|
|fontColor|字体颜色|否|'#333333'|string|
|pointRadius|点半径|否|3|number|

--------
# AILabel.Util
相关工具库。
## worldToScreen
实际坐标转屏幕坐标。
```javascript
const sxy = AILabel.Util.worldToScreen(gMap, x, y);
```

## screenToWorld
屏幕坐标转实际坐标。
```javascript
const wxy = AILabel.Util.screenToWorld(gMap, x, y);
```

## getBounds
屏幕坐标转实际坐标。
```javascript
const bounds = AILabel.Util.getBounds(points); // [left_top_point, right_top_point, left_bottom_point, right_bottom_point]
```

--------
# FAQ

* <h6>AILabel坐标系</h6>

> AILabel的原点是基于用户数据的原点，即原点依赖于传入数据，x轴向右，y轴向上（当图片存在时，图片的中心点就是实际坐标系的原点）；

* <h6>为什么后端给我返回的坐标系不能正确的显示？</h6>

> 原因一：坐标系不一致造成：后端返回的数据可能是基于图像左上角为(0, 0)原点，x轴向右，y轴向下坐标系产生的，但我们的坐标系实际是x轴向右，y轴向上（当图片存在时，图片的中心点就是实际坐标系的原点）；

> 原因二：...

* <h6>实际坐标系与屏幕坐标系区别？</h6>

> 实际坐标系就是实体的本身坐标系，不会随着视野范围变化而产生变化。
> 屏幕坐标系就是用来将实际意义的坐标应用于电子地图上展示的临时坐标系。
> 举个栗子：比如您家的房子位于(lat36, lng128)，在电子地图上展示你家的实际位置用户不会变化，但是当电子地图进行平移或者缩放时，您家房子的展示位置可能会发生变化，这里所说的展示位置就是屏幕坐标位置；

* <h6>zoom值到底是啥</h6>

> zoom值的意思就是缩放值，即显示容器的宽所代表的实际距离宽；比如容器宽度是1000px，而此时如果设置zoom为2000，则zoom的意思就是1000px宽的容器所指代的实际距离是2000，更进一步说就是，比如从您家到您姑姑家距离是2000米，则显示在屏幕上设置zoom=2000就是1000px宽的显示容器代表的实际距离就是2000米；

* <h6>未完待续</h6>

