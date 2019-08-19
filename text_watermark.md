## 文字水印

image watermark 是将logo图片叠加到源图片上的功能。

### watermark

>**注意：**
>请忽略以下内容中的空格与换行符。

```
watermark/2
         /text/<encodedText>
         /font/<encodedFontName>
         /fontsize/<fontSize>
         /fill/<encodedTextColor>
         /dissolve/<dissolve>
         /gravity/<gravity>
         /dx/<distanceX>
         /dy/<distanceY>
```
### 参数说明

| 参数名称                 | 说明                                                         |
| :----------------------- | :----------------------------------------------------------- |
| /text/<encodedText>      | 水印文字内容（经过[URL安全的Base64编码）                     |
| /font/<encodedFontName>  | 水印文字字体（经过URL安全的Base64编码），默认为黑体          |
| /fontsize/<fontSize>     | 水印文字大小，单位: 缇 ，等于1/20磅，默认值是240缇，参考DPI为72。 |
| /fill/<encodedTextColor> | 水印文字颜色，RGB格式，可以是颜色名称（例如 red）或十六进制（例如 #FF0000）。默认为黑色。经过URL安全的Base64编码。 |
| /dissolve/<dissolve>     | 透明度，取值范围1-100，默认值为100（完全不透明）。           |
| /gravity/<gravity>       | 水印位置，默认值为`SouthEast`（右下角）。                    |
| /dx/<distanceX>          | 横轴边距，单位:像素(px)，默认值为10。                        |
| /dy/<distanceY>          | 纵轴边距，单位:像素(px)，默认值为10。                        |

#### 使用实例

* POST http://ctaccel.com/api/v1?watermark/2/text/5rWLQ1RBYWFhVHh0/dy/50/dx/50/fill/UmVk/dissolve/50/fontsize/900/gravity/center

![text-wm_all_params](https://thumbnail0.baidupcs.com/thumbnail/144797da571bad0e0a9ec9570bba09ce?fid=2117452681-250528-411646630646780&time=1565938800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-UThJWIq7f5a%2Btdo8nUAeGxF6RIs%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5279734138611829585&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

> **注意：**
> 请忽略以下内容中的空格与换行符。

```
watermark/4
         /text/<encodedText>
         /font/<encodedFontName>
         /fontsize/<fontSize>
         /fill/<encodedTextColor>
         /dissolve/<dissolve>
         /rotate/<rotate>
         /uw/<unitW>
         /uh/<unitH>
         /resize/<resize>
```

### 参数说明

| 参数名称                 | 说明                                                         |
| :----------------------- | :----------------------------------------------------------- |
| /text/<encodedText>      | 水印文字内容（经过[URL安全的Base64编码）                     |
| /font/<encodedFontName>  | 水印文字字体（经过URL安全的Base64编码），默认为黑体          |
| /fontsize/<fontSize>     | 水印文字大小，单位: 缇 ，等于1/20磅，默认值是240缇，参考DPI为72。 |
| /fill/<encodedTextColor> | 水印文字颜色，RGB格式，可以是颜色名称（例如 red）或十六进制（例如 #FF0000）。默认为黑色。经过URL安全的Base64编码。 |
| /dissolve/<dissolve>     | 透明度，取值范围1-100，默认值为100（完全不透明）。           |
| /rotate/<rotate>         | 水印文字旋转角度，[-180, 180]，默认为０。                    |
| /uw/<unitW>              | 水印文字填充单元宽度，默认值为 100。                         |
| /uh/<unitH>              | 水印文字填充单元高度，默认值为 100。                         |
| /resize/<resize>         | 水印文字填充单元缩放比例，[0.1, 10]，　默认为１ （不缩放）。 |



* POST  http://ctaccel.com/api/v1?watermark/4/text/5rWLQ1RBYWFhVHh0/uw/160/resize/1/uh/50/fill/UmVk/rotate/180/fontsize/500/font/5b6u6L2v6ZuF6buR/dissolve/100

![wm-m4_all_params](https://thumbnail0.baidupcs.com/thumbnail/67d030df62f483cfdda436e81b43a329?fid=2117452681-250528-111861808630421&time=1565938800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-HFjPPU5a4xezg3KbRqOEqqA9LgA%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5279833661073384042&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)