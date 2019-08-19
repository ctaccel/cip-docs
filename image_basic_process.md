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

![原图](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/image_origin.jpg)

* mode=0, w/400/h400变换成 400x300

  POST http://ctaccel.com/api/v1?imageView2/0/w/400/h/400

![mode0_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m0_400x400.jpeg)

* mode=1, w/400/h/400变换成 400x400

  POST http://ctaccel.com/api/v1?imageView2/1/w/400/h/400

![mode_1_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m1_400x400.jpeg)

* mode=2, w/400/h/400变换成400x300
  POST http://ctaccel.com/api/v1?imageView2/2/w/400/h/400

![mode2_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m2_400x400.jpeg)

* mode=3, w/400/h/400变换成533x400

  POST http://ctaccel.com/api/v1?imageView2/3/w/400/h/400

![mode3_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m3_400x400.jpeg)

* mode=4, w/400/h/400变换成533x400

  POST http://ctaccel.com/api/v1?imageView2/4/w/400/h/400

![mode4_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m4_400x400.jpeg)

* mode=5, w/400/h/400变换成400x400

  POST http://ctaccel.com/api/v1?imageView2/5/w/400/h/400

![mode5_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m5_400x400.jpeg)

* mode=0, w/400, 表示限定长边为400， 短边自适应。变换成400x300的图。

  POST http://ctaccel.com/api/v1?imageView2/0/w/400

![mode0_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m0_w400.jpeg)

* mode=1,  w/400，只指定w或h， 按比例缩放， 然后按中心裁剪为长宽相等的正方图， 变换成400x400的图。

  POST http://ctaccel.com/api/v1?imageView2/1/w/400

![mode_1_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m1_w400.jpeg)

* mode=2,  w/400， 宽最多为400， 高度自适应， 变换成400x300的图。

  POST http://ctaccel.com/api/v1?imageView2/2/w/400

![mode2_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m2_w400.jpeg)

* mode=3, w/400， 宽至少为400， 高也至少为400， 变换成533x400的图。

  POST http://ctaccel.com/api/v1?imageView2/3/w/400

![mode4_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m3_w400.jpeg)

* mode=4, w/400， 长边至少为400， 短边至少为400， 进行等比缩放。变换成533x400的图。

  POST http://ctaccel.com/api/v1?imageView2/4/w/400

![mode4_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m4_w400.jpeg)

* mode=5, w/400， 长边至少为400， 短边至少为400， 进行等比缩放。居中裁剪为400x400的图。
  POST http://ctaccel.com/api/v1?imageView2/5/w/400

![mode5_w400h400](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_m5_w400.jpeg)

* mode=1, w/400/h/400/format/png/q/70/fpga/false, 居中裁剪为400x400的图。输出格式为png。

  POST http://ctaccel.com/api/v1?imageView2/1/w/400/h/400/format/png/q/70/fpga/false

![mode1_all_params](https://raw.githubusercontent.com/ctaccel/cip-docs/master/images/imageview_all_params.png)
