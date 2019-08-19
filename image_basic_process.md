## 图片基本处理

imageView2 是图片基本处理的接口，简单，功能强大的图像处理接口，包括裁剪、压缩、格式转换等。

### imageView2

>**注意：**
>请忽略以下内容中的空格与换行符。

```
imageView2/<mode>/w/<LongEdge>
                    /h/<ShortEdge>
                    /format/<Format>
                    /q/<Quality>
                    /fpga/<Fpga>
```
### 参数说明
| Item              | Value                                              | Description                                   | Optional |
| ----------------- | -------------------------------------------------- | --------------------------------------------- | -------- |
| imageView2/<mode> | 0, 1, 2, 3, 4, 5                                   | 参考mode参数详细说明， 包括一下w和h参数说明。 | M        |
| /format/<Format>  | `jpg`，`gif`，`png`，`webp`等， 默认为原图输出格式 | 新图的输出格式                                | O        |
| /q/<Quality>      | 取值范围1-100， 默认值75                           | 新图的输出质量                                | O        |
| /fpga/<Fpga>      | 是否使用cip加速， 默认为true                       | 使用fpga加速卡                                | O        |

#### 关于mode说明

| mode                            | description                                                  |
| :------------------------------ | :----------------------------------------------------------- |
| `/0/w/<LongEdge>/h/<ShortEdge>` | 限定缩略图的长边最多为`<LongEdge>`，短边最多为`<ShortEdge>`，进行等比缩放，不裁剪。如果只指定 `w` 参数则表示限定长边（短边自适应），只指定 `h` 参数则表示限定短边（长边自适应）。 |
| `/1/w/<Width>/h/<Height>`       | 限定缩略图的宽最少为`<Width>`，高最少为`<Height>`，进行等比缩放，居中裁剪。转后的缩略图通常恰好是 `<Width>x<Height>` 的大小（有一个边缩放的时候会因为超出矩形框而被裁剪掉多余部分）。如果只指定 `w` 参数或只指定 `h` 参数，代表限定为长宽相等的正方图。 |
| `/2/w/<Width>/h/<Height>`       | 限定缩略图的宽最多为`<Width>`，高最多为`<Height>`，进行等比缩放，不裁剪。如果只指定 `w` 参数则表示限定宽（长自适应），只指定 `h` 参数则表示限定长（宽自适应）。它和模式0类似，区别只是限定宽和高，不是限定长边和短边。从应用场景来说，模式0适合移动设备上做缩略图，模式2适合PC上做缩略图。 |
| `/3/w/<Width>/h/<Height>`       | 限定缩略图的宽最少为`<Width>`，高最少为`<Height>`，进行等比缩放，不裁剪。如果只指定 `w` 参数或只指定 `h`参数，代表长宽限定为同样的值。你可以理解为模式1是模式3的结果再做居中裁剪得到的。 |
| `/4/w/<LongEdge>/h/<ShortEdge>` | 限定缩略图的长边最少为`<LongEdge>`，短边最少为`<ShortEdge>`，进行等比缩放，不裁剪。如果只指定 `w` 参数或只指定 `h` 参数，表示长边短边限定为同样的值。这个模式很适合在手持设备做图片的全屏查看（把这里的长边短边分别设为手机屏幕的分辨率即可），生成的图片尺寸刚好充满整个屏幕（某一个边可能会超出屏幕）。 |
| `/5/w/<LongEdge>/h/<ShortEdge>` | 限定缩略图的长边最少为`<LongEdge>`，短边最少为`<ShortEdge>`，进行等比缩放，居中裁剪。如果只指定 `w` 参数或只指定 `h` 参数，表示长边短边限定为同样的值。同上模式4，但超出限定的矩形部分会被裁剪。 |

### 示例
#### 实时

* 原图: 1280x768

![原图](https://thumbnail0.baidupcs.com/thumbnail/fd59ce035fab0e8e1cb621e27c1e204c?fid=2117452681-250528-87487597832349&time=1565848800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-pIHdCSDQ1WKJ12WTUcTxV8UwHHM%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5255874777737654587&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=0, w/400/h400变换成 400x300

  POST http://ctaccel.com/api/v1?imageView2/0/w/400/h/400

![mode0_w400h400](https://thumbnail0.baidupcs.com/thumbnail/c9588f435dc3cfc804f698d84f46e548?fid=2117452681-250528-24708815581521&time=1565859600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-K604VZ6n8X83q6v5nl3pEttfueg%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5258598137571778377&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=1, w/400/h/400变换成 400x400

  POST http://ctaccel.com/api/v1?imageView2/1/w/400/h/400

![mode_1_w400h400](https://thumbnail0.baidupcs.com/thumbnail/038618cf347353be59098e0acab2b95d?fid=2117452681-250528-833328866622731&time=1565852400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-yilYrohq%2FOGY2KEHCzb78pxOYYQ%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5256779551481740548&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=2, w/400/h/400变换成400x300
  POST http://ctaccel.com/api/v1?imageView2/2/w/400/h/400

![mode2_w400h400](https://thumbnail0.baidupcs.com/thumbnail/c9588f435dc3cfc804f698d84f46e548?fid=2117452681-250528-339479685599223&time=1565852400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-PCtOJbuEr9kQ0EdbC4qFFJpTiTw%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5256843417143375591&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=3, w/400/h/400变换成533x400

  POST http://ctaccel.com/api/v1?imageView2/3/w/400/h/400

![mode3_w400h400](https://thumbnail0.baidupcs.com/thumbnail/e2aa8991f1a1bf4674d76d2eded4df95?fid=2117452681-250528-946058103255624&time=1565852400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-p20bNu2lvyZob5pTtATN9DlxLaQ%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5256894521303482293&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=4, w/400/h/400变换成533x400

  POST http://ctaccel.com/api/v1?imageView2/4/w/400/h/400

![mode4_w400h400](https://thumbnail0.baidupcs.com/thumbnail/e2aa8991f1a1bf4674d76d2eded4df95?fid=2117452681-250528-477419117728505&time=1565859600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-bQbHARjs5O9NdHw3%2FLvAA24DQd8%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5258373788021590339&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=5, w/400/h/400变换成400x400

  POST http://ctaccel.com/api/v1?imageView2/5/w/400/h/400

![mode5_w400h400](https://thumbnail0.baidupcs.com/thumbnail/038618cf347353be59098e0acab2b95d?fid=2117452681-250528-645697363792699&time=1565859600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-QYqpD%2FrhZiKrlVbmM2MkxU0D6yQ%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5258419049796294449&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=0, w/400, 表示限定长边为400， 短边自适应。变换成400x300的图。

  POST http://ctaccel.com/api/v1?imageView2/0/w/400

![mode0_w400h400](https://thumbnail0.baidupcs.com/thumbnail/c9588f435dc3cfc804f698d84f46e548?fid=2117452681-250528-24708815581521&time=1565859600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-K604VZ6n8X83q6v5nl3pEttfueg%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5258598137571778377&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=1,  w/400，只指定w或h， 按比例缩放， 然后按中心裁剪为长宽相等的正方图， 变换成400x400的图。

  POST http://ctaccel.com/api/v1?imageView2/1/w/400

![mode_1_w400h400](https://thumbnail0.baidupcs.com/thumbnail/038618cf347353be59098e0acab2b95d?fid=2117452681-250528-833328866622731&time=1565852400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-yilYrohq%2FOGY2KEHCzb78pxOYYQ%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5256779551481740548&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=2,  w/400， 宽最多为400， 高度自适应， 变换成400x300的图。

  POST http://ctaccel.com/api/v1?imageView2/2/w/400

![mode2_w400h400](https://thumbnail0.baidupcs.com/thumbnail/c9588f435dc3cfc804f698d84f46e548?fid=2117452681-250528-339479685599223&time=1565852400&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-PCtOJbuEr9kQ0EdbC4qFFJpTiTw%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5256843417143375591&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=3, w/400， 宽至少为400， 高也至少为400， 变换成533x400的图。

  POST http://ctaccel.com/api/v1?imageView2/3/w/400

![mode4_w400h400](https://thumbnail0.baidupcs.com/thumbnail/e2aa8991f1a1bf4674d76d2eded4df95?fid=2117452681-250528-477419117728505&time=1565859600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-bQbHARjs5O9NdHw3%2FLvAA24DQd8%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5258373788021590339&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=4, w/400， 长边至少为400， 短边至少为400， 进行等比缩放。变换成533x400的图。

  POST http://ctaccel.com/api/v1?imageView2/4/w/400

![mode4_w400h400](https://thumbnail0.baidupcs.com/thumbnail/e2aa8991f1a1bf4674d76d2eded4df95?fid=2117452681-250528-477419117728505&time=1565859600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-bQbHARjs5O9NdHw3%2FLvAA24DQd8%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5258373788021590339&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=5, w/400， 长边至少为400， 短边至少为400， 进行等比缩放。居中裁剪为400x400的图。
  POST http://ctaccel.com/api/v1?imageView2/5/w/400

![mode5_w400h400](https://thumbnail0.baidupcs.com/thumbnail/038618cf347353be59098e0acab2b95d?fid=2117452681-250528-645697363792699&time=1565859600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-QYqpD%2FrhZiKrlVbmM2MkxU0D6yQ%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5258419049796294449&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

* mode=1, w/400/h/400/format/png/q/70/fpga/false, 居中裁剪为400x400的图。输出格式为png。

  POST http://ctaccel.com/api/v1?imageView2/1/w/400/h/400/format/png/q/70/fpga/false

![mode1_all_params](https://thumbnail0.baidupcs.com/thumbnail/23b7e1c9755a6d21bec8dc44651fc867?fid=2117452681-250528-486309331441357&time=1565863200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-Kq%2FAjyeqbphWlhEURm%2FW%2BXM996k%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5259133562143702868&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)