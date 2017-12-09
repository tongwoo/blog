---
layout: post
title: 'Mac下的Photoshop CC系列版本另存为png、jpg文件过大的问题分析与解决'
date: 2015-12-27
author: wutong
tags:  mac photoshop
---

在使用 Mac 下的 Photoshop CC 版本对文件进行存储的时候，会发现文件体积比CS6之前的版本生成的文件大10倍以上，比如我另存为了一个“icon-progress.png”，执行顺序是：文件 – 存储为 – PNG，出来的文件有6M之多。

### 分析

既然文件过大，那肯定是ps对文件的真实内容进行了扩充，用代码编辑器打开了图片，发现了如下内容：

```xml
<x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 5.5-c021 79.155772, 2014/01/13-19:44:00        ">
   <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:Description rdf:about=""
            xmlns:photoshop="http://ns.adobe.com/photoshop/1.0/"
            xmlns:xmpMM="http://ns.adobe.com/xap/1.0/mm/"
            xmlns:stEvt="http://ns.adobe.com/xap/1.0/sType/ResourceEvent#"
            xmlns:stRef="http://ns.adobe.com/xap/1.0/sType/ResourceRef#"
            xmlns:xmp="http://ns.adobe.com/xap/1.0/"
            xmlns:dc="http://purl.org/dc/elements/1.1/"
            xmlns:tiff="http://ns.adobe.com/tiff/1.0/"
            xmlns:exif="http://ns.adobe.com/exif/1.0/">
         <photoshop:LegacyIPTCDigest>2E3857CCBA7891F73749CE549FF5A7BD</photoshop:LegacyIPTCDigest>
         <photoshop:ColorMode>3</photoshop:ColorMode>
         <photoshop:ICCProfile>sRGB IEC61966-2.1</photoshop:ICCProfile>
         <photoshop:DocumentAncestors>
            <rdf:Bag>
               <rdf:li>0</rdf:li>
               <rdf:li>000B0C073A7B9F448D4024568E1D2400</rdf:li>
               <rdf:li>00156DBEC3FBC67004F74B414AA78804</rdf:li>
               <rdf:li>001A2BEFBA3041BB03814D05EC879BCE</rdf:li>
               <rdf:li>001C5C4D9C1FC7A7216FA8737C25460B</rdf:li>
         ................
         <exif:PixelXDimension>32</exif:PixelXDimension>
         <exif:PixelYDimension>32</exif:PixelYDimension>
      </rdf:Description>
   </rdf:RDF>
</x:xmpmeta>
.......
```

足足10几万行，这个叫 metadata，翻译过来就是 “元数据”，adobe为什么加上这个东东？看xml的描述应该是记录了操作的过程和文件信息。

### 解决

既然他加了这个东西那有没有办法让他不加？我使用了如下方式进行解决:

 > 文件 – 存储为web格式 - 元数据(无) – 存储

![存储为web格式图片](/screenshot/2015-12-27/ps-saveas.png)
 