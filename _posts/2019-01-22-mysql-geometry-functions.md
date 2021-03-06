---
layout: post
title: 'MySQL空间函数'
date: 2019-01-22
author: wutong
tags:  mysql mariadb
---

在日常项目少不了基于位置的功能，比如附近餐馆、单车运行轨迹，这些都可以存储为空间类型的字段，随着MySQL的升级，其空间函数也向规范标准靠拢，本表格则是空间函数的列表并包含了废弃的提醒

<table>
	<thead>
		<tr>
			<th scope="col">名称</th>
			<th scope="col">描述</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-polygon-property-functions.html#function_area"><code>Area()</code></a> （已弃用5.7.6）</td>
			<td>返回Polygon或MultiPolygon区域</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-format-conversion-functions.html#function_asbinary"><code>AsBinary()</code>，<code>AsWKB()</code></a>（已弃用5.7.6）</td>
			<td>从内部几何格式转换为WKB</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-format-conversion-functions.html#function_astext"><code>AsText()</code>，<code>AsWKT()</code></a>（已弃用5.7.6）</td>
			<td>从内部几何格式转换为WKT</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-operator-functions.html#function_buffer"><code>Buffer()</code></a> （已弃用5.7.6）</td>
			<td>返回距离几何体的给定距离内的点的几何</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-polygon-property-functions.html#function_centroid"><code>Centroid()</code></a> （已弃用5.7.6）</td>
			<td>返回质心作为一个点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_contains"><code>Contains()</code></a> （已弃用5.7.6）</td>
			<td>一个几何的MBR是否包含另一个几何的MBR</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-operator-functions.html#function_convexhull"><code>ConvexHull()</code></a> （已弃用5.7.6）</td>
			<td>返回几何体的凸包</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_crosses"><code>Crosses()</code></a> （已弃用5.7.6）</td>
			<td>一个几何是否与另一个几何相交</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_dimension"><code>Dimension()</code></a> （已弃用5.7.6）</td>
			<td>几何尺寸</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_disjoint"><code>Disjoint()</code></a> （已弃用5.7.6）</td>
			<td>两个几何形状的MBR是否不相交</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_distance"><code>Distance()</code></a> （已弃用5.7.6）</td>
			<td>一个几何与另一个几何的距离</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_endpoint"><code>EndPoint()</code></a> （已弃用5.7.6）</td>
			<td>LineString的终点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_envelope"><code>Envelope()</code></a> （已弃用5.7.6）</td>
			<td>返回几何的MBR</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_equals"><code>Equals()</code></a> （已弃用5.7.6）</td>
			<td>两个几何的MBR是否相等</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-polygon-property-functions.html#function_exteriorring"><code>ExteriorRing()</code></a> （已弃用5.7.6）</td>
			<td>返回Polygon的外环</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_geomcollfromtext"><code>GeomCollFromText()</code><br>
<code>GeometryCollectionFromText()</code></a>（已弃用5.7.6）</td>
			<td>从WKT返回几何集合</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_geomcollfromwkb"><code>GeomCollFromWKB()</code><br>
<code>GeometryCollectionFromWKB()</code></a>（已弃用5.7.6）</td>
			<td>从WKB返回几何集合</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-mysql-specific-functions.html#function_geometrycollection"><code>GeometryCollection()</code></a></td>
			<td>从几何构造几何集合</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-geometrycollection-property-functions.html#function_geometryn"><code>GeometryN()</code></a> （已弃用5.7.6）</td>
			<td>从几何集合中返回第N个几何</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_geometrytype"><code>GeometryType()</code></a> （已弃用5.7.6）</td>
			<td>返回几何类型的名称</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_geomfromtext"><code>GeomFromText()</code><br>
<code>GeometryFromText()</code></a>（已弃用5.7.6）</td>
			<td>从WKT返回几何</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_geomfromwkb"><code>GeomFromWKB()</code><br>
<code>GeometryFromWKB()</code></a>（已弃用5.7.6）</td>
			<td>从WKB返回几何</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_glength"><code>GLength()</code></a> （已弃用5.7.6）</td>
			<td>返回LineString的长度</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-polygon-property-functions.html#function_interiorringn"><code>InteriorRingN()</code></a> （已弃用5.7.6）</td>
			<td>返回Polygon的第N个内环</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_intersects"><code>Intersects()</code></a> （已弃用5.7.6）</td>
			<td>两个几何的MBR是否相交</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_isclosed"><code>IsClosed()</code></a> （已弃用5.7.6）</td>
			<td>几何是否封闭且简单</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_isempty"><code>IsEmpty()</code></a> （已弃用5.7.6）</td>
			<td>占位符功能</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_issimple"><code>IsSimple()</code></a> （已弃用5.7.6）</td>
			<td>几何是否简单</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_linefromtext"><code>LineFromText()</code><br>
<code>LineStringFromText()</code></a>（已弃用5.7.6）</td>
			<td>从WKT构造LineString</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_linefromwkb"><code>LineFromWKB()</code><br>
<code>LineStringFromWKB()</code></a>（已弃用5.7.6）</td>
			<td>从WKB构造LineString</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-mysql-specific-functions.html#function_linestring"><code>LineString()</code></a></td>
			<td>从Point值构造LineString</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_mbrcontains"><code>MBRContains()</code></a></td>
			<td>一个几何的MBR是否包含另一个几何的MBR</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_mbrcoveredby"><code>MBRCoveredBy()</code></a></td>
			<td>一个MBR是否被另一个MBR覆盖</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_mbrcovers"><code>MBRCovers()</code></a></td>
			<td>一个MBR是否涵盖另一个MBR</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_mbrdisjoint"><code>MBRDisjoint()</code></a></td>
			<td>两个几何形状的MBR是否不相交</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_mbrequal"><code>MBREqual()</code></a> （已弃用5.7.6）</td>
			<td>两个几何的MBR是否相等</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_mbrequals"><code>MBREquals()</code></a></td>
			<td>两个几何的MBR是否相等</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_mbrintersects"><code>MBRIntersects()</code></a></td>
			<td>两个几何的MBR是否相交</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_mbroverlaps"><code>MBROverlaps()</code></a></td>
			<td>两个几何的MBR是否重叠</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_mbrtouches"><code>MBRTouches()</code></a></td>
			<td>两种几何形状的MBR是否接触</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_mbrwithin"><code>MBRWithin()</code></a></td>
			<td>一个几何的MBR是否在另一个几何的MBR内</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_mlinefromtext"><code>MLineFromText()</code><br>
<code>MultiLineStringFromText()</code></a>（已弃用5.7.6）</td>
			<td>从WKT构造MultiLineString</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_mlinefromwkb"><code>MLineFromWKB()</code><br>
<code>MultiLineStringFromWKB()</code></a>（已弃用5.7.6）</td>
			<td>从WKB构造MultiLineString</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_mpointfromtext"><code>MPointFromText()</code><br>
<code>MultiPointFromText()</code></a>（已弃用5.7.6）</td>
			<td>从WKT构造MultiPoint</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_mpointfromwkb"><code>MPointFromWKB()</code><br>
<code>MultiPointFromWKB()</code></a>（已弃用5.7.6）</td>
			<td>从WKB构造MultiPoint</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_mpolyfromtext"><code>MPolyFromText()</code><br>
<code>MultiPolygonFromText()</code></a>（已弃用5.7.6）</td>
			<td>从WKT构造MultiPolygon</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_mpolyfromwkb"><code>MPolyFromWKB()</code><br>
<code>MultiPolygonFromWKB()</code></a>（已弃用5.7.6）</td>
			<td>从WKB构造MultiPolygon</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-mysql-specific-functions.html#function_multilinestring"><code>MultiLineString()</code></a></td>
			<td>从LineString值构造MultiLineString</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-mysql-specific-functions.html#function_multipoint"><code>MultiPoint()</code></a></td>
			<td>从Point值构造MultiPoint</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-mysql-specific-functions.html#function_multipolygon"><code>MultiPolygon()</code></a></td>
			<td>从Polygon值构造MultiPolygon</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-geometrycollection-property-functions.html#function_numgeometries"><code>NumGeometries()</code></a> （已弃用5.7.6）</td>
			<td>返回几何集合中的几何数量</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-polygon-property-functions.html#function_numinteriorrings"><code>NumInteriorRings()</code></a> （已弃用5.7.6）</td>
			<td>返回多边形内圈的数量</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_numpoints"><code>NumPoints()</code></a> （已弃用5.7.6）</td>
			<td>返回LineString中的点数</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_overlaps"><code>Overlaps()</code></a> （已弃用5.7.6）</td>
			<td>两个几何的MBR是否重叠</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-mysql-specific-functions.html#function_point"><code>Point()</code></a></td>
			<td>从坐标构造点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_pointfromtext"><code>PointFromText()</code></a> （已弃用5.7.6）</td>
			<td>从WKT构建点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_pointfromwkb"><code>PointFromWKB()</code></a> （已弃用5.7.6）</td>
			<td>从WKB构造点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_pointn"><code>PointN()</code></a> （已弃用5.7.6）</td>
			<td>从LineString返回第N个点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_polyfromtext"><code>PolyFromText()</code><br>
<code>PolygonFromText()</code></a>（已弃用5.7.6）</td>
			<td>从WKT构造多边形</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_polyfromwkb"><code>PolyFromWKB()</code><br>
<code>PolygonFromWKB()</code></a>（已弃用5.7.6）</td>
			<td>从WKB构造多边形</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-mysql-specific-functions.html#function_polygon"><code>Polygon()</code></a></td>
			<td>从LineString参数构造多边形</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_srid"><code>SRID()</code></a> （已弃用5.7.6）</td>
			<td>返回几何的空间参考系统ID</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-polygon-property-functions.html#function_st-area"><code>ST_Area()</code></a></td>
			<td>返回Polygon或MultiPolygon区域</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-format-conversion-functions.html#function_st-asbinary"><code>ST_AsBinary()</code><br>
<code>ST_AsWKB()</code></a></td>
			<td>从内部几何格式转换为WKB</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-geojson-functions.html#function_st-asgeojson"><code>ST_AsGeoJSON()</code></a></td>
			<td>从几何体生成GeoJSON对象</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-format-conversion-functions.html#function_st-astext"><code>ST_AsText()</code><br>
<code>ST_AsWKT()</code></a></td>
			<td>从内部几何格式转换为WKT</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-operator-functions.html#function_st-buffer"><code>ST_Buffer()</code></a></td>
			<td>返回距离几何体的给定距离内的点的几何</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-operator-functions.html#function_st-buffer-strategy"><code>ST_Buffer_Strategy()</code></a></td>
			<td>为ST_Buffer（）生成策略选项</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-polygon-property-functions.html#function_st-centroid"><code>ST_Centroid()</code></a></td>
			<td>返回质心作为一个点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_st-contains"><code>ST_Contains()</code></a></td>
			<td>一个几何是否包含另一个</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-operator-functions.html#function_st-convexhull"><code>ST_ConvexHull()</code></a></td>
			<td>返回几何体的凸包</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_st-crosses"><code>ST_Crosses()</code></a></td>
			<td>一个几何是否与另一个几何相交</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-operator-functions.html#function_st-difference"><code>ST_Difference()</code></a></td>
			<td>两个几何的返回点集差异</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_st-dimension"><code>ST_Dimension()</code></a></td>
			<td>几何尺寸</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_st-disjoint"><code>ST_Disjoint()</code></a></td>
			<td>一个几何是否与另一个几何脱节</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_st-distance"><code>ST_Distance()</code></a></td>
			<td>一个几何与另一个几何的距离</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-convenience-functions.html#function_st-distance-sphere"><code>ST_Distance_Sphere()</code></a></td>
			<td>两个几何形状之间的最小地球距离</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_st-endpoint"><code>ST_EndPoint()</code></a></td>
			<td>LineString的终点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_st-envelope"><code>ST_Envelope()</code></a></td>
			<td>返回几何的MBR</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_st-equals"><code>ST_Equals()</code></a></td>
			<td>一个几何是否与另一个几何相等</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-polygon-property-functions.html#function_st-exteriorring"><code>ST_ExteriorRing()</code></a></td>
			<td>返回Polygon的外环</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-geohash-functions.html#function_st-geohash"><code>ST_GeoHash()</code></a></td>
			<td>产生geohash值</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_st-geomcollfromtext"><code>ST_GeomCollFromText()</code><br>
<code>ST_GeometryCollectionFromText()</code><br>
<code>ST_GeomCollFromTxt()</code></a></td>
			<td>从WKT返回几何集合</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_st-geomcollfromwkb"><code>ST_GeomCollFromWKB()</code><br>
<code>ST_GeometryCollectionFromWKB()</code></a></td>
			<td>从WKB返回几何集合</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-geometrycollection-property-functions.html#function_st-geometryn"><code>ST_GeometryN()</code></a></td>
			<td>从几何集合中返回第N个几何</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_st-geometrytype"><code>ST_GeometryType()</code></a></td>
			<td>返回几何类型的名称</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-geojson-functions.html#function_st-geomfromgeojson"><code>ST_GeomFromGeoJSON()</code></a></td>
			<td>从GeoJSON对象生成几何</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_st-geomfromtext"><code>ST_GeomFromText()</code><br>
<code>ST_GeometryFromText()</code></a></td>
			<td>从WKT返回几何</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_st-geomfromwkb"><code>ST_GeomFromWKB()</code><br>
<code>ST_GeometryFromWKB()</code></a></td>
			<td>从WKB返回几何</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-polygon-property-functions.html#function_st-interiorringn"><code>ST_InteriorRingN()</code></a></td>
			<td>返回Polygon的第N个内环</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-operator-functions.html#function_st-intersection"><code>ST_Intersection()</code></a></td>
			<td>返回点设置两个几何的交集</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_st-intersects"><code>ST_Intersects()</code></a></td>
			<td>一个几何是否与另一个相交</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_st-isclosed"><code>ST_IsClosed()</code></a></td>
			<td>几何是否封闭且简单</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_st-isempty"><code>ST_IsEmpty()</code></a></td>
			<td>占位符功能</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_st-issimple"><code>ST_IsSimple()</code></a></td>
			<td>几何是否简单</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-convenience-functions.html#function_st-isvalid"><code>ST_IsValid()</code></a></td>
			<td>几何是否有效</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-geohash-functions.html#function_st-latfromgeohash"><code>ST_LatFromGeoHash()</code></a></td>
			<td>从geohash值返回纬度</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_st-length"><code>ST_Length()</code></a></td>
			<td>返回LineString的长度</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_st-linefromtext"><code>ST_LineFromText()</code><br>
<code>ST_LineStringFromText()</code></a></td>
			<td>从WKT构造LineString</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_st-linefromwkb"><code>ST_LineFromWKB()</code><br>
<code>ST_LineStringFromWKB()</code></a></td>
			<td>从WKB构造LineString</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-geohash-functions.html#function_st-longfromgeohash"><code>ST_LongFromGeoHash()</code></a></td>
			<td>从geohash值返回经度</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-convenience-functions.html#function_st-makeenvelope"><code>ST_MakeEnvelope()</code></a></td>
			<td>两点左右的矩形</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_st-mlinefromtext"><code>ST_MLineFromText()</code><br>
<code>ST_MultiLineStringFromText()</code></a></td>
			<td>从WKT构造MultiLineString</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_st-mlinefromwkb"><code>ST_MLineFromWKB()</code><br>
<code>ST_MultiLineStringFromWKB()</code></a></td>
			<td>从WKB构造MultiLineString</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_st-mpointfromtext"><code>ST_MPointFromText()</code><br>
<code>ST_MultiPointFromText()</code></a></td>
			<td>从WKT构造MultiPoint</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_st-mpointfromwkb"><code>ST_MPointFromWKB()</code><br>
<code>ST_MultiPointFromWKB()</code></a></td>
			<td>从WKB构造MultiPoint</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_st-mpolyfromtext"><code>ST_MPolyFromText()</code><br>
<code>ST_MultiPolygonFromText()</code></a></td>
			<td>从WKT构造MultiPolygon</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_st-mpolyfromwkb"><code>ST_MPolyFromWKB()</code><br>
<code>ST_MultiPolygonFromWKB()</code></a></td>
			<td>从WKB构造MultiPolygon</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-geometrycollection-property-functions.html#function_st-numgeometries"><code>ST_NumGeometries()</code></a></td>
			<td>返回几何集合中的几何数量</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-polygon-property-functions.html#function_st-numinteriorrings"><code>ST_NumInteriorRing()</code><br>
<code>ST_NumInteriorRings()</code></a></td>
			<td>返回多边形内圈的数量</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_st-numpoints"><code>ST_NumPoints()</code></a></td>
			<td>返回LineString中的点数</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_st-overlaps"><code>ST_Overlaps()</code></a></td>
			<td>一个几何是否与另一个重叠</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-geohash-functions.html#function_st-pointfromgeohash"><code>ST_PointFromGeoHash()</code></a></td>
			<td>将geohash值转换为POINT值</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_st-pointfromtext"><code>ST_PointFromText()</code></a></td>
			<td>从WKT构建点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_st-pointfromwkb"><code>ST_PointFromWKB()</code></a></td>
			<td>从WKB构造点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_st-pointn"><code>ST_PointN()</code></a></td>
			<td>从LineString返回第N个点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkt-functions.html#function_st-polyfromtext"><code>ST_PolyFromText()</code><br>
<code>ST_PolygonFromText()</code></a></td>
			<td>从WKT构造多边形</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-wkb-functions.html#function_st-polyfromwkb"><code>ST_PolyFromWKB()</code><br>
<code>ST_PolygonFromWKB()</code></a></td>
			<td>从WKB构造多边形</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-convenience-functions.html#function_st-simplify"><code>ST_Simplify()</code></a></td>
			<td>返回简化几何</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-general-property-functions.html#function_st-srid"><code>ST_SRID()</code></a></td>
			<td>返回几何的空间参考系统ID</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_st-startpoint"><code>ST_StartPoint()</code></a></td>
			<td>LineString的起始点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-operator-functions.html#function_st-symdifference"><code>ST_SymDifference()</code></a></td>
			<td>返回点设置两个几何的对称差异</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_st-touches"><code>ST_Touches()</code></a></td>
			<td>一个几何是否接触另一个</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-operator-functions.html#function_st-union"><code>ST_Union()</code></a></td>
			<td>返回点集两个几何的并集</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-convenience-functions.html#function_st-validate"><code>ST_Validate()</code></a></td>
			<td>返回验证的几何体</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_st-within"><code>ST_Within()</code></a></td>
			<td>一个几何是否在另一个之内</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-point-property-functions.html#function_st-x"><code>ST_X()</code></a></td>
			<td>返回Point的X坐标</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-point-property-functions.html#function_st-y"><code>ST_Y()</code></a></td>
			<td>返回Point的Y坐标</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-linestring-property-functions.html#function_startpoint"><code>StartPoint()</code></a> （已弃用5.7.6）</td>
			<td>LineString的起始点</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-object-shapes.html#function_touches"><code>Touches()</code></a> （已弃用5.7.6）</td>
			<td>一个几何是否接触另一个</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/spatial-relation-functions-mbr.html#function_within"><code>Within()</code></a> （已弃用5.7.6）</td>
			<td>一个几何的MBR是否在另一个几何的MBR内</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-point-property-functions.html#function_x"><code>X()</code></a> （已弃用5.7.6）</td>
			<td>返回Point的X坐标</td>
		</tr>
		<tr>
			<td scope="row"><a href="https://dev.mysql.com/doc/refman/5.7/en/gis-point-property-functions.html#function_y"><code>Y()</code></a> （已弃用5.7.6）</td>
			<td>返回Point的Y坐标</td>
		</tr>
	</tbody>
</table>
