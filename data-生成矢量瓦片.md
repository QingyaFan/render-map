# 生成矢量瓦片的方法

## 使用postgis

Postgis2.4.0增加了生成矢量切片的功能： `ST_AsMVTGeom`、`ST_AsMVT`，利用它们可以从geometry字段生成字符串表示的矢量切片，我们还可以将字符串保存到文件，将文件按照一定的形式组织，即可像栅格切片一样使用矢量切片。

首先需要将geometry从自己的坐标系转换到mvt的坐标空间（coordinate space），这里用到的就是`ST_AsMVTGeom`，函数签名如下：

```sql
geometry ST_AsMVTGeom(geometry geom, box2d bounds, integer extent=4096, integer buffer=256, boolean clip_geom=true);
```

- geom，待转换的空间字段；
- bounds，瓦片坐标空间中切片的范围，不包含buffer；
- extent，瓦片坐标空间中切片的范围；
- buffer，瓦片坐标空间中缓冲区的距离；
- clip_geom，geometry是否应该切割或者编码。

接下来我们就可以将空间数据转换为矢量瓦片格式：

```sql
bytea ST_AsMVT(anyelement row, text name, integer extent, text geom_name);
```

- row,至少包含一列geometry的数据；
- name,图层的名称，默认为'default'；
- extent,瓦片的extent，默认4096；
- geom_name,row中包含的geometry类型的列名称。