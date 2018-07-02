---
layout: post
title: '中国行政区域导入数据库'
date: 2018-07-03
author: wutong
tags:  linux php mysql mariadb
---

对于开发人员来说经常会使用到行政区相关的数据，比如级联菜单等，但是维护其中的数据比较麻烦，本文则是来解决如何不自己去维护的问题

## 行政区域来源

百度维护了一个行政区域的excel表，这样就不用我们来维护了，直接每隔一段时间下载他的excel来进行导入就行了，并且百度地图的省市区也是对应这个excel的，所以使用起来也很方便

 > 下载地址：http://lbsyun.baidu.com/index.php?title=open/dev-res
 
## 导入数据库
 
 准备一张表。自己根据需要创建相关结构，我自己用的如下结构：
 
 ```sql
CREATE TABLE `region` (
  `id` smallint(5) unsigned NOT NULL AUTO_INCREMENT,
  `parent_id` smallint(5) unsigned NOT NULL DEFAULT '0' COMMENT '所属父区域',
  `name` varchar(120) NOT NULL DEFAULT '' COMMENT '区域名称',
  `code` varchar(10) NOT NULL DEFAULT '' COMMENT '区域代码',
  PRIMARY KEY (`id`),
  KEY `parent_id` (`parent_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8 ROW_FORMAT=DYNAMIC COMMENT='区域';
```

将下列代码保存并执行，填上excel的路径、数据库信息即可，使用之前需要执行一下 `composer require phpoffice/phpspreadsheet`

```php
<?php

use PhpOffice\PhpSpreadsheet\IOFactory;

require "vendor/autoload.php";

//行政区excel
$excelPath = '/Users/wutong/Downloads/行政区域.xlsx';
echo "导入文件：" . $excelPath . "\n";

$pdo = getPdo();
$sheet = getExcelSheet($excelPath);

//所有区域
$regions = $sheet->toArray();

//要保存到数据中的记录集合
$records = [];

//当前省份、城市
$currentProvince = null;
$currentCity = null;

//直辖市列表
$zhiXiaCities = ['北京', '天津', '上海', '重庆'];

//循环处理区域
foreach ($regions as $i => $region) {
    //是否是直辖市
    $zhiXiaCity = false;
    if ($i == 0) {
        continue;
    }
    //如果第5栏和第6栏是空的则是省份
    if ($region[4] == '' && $region[5] == '') {
        if ($currentCity != null) {
            $currentProvince['children'][] = $currentCity;
        }
        $currentCity = null;
        if ($currentProvince != null) {
            $records[] = $currentProvince;
        }
        //直辖市
        if ($region[1] == $region[2] && $region[2] == $region[3] && in_array(mb_substr($region[1], 0, 2), $zhiXiaCities)) {
            $zhiXiaCity = true;
        }
        $currentProvince = [
            'name'     => $region[1],
            'code'     => $region[6],
            'zhixia'   => $zhiXiaCity,
            'children' => [],
        ];
        continue;
    }
    //如果是直辖市
    if ($currentProvince['zhixia']) {
        $currentProvince['children'][] = [
            'name'     => $region[3],
            'code'     => $region[6],
            'children' => [],
        ];
        continue;
    }
    //如果第6栏是空的则是市区
    if ($region[5] == '') {
        if ($currentCity != null) {
            $currentProvince['children'][] = $currentCity;
        }
        $currentCity = [
            'name'     => $region[2],
            'code'     => $region[6],
            'children' => [],
        ];
        continue;
    }
    $currentCity['children'][] = [
        'name'     => $region[3],
        'code'     => $region[6],
        'children' => [],
    ];
}
if ($currentCity != null) {
    $currentProvince['children'][] = $currentCity;
}
if ($currentProvince != null) {
    $records[] = $currentProvince;
}

//添加进数据库
insertRecords(0, $records, $pdo);


/**
 * 插入记录
 * @param int   $parentId 父区域Id
 * @param array $records 记录集
 * @param PDO   $pdo pdo实例
 * @throws Exception
 */
function insertRecords($parentId, array $records, $pdo)
{
    foreach ($records as $record) {
        $message = "开始存储【%s】省数据 \n";
        echo sprintf($message, $record['name']);
        $sqlTemplate = "INSERT INTO region (parent_id,name,code)VALUES(%d,'%s',%s)";
        $sql = sprintf($sqlTemplate, $parentId, $record['name'], $record['code']);
        $affectRows = $pdo->exec($sql);
        if ($affectRows == 0) {
            throw new \Exception('插入数据失败：' . $sql);
        }
        if ($record['children']) {
            $lastInsertId = $pdo->lastInsertId();
            insertRecords($lastInsertId, $record['children'], $pdo);
        }
    }
}

/**
 * 获得PDO实例
 * @return PDO
 */
function getPdo()
{
    $host = '127.0.0.1';
    $db = 'test';
    $user = 'root';
    $password = 'root';
    try {
        $pdo = new PDO("mysql:host={$host};dbname={$db}", $user, $password);
    } catch (\Exception $e) {
        echo '无法连接数据库：' . $e->getMessage();
        exit;
    }
    return $pdo;
}

/**
 * 行政区域物理路径
 * @param $excelPath
 * @return \PhpOffice\PhpSpreadsheet\Worksheet\Worksheet
 */
function getExcelSheet($excelPath)
{
    try {
        $excel = IOFactory::load($excelPath);
        $sheet = $excel->getActiveSheet();
    } catch (\Exception $e) {
        echo '无法加载Excel文件：' . $e->getMessage();
        exit;
    }
    return $sheet;
}
```