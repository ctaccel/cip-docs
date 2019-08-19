## 图片水印

image watermark 是将logo图片叠加到源图片上的功能。

### watermark

>**注意：**
>请忽略以下内容中的空格与换行符。

```
watermark/1
         /image/<encodedImageURL>
         /dissolve/<dissolve>
         /gravity/<gravity>
         /dx/<distanceX>
         /dy/<distanceY>
         /ws/<watermarkScale>
         /wst/<watermarkScaleType>
```
### 参数说明

| 参数名称                    | 说明                                                         |
| :-------------------------- | :----------------------------------------------------------- |
| `/image/<encodedImageURL>`  | 水印源图片网址（经过URL安全的Base64编码），必须有效且返回一张图片。 |
| `/dissolve/<dissolve>`      | 透明度，取值范围1-100，默认值为100（完全不透明）。           |
| `/gravity/<gravity>`        | 水印位置，默认值为`SouthEast`（右下角）。                    |
| `/dx/<distanceX>`           | 横轴边距，单位:像素(px)，默认值为10。                        |
| `/dy/<distanceY>`           | 纵轴边距，单位:像素(px)，默认值为10。                        |
| `/ws/<watermarkScale>`      | 水印图片自适应原图的短边比例，ws的取值范围为0-1。具体是指水印图片保持原比例，并短边缩放到原图短边＊ws。 |
| `/wst/<watermarkScaleType>` | 水印图片自适应原图的类型，取值0、1、2、3分别表示为自适应原图的短边、长边、宽、高，默认值为0 |

例如：原图大小为250x250，水印图片大小为91x61，如果ws=1，那么最终水印图片的大小为：372x250。

####　使用实例

POST http://ctaccel.com/api/v1?watermark/1/image/aHR0cDovL3d3dy5wbmdhbGwuY29tL3dwLWNvbnRlbnQvdXBsb2Fkcy8yMDE2LzA1L1B5dGhvbi1Mb2dvLUZyZWUtRG93bmxvYWQtUE5HLnBuZw==/dissolve/80/gravity/center/dx/200/dy/100/ws/1/wst/0

![watermark_m1_all_params](https://thumbnail0.baidupcs.com/thumbnail/be65778441944c7049dfaf282b17d54b?fid=2117452681-250528-239371711410389&time=1565938800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-EdzacxDjBljrOQ6vcaCiP%2BsIcy8%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5279480095906046945&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

