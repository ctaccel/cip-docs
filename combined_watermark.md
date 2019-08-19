## 混合水印

混合水印用于同时在一个原图上打多个不同类型的水印。

### watermark

>**注意：**
>请忽略以下内容中的空格与换行符。

```
watermark/３
         /text/<textWaterMarkParams1>
         /image/<imageWaterMarkParams1>
         /image/<imageWaterMarkParams2>
         /text/<textWaterMarkParams2>
```
### 参数说明

| 参数名称                        | 说明             |
| :------------------------------ | :--------------- |
| `/image/<imageWaterMarkParams>` | 参考图片水印参数 |
| `/text/<textWaterMarkParams>`   | 参考文字水印参数 |

####　使用实例

POST http://192.168.55.93:8383/api/v1?imageMogr2/auto-orient/format/png|watermark/3/image/aHR0cDovLzd4bHY0Ny5jb20wLnowLmdsYi5jbG91ZGRuLmNvbS94aWFvamkucG5n/gravity/North/dy/-10/dx/0/text/5ZCD6L-H54yr5bGx546L77yM5YW25LuW5qa06I6y55qG6Lev5Lq6/gravity/SouthWest/dx/10/dy/180/fontsize/500/text/5LuF6ZmQN-WkqSAgMjAxOS4wNC4wMS0yMDE5LjA0LjA3/gravity/SouthWest/dx/30/dy/130/fontsize/300/image/aHR0cDovLzd4bHY0Ny5jb20wLnowLmdsYi5jbG91ZGRuLmNvbS9xdWFuLnBuZw==/gravity/SouthWest/dx/80/dy/30/image/aHR0cDovLzd4bHY0Ny5jb20wLnowLmdsYi5jbG91ZGRuLmNvbS_kuoznu7TnoIEucG5n/gravity/SouthEast/dx/10/dy/30/text/5omr56CB6aKG5Y-W5LyY5oOg5Yi4/gravity/SouthEast/dx/20/dy/10/fontsize/300/fill/UmVk

注意：　id=http://7xlv47.com0.z0.glb.clouddn.com/baidi.png

![watermark_m1_all_params](https://thumbnail0.baidupcs.com/thumbnail/65fac8d018f5c29b4e1f7228d5912824?fid=2117452681-250528-1062396298115126&time=1565938800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-UakZZC4JUfhvDr4zjzKw0MrhFH0%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5280131426579087993&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)

