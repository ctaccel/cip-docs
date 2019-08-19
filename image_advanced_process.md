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

  ![thumbnail_s75p](https://thumbnail0.baidupcs.com/thumbnail/a47697e372d36b4b39509fffb8ea1cc6?fid=2117452681-250528-378143468343094&time=1565917200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-FVepGXt%2B6nVHqqYu7T7rHvycmFE%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5273789755550888266&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 按原宽度75%等比缩小， 高度不变。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/!75px	

  ![thumbnail_s75px](https://thumbnail0.baidupcs.com/thumbnail/2f88503c0b8411793d731337e7dcae97?fid=2117452681-250528-1074743522445034&time=1565917200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-JWXvHi6ntmcMRqaU8ESNdbTwIMQ%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5273853011793703403&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

  * 按原高度75%等比缩小， 宽度不变。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/!x75p

  ![thumbnail_sx75p](https://thumbnail0.baidupcs.com/thumbnail/0258dcc82ba7c93b48606a7c445a4ddb?fid=2117452681-250528-1079410904352132&time=1565917200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-uhHSFPhCqTfmeSR1p8gOJo7g86I%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5273919174895451045&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

  * 指定新宽度 1536px， 等比缩放。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/1536x

  ![thumbnail_1536x](https://thumbnail0.baidupcs.com/thumbnail/887ac568ddf90234cb9abab0b6603236?fid=2117452681-250528-953778669971612&time=1565917200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-GjX7DnUOk7IgZYRtiWQTyIt9iLg%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5273964476133843515&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

  * 指定新高度 1152px， 等比缩放。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/x1152

  ![thumbnail_x1152](https://thumbnail0.baidupcs.com/thumbnail/887ac568ddf90234cb9abab0b6603236?fid=2117452681-250528-422864728573088&time=1565917200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-QEBPRpsEvrD2Sc%2FD7UkMuHF4Zok%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274001965040681842&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

  * 限定长边， 生成不超过 400x400 的缩略图

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/400x400

  ![thumbnail_400x400](https://thumbnail0.baidupcs.com/thumbnail/c9588f435dc3cfc804f698d84f46e548?fid=2117452681-250528-907339654380957&time=1565917200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-4m81EMLyKz1zf3JHlgyoPQ%2BDFBw%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274068508810564335&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

  * 限定短边， 生成不小于 400x400的缩略图

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/!400x400r

  ![thumbnail_s400x400r](https://thumbnail0.baidupcs.com/thumbnail/e2aa8991f1a1bf4674d76d2eded4df95?fid=2117452681-250528-471870825011605&time=1565917200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-LfVsj0sCCp71QntM0W7sa6zsSAE%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274117582310739640&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

  * 强制生成400x600的图

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/400x600!

  ![thumbnail_400x600s](https://thumbnail0.baidupcs.com/thumbnail/425482c9d972eea14090915a1631b6b7?fid=2117452681-250528-357746450877971&time=1565917200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-lXY268F9WAQAgZ%2B6Hml4FeVThIg%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274146538673562300&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

  * 原图大于指定长宽矩形， 按宽缩放比和高缩放比的较大值进行缩放成400x300。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/400x600>

  ![thumbnail_400x600gt](https://thumbnail0.baidupcs.com/thumbnail/c9588f435dc3cfc804f698d84f46e548?fid=2117452681-250528-387308204181729&time=1565917200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-xnzCOF30fwdxGJX1QD8WklJbRqo%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274247474117200388&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

  * 原图小于指定长宽矩形， 按宽缩放比和高缩放比的较小值缩放成1467x1100。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/1500x1100<

  ![thumbnail_1500x1100lt](https://thumbnail0.baidupcs.com/thumbnail/54f99e6e61fcb99cde3472bee11392c9?fid=2117452681-250528-387312171385786&time=1565917200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-v3tdrpfaFKNhpQpQsGlBC5kU4Kg%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274374505899813973&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

  * 按原图高宽比例等比缩放， 缩放后的像素数量不超过900000。

  POST http://ctaccel.com/api/v1?imageMogr2/thumbnail/900000@

  ![thumbnail_900000at](https://thumbnail0.baidupcs.com/thumbnail/02b93d3aad285243c5f4fd3b65e48e06?fid=2117452681-250528-1004287043961016&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-QacGAhD%2FpOdktjb6DQW7RRtnfL8%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274535427014666905&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

##### 裁剪
* 生成 400x768裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/crop/400x

![crop_400x](https://thumbnail0.baidupcs.com/thumbnail/cd981dd245be37d42b88fc2689e2b9ff?fid=2117452681-250528-171434618929530&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-uq8ojUBMSRCQdh3ziPT8A1lwYWw%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274633040127156541&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 生成1024x400的裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/crop/x400

![crop_x400](https://thumbnail0.baidupcs.com/thumbnail/a5ef382d4ad9de3ca809957d5feeb466?fid=2117452681-250528-526212237105490&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-UpMlPOwaqnil5A5SEy%2BE0Xs9Lu4%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274707552104123589&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 生成400x400的裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/crop/400x400

![crop_400x400](https://thumbnail0.baidupcs.com/thumbnail/e2526fe6fce622cd2bd35ab91c4c6524?fid=2117452681-250528-1007716388943336&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-oBA8E1r0%2B0YwHxEHF7B5vC52A7U%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274744391429826087&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 生成300x300裁剪图， 偏移距离30x100

POST http://ctaccel.com/api/v1?imageMogr2/crop/!400x400a30a100

![crop_s400x400a30a100](https://thumbnail0.baidupcs.com/thumbnail/1770d440f11de67fef6f5cc59ab9a3a8?fid=2117452681-250528-601815068939532&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-479HdMgXKBfEXpsG%2FtMhLZMrRzk%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274780470519996104&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 生成400x300裁剪图， 偏移距离30x0

POST http://ctaccel.com/api/v1?imageMogr2/crop/!400x400a30-100

![crop_s400x400a30-100](https://thumbnail0.baidupcs.com/thumbnail/7eccfbdb0fa0954867597fe030377aa9?fid=2117452681-250528-828736304659035&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-XR2ocTHc8X4%2Bdv45MY9UXgbgdjI%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274811623716626814&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 生成370*400裁剪图， 偏移距离0x100

POST http://ctaccel.com/api/v1?imageMogr2/crop/!400x400-30a100

![crop_s400x400-30a100](https://thumbnail0.baidupcs.com/thumbnail/366723a2f36a6f81bafaf260fdeeee29?fid=2117452681-250528-839207007134200&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-l0fzjCrXHwQjrErCIHmb%2BKqMBqo%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274844839933536932&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 生成370x300裁剪图， 偏移距离0x0

POST http://ctaccel.com/api/v1?imageMogr2/crop/!400x400-30-100

![crop_s400x400-30-100](https://thumbnail0.baidupcs.com/thumbnail/90b6c5a1ca05bc9cb58109a4d562a811?fid=2117452681-250528-885617217162262&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-eXAr6nUj3G9kbY5rZZetgEYGKn4%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274877885242710183&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 锚点在左上角（northwest）， 生成300x300裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/northwest/crop/400x400

![crop_northwest_400x400](https://thumbnail0.baidupcs.com/thumbnail/e2526fe6fce622cd2bd35ab91c4c6524?fid=2117452681-250528-844680269005286&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-Dyaoy6XMtDnM4vMi1mgrdLa2edE%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274963897333334182&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 锚点在正上方（north）， 生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/north/crop/400x400

![crop_north_400x400](https://thumbnail0.baidupcs.com/thumbnail/2ac7e5cf1865764ca0bff33da148470d?fid=2117452681-250528-915318082312571&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-TpYgdIXnk%2FSqHsyfhh%2B0HPfRh1Y%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5274995652072741012&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 锚点在右上方（northeast）， 生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/northeast/crop/400x400

![crop_northeast_400x400](https://thumbnail0.baidupcs.com/thumbnail/2aefac4056861fe5eed2da720a11dfb5?fid=2117452681-250528-106321474270451&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-Cp4zRB%2BYZoQU6UHeDAbe6GqJUo0%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275105323326428771&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 锚点在正左方（west），　生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/west/crop/400x400

![crop_west_400x400](https://thumbnail0.baidupcs.com/thumbnail/7a7bcea14e11d75ab666280403deaeac?fid=2117452681-250528-140915434555824&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-IUC7CjCV0PT%2BxB4nulRh9WPjDiM%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275124280715611606&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 锚点在正中（center），　生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/center/crop/400x400

![crop_center_400x400](https://thumbnail0.baidupcs.com/thumbnail/f4b0255517981a892c8a7a67e391c302?fid=2117452681-250528-812678551345388&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-CSU5uebP%2F8IC8AqN3r9%2FsNH667I%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275143734244859852&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 锚点在正右方 （east），  生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/east/crop/400x400

![crop_east_400x400](https://thumbnail0.baidupcs.com/thumbnail/cc90f3947eb11943def24ffbb4cd2cc9?fid=2117452681-250528-511570092930636&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-ey32lIXvNIY2siyykfGpKZeWQqg%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275164679239252975&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 锚点在左下方 （southwest），  生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/southwest/crop/400x400

![crop_southwest_400x400](https://thumbnail0.baidupcs.com/thumbnail/76405f4f838cdef5c41628513277121a?fid=2117452681-250528-842891497376733&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-wWQXDRtSplmVLu14SOQLogGIkIw%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275186478828935477&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 锚点在正下方 （south），  生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/south/crop/400x400

![crop_south_400x400](https://thumbnail0.baidupcs.com/thumbnail/e3499f27ad387b607e25656d59d3c4f3?fid=2117452681-250528-1017848313029726&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-I9Jcw%2BOWYpN5ct2zdKBtN6yTa7E%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275207597153536769&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 锚点在右下方 （southeast），  生成400x400裁剪图

POST http://ctaccel.com/api/v1?imageMogr2/gravity/southeast/crop/400x400

![crop_southeast_400x400](https://thumbnail0.baidupcs.com/thumbnail/7b8250405cdab17b0fc51a6602167d9b?fid=2117452681-250528-535628174893249&time=1565920800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-UT5N2Kb97qj7RAb%2Fpo9dtOC3zCM%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275251131319109556&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

##### 旋转
* 顺时针旋转45度

POST http://ctaccel.com/api/v1?imageMogr2/rotate/45

![rotate_45](https://thumbnail0.baidupcs.com/thumbnail/b7d9702e224c0c7b26d9470d0a3ccf67?fid=2117452681-250528-127010412697082&time=1565924400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-F0k0g9cV9Frpc35lvq64eNE%2B5To%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275501704280282869&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 旋转并添加背景色，裁剪以及高斯模糊，输出质量为80%

POST http://ctaccel.com/api/v1?imageMogr2/auto-orient/thumbnail/!256x256r/background/b3Jhbmdl/gravity/center/crop/256x256/blur/3x9/quality/80/rotate/45

![imagemogr2_all_params](https://thumbnail0.baidupcs.com/thumbnail/636b4d3dc78aa575371d2b99d9fd247a?fid=2117452681-250528-874093766724535&time=1565924400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-KJhl9RBKwfRhWcbWr%2BIEVEr4GDI%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275541219285282638&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

#### 高斯模糊

* 半径为5， sigma值为9。

POST http://ctaccel.com/api/v1?imageMogr2/blur/5x9

![blur_5x9](https://thumbnail0.baidupcs.com/thumbnail/02ee677a8cc19e94472aad083a503c20?fid=2117452681-250528-693482787211684&time=1565924400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-LEjYfZUPEH%2By0bardHRB%2BNusj%2Bg%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275563136475164396&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

#### 椭圆圆角

* 水平方向和垂直方向都为300像素

POST http://ctaccel.com/api/v1?imageMogr2/roundpic/300

![roundpic_300](https://thumbnail0.baidupcs.com/thumbnail/1a6de538aea729873734810753104a8c?fid=2117452681-250528-445270035845771&time=1565924400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-8kxFu0q4YMUzjeDA6qurZVUMags%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275631057405819431&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 水平方向为300px，　垂直方向为400px

POST http://ctaccel.com/api/v1?imageMogr2/roundpic/300x400

![roundpic_300x400](https://thumbnail0.baidupcs.com/thumbnail/dae176d98421cf83df1d58e003d3aaa1?fid=2117452681-250528-76613254296956&time=1565924400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-UIHMdMimpJi4BSqGBLdWPyU2dXs%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275641955506238410&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 水平方向和垂直方向都为原图片的30%大小

POST http://ctaccel.com/api/v1?imageMogr2/roundpic/!30p

![roundpic_s30p](https://thumbnail0.baidupcs.com/thumbnail/938b0822d92e49cfc2d3ece8db1fce58?fid=2117452681-250528-1098266142119336&time=1565924400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-EcHXVfMu6kzPZCWmxPu7g3jItbg%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275648723968573462&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

### 中心原图
* 中心原图半径为300px

POST http://ctaccel.com/api/v1?imageMogr2/iradius/300

![iradius_300](https://thumbnail0.baidupcs.com/thumbnail/4749fc137dbd517831872d863058070e?fid=2117452681-250528-205965934333302&time=1565924400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-fTJeD7BAWmWkBoc2vBQByAwfyk4%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275703655142058200&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* 中心原图直径为原宽高最小值的60%

POST http://ctaccel.com/api/v1?imageMogr2/iradius/!60p

![iradius_s60p](https://thumbnail0.baidupcs.com/thumbnail/f3252629bbc46d7268a79d52b23ae407?fid=2117452681-250528-854003021566859&time=1565924400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-4hTNq7ecrehkpQKrnlFjkEc50tQ%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5275711285942809246&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)