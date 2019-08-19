## 图片高级处理

### imageMogr2
```
imageMogr2/auto-orient
            /thumbnail/<imageSizeGeometry>
            /gravity/<gravityType>
            /crop/<imageSizeAndOffsetGeometry>
            /rotate/<rotateDegree>
            /format/<destinationImageFormat>
            /blur/<radius>x<sigma>
            /background/<ecodedBackgroundColor>
      		/quality/<quality>
            /sharpen/<sharpen>
            /roundpic/<radiusX>x<radiusY>
    	    /iradius/<iradius>
```
### 参数说明

| Item                                | Value                                                        | Description                                            | Optional |
| ----------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------ | -------- |
| /auto-orient                        | 无                                                           | 建议放在首位，根据原图EXIF信息自动旋正，便于后续处理。 | O        |
| /thumbnail/<imageSizeGeometry>      | -                                                            | 参考 [**thumbnail**说明](#Thumbnail)                   | O        |
| /gravity/<gravityType>              | -                                                            | 参考 [**gravity**说明](#Gravity)                       | O        |
| /crop/<imageSizeAndOffsetGeometry>  | -                                                            | 参考 [**crop**说明](#Crop)                             | O        |
| /rotate/<rotateDegree>              | 取值范围为1-360，默认为不旋转                                | 图片旋转角度                                           | O        |
| /format/<destinationImageFormat>    | 支持jpg、gif、png、webp等，默认为原图格式                    | 新图的输出格式                                         | O        |
| /blur/<radius>x<sigma>              | radius是模糊半径，取值范围为1-50。sigma是正态分布的标准差，必须大于0。 | 高斯模糊参数                                           | O        |
| /background/<ecodedBackgroundColor> | -                                                            | 背景填充颜色,参考color说明                             | O        |
| /quality/<quality>                  | 取值范围1-100， 默认值75                                     | 新图的输出质量                                         | O        |
| /sharpen/<sharpen>                  | 锐化参数值，取值范围为10-300间的整数。参数值越大，锐化效果越明显。 | 图片是否锐化                                           | O        |
| /roundpic/<radiusX>x<radiusY>       | 水平和垂直的值相同， 则可以写成类似/roundpic/200这样， 否则/roundpic/200x300。 支持/roundpic/!50p和/roundpic/50p这种形式， 意思是原图的宽和高的50%作为radiusX和radiusY值。 | 圆角大小的参数                                         | O        |
| /iradius/<iradius>                  | radius是内切圆的半径，取值范围为大于0、小于原图最小边一半的整数。内切圆的圆心为图片的中心。图片格式为gif时，不支持该参数。 | 内切圆裁剪功能                                         | O        |

<span id="Thumbnail"></span>

#### thumbnail说明

| Item                                      | Description                                                  |
| ----------------------------------------- | ------------------------------------------------------------ |
| /thumbnail/!&lt;Scale&gt;p                | 指定图片的宽高为原图的 Scale%。                              |
| /thumbnail/!&lt;Scale&gt;px               | 指定图片的宽为原图的 Scale% ，高度不变。                     |
| /thumbnail/!x&lt;Scale&gt;p               | 指定图片的高为原图的 Scale% ，宽度不变。                     |
| /thumbnail/&lt;Width&gt;x                 | 指定目标图片宽度为 Width ，高度等比压缩。                    |
| /thumbnail/x&lt;Height&gt;                | 指定目标图片高度为 Height ，宽度等比压缩。                   |
| /thumbnail/&lt;Width&gt;x&lt;Height&gt;   | 限定缩略图的宽度和高度的最大值分别为 Width 和 Height，进行等比缩放。 |
| /thumbnail/!&lt;Width&gt;x&lt;Height&gt;r | 限定缩略图的宽度和高度的最小值分别为 Width 和 Height，进行等比缩放 。 |
| /thumbnail/&lt;Width&gt;x&lt;Height&gt;!  | 忽略原图宽高比例，指定图片宽度为 Width ，高度为 Height ，强行缩放图片，可能导致目标图片变形。 |
| /thumbnail/&lt;Area&gt;@                  | 等比缩放图片，缩放后的图像，总像素数量不超过 Area。          |

<span id="Gravity"></span>

#### gravity说明

图片处理重心参数表
在图片高级处理现有的功能中只影响其后的裁剪操作参数表，即裁剪操作以 gravity 为原点开始偏移后，进行裁剪操作。
![img](https://camo.githubusercontent.com/5ef9d564005500065dd85158e9bdee6f385447f4/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f32353539366139313139313965343634643565646634633834623832396662652e706e67)

<span id="Crop"></span>

#### crop说明

##### 裁剪操作参数表 (cropsize)

| 参数名称                 | 必填 | 说明                                            |
| :----------------------- | :--- | :---------------------------------------------- |
| `/crop/<Width>x`         |      | 指定目标图片宽度，高度不变。取值范围为0-10000。 |
| `/crop/x<Height>`        |      | 指定目标图片高度，宽度不变。取值范围为0-10000。 |
| `/crop/<Width>x<Height>` |      | 同时指定目标图片宽高。取值范围为0-10000。       |

##### 裁剪偏移参数表 (cropoffset)

| 参数名称                      | 必填 | 说明                                                         |
| :---------------------------- | :--- | :----------------------------------------------------------- |
| `/crop/!{cropsize}a<dx>a<dy>` |      | 相对于偏移锚点，向右偏移dx个像素，同时向下偏移dy个像素。取值范围不限，小于原图宽高即可。 |
| `/crop/!{cropsize}-<dx>a<dy>` |      | 相对于偏移锚点，从指定宽度中减去dx个像素，同时向下偏移dy个像素。取值范围不限，小于原图宽高即可。 |
| `/crop/!{cropsize}a<dx>-<dy>` |      | 相对于偏移锚点，向右偏移dx个像素，同时从指定高度中减去dy个像素。取值范围不限，小于原图宽高即可。 |
| `/crop/!{cropsize}-<dx>-<dy>` |      | 相对于偏移锚点，从指定宽度中减去dx个像素，同时从指定高度中减去dy个像素。取值范围不限，小于原图宽高即可。 |

#### color说明

可以是颜色名称（比如red）或十六进制颜色（比如#FF0000）的URL安全的Base64编码。我们支持的颜色名称有transparent（#00000000）、none（#00000000）、white（#FFFFFF）、black（#000000）、red（#FF0000）、orange（#FFA500）、yellow（#FFFF00）、green（#008000）、blue（#0000FF）、purple（#800080）、gray（#7E7E7E）、pink（#FFC0CB），其中none与transparent均为透明背景色，另外十六进制颜色不区分大小写，具体颜色请参考颜色编码表。缺省背景色为white（#FFFFFF）。


### 示例
#### 实时
##### 缩略图

* 等比缩小75%

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/!75p	

  ![thumbnail_s75p](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_thumbnail_s75p.jpeg)

* 按原宽度75%等比缩小， 高度不变。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/!75px	

  ![thumbnail_s75px](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_thumbnail_s75px.jpeg)

  * 按原高度75%等比缩小， 宽度不变。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/!x75p

  ![thumbnail_sx75p](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_thumbnail_sx75p.jpeg)

  * 指定新宽度 1536px， 等比缩放。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/1536x

  ![thumbnail_1536x](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_thumbnail_1536x.jpeg)

  * 指定新高度 1152px， 等比缩放。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/x1152

  ![thumbnail_x1152](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_thumbnail_x1152.jpeg)

  * 限定长边， 生成不超过 400x400 的缩略图

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/400x400

  ![thumbnail_400x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_thumbnail_400x400.jpeg)

  * 限定短边， 生成不小于 400x400的缩略图

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/!400x400r

  ![thumbnail_s400x400r](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_thumbnail_s400x400r.jpeg)

  * 强制生成400x600的图

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/400x600!

  ![thumbnail_400x600s](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_thumbnail_400x600s.jpeg)

  * 原图大于指定长宽矩形， 按宽缩放比和高缩放比的较大值进行缩放成400x300。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/400x600>

  ![thumbnail_400x600gt](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_thumbnail_400x600gt.jpeg)

  * 原图小于指定长宽矩形， 按宽缩放比和高缩放比的较小值缩放成1467x1100。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/1500x1100<

  ![thumbnail_1500x1100lt](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_thumbnail_1500x1100lt.jpeg)

  * 按原图高宽比例等比缩放， 缩放后的像素数量不超过900000。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/900000@

  ![thumbnail_900000at](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_thumbnail_900000at.jpeg)

##### 裁剪
* 生成 400x768裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/crop/400x

![crop_400x](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_crop_400x.jpeg)

* 生成1024x400的裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/crop/x400

![crop_x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_crop_x400.jpeg)

* 生成400x400的裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/crop/400x400

![crop_400x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_crop_400x400.jpeg)

* 生成300x300裁剪图， 偏移距离30x100

POST http://ctaccel.com/api/v1?imageMogr2/crop/!400x400a30a100

![crop_s400x400a30a100](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_crop_s400x400a30a100.jpeg)

* 生成400x300裁剪图， 偏移距离30x0

POST http://ctaccel.com/api/v1?imageMogr2/crop/!400x400a30-100

![crop_s400x400a30-100](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_crop_s400x400a30-100.jpeg)

* 生成370*400裁剪图，偏移距离0x100

POST http://ctaccel.com/api/v1?imageMogr2/crop/!400x400-30a100

![crop_s400x400-30a100](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_crop_s400x400-30a100.jpeg)

* 生成370x300裁剪图， 偏移距离0x0

POST http://ctaccel.com/api/v1?imageMogr2/crop/!400x400-30-100

![crop_s400x400-30-100](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_crop_s400x400-30-100.jpeg)

* 锚点在左上角（northwest）， 生成300x300裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/northwest/crop/400x400

![crop_northwest_400x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_gravity_northwest_crop_400x400.jpeg)

* 锚点在正上方（north）， 生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/north/crop/400x400

![crop_north_400x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_gravity_north_crop_400x400.jpeg)

* 锚点在右上方（northeast）， 生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/northeast/crop/400x400

![crop_northeast_400x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_gravity_northeast_crop_400x400.jpeg)

* 锚点在正左方（west），　生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/west/crop/400x400

![crop_west_400x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_gravity_west_crop_400x400.jpeg)

* 锚点在正中（center），　生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/center/crop/400x400

![crop_center_400x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_gravity_center_crop_400x400.jpeg)

* 锚点在正右方 （east），  生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/east/crop/400x400

![crop_east_400x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_gravity_east_crop_400x400.jpeg)

* 锚点在左下方 （southwest），  生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/southwest/crop/400x400

![crop_southwest_400x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_gravity_southwest_crop_400x400.jpeg)

* 锚点在正下方 （south），  生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/south/crop/400x400

![crop_south_400x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_gravity_south_crop_400x400.jpeg)

* 锚点在右下方 （southeast），  生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/southeast/crop/400x400

![crop_southeast_400x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_gravity_southeast_crop_400x400.jpeg)

##### 旋转
* 顺时针旋转45度

POST http://ctaccel.com/api/v1?imageMogr2/rotate/45

![rotate_45](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_rotate_45.jpeg)

* 旋转并添加背景色，裁剪以及高斯模糊，输出质量为80%

POST http://ctaccel.com/api/v1?imageMogr2/auto-orient/thumbnail/!256x256r/background/b3Jhbmdl/gravity/center/crop/256x256/blur/3x9/quality/80/rotate/45

![imagemogr2_all_params](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_all_params.jpeg)

#### 高斯模糊

* 半径为5， sigma值为9。

POST http://ctaccel.com/api/v1?imageMogr2/blur/5x9

![blur_5x9](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_blur_5x9.jpeg)

#### 椭圆圆角

* 水平方向和垂直方向都为300像素

POST http://ctaccel.com/api/v1?imageMogr2/roundpic/300

![roundpic_300](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_roundpic_300.jpeg)

* 水平方向为300px，　垂直方向为400px

POST http://ctaccel.com/api/v1?imageMogr2/roundpic/300x400

![roundpic_300x400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_roundpic_300x400.jpeg)

* 水平方向和垂直方向都为原图片的30%大小

POST http://ctaccel.com/api/v1?imageMogr2/roundpic/!30p

![roundpic_s30p](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_roundpic_s30p.jpeg)

### 中心原图
* 中心原图半径为300px

POST http://ctaccel.com/api/v1?imageMogr2/iradius/300

![iradius_300](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_iradius_300.jpeg)

* 中心原图直径为原宽高最小值的60%

POST http://ctaccel.com/api/v1?imageMogr2/iradius/!60p

![iradius_s60p](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imagemogr2_iradius_s60p.jpeg)
