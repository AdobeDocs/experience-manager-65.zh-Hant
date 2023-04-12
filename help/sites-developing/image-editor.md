---
title: 影像編輯器
description: 影像編輯器是AEM的核心部分，可供元件使用，以方便內容作者操作影像。
uuid: de6ac71b-380a-4b67-b697-ac34a79a9cc4
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: f6347492-cf48-4835-b8fd-ce9a75a09abe
exl-id: af6cf1e0-8901-4621-9f72-e791cb8d68ae
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 8%

---

# 影像編輯器{#image-editor}

影像編輯器是AEM的核心部分，可供元件使用，以方便內容作者操作影像。

>[!CAUTION]
>
>若要使用本文所述影像編輯器的功能， [功能包24267](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267) 必須安裝。

## 影像映射的相對單位 {#relative-units-for-image-map}

影像編輯器會將影像映射區域以絕對單位和相對單位保存。 當提供相對單位作為資料屬性時，在響應式影像元件的客戶端上動態調整影像映射（相對於影像大小）的大小時，相對單位很有用。

### imageMap屬性 {#imagemap-property}

影像地圖座標會以 `imageMap` 屬性。 其格式如下。

屬性商店的地圖區域如下：

`[area1][area2][...]`

區域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

範例:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支援SVG影像 {#support-for-svg-images}

影像編輯器支援可縮放向量圖形(SVG)。

* 從DAM拖放SVG資產，以及從本機檔案系統上傳SVG檔案均受支援。

## 按MIME類型啟用插件 {#enabling-plugins-by-mime-type}

由於伺服器端處理缺乏支援，在某些情況下，某些MIME類型必須限制編寫動作。 例如，可能不允許編輯SVG影像。

影像編輯器中的外掛程式可透過設定 `supportedMimeTypes` 屬性。

### 範例 {#example}

例如，裁切功能僅適用於GIF、JPEG、PNG、WEBP和TIFF影像。

此 `supportedMimeTypes` 然後，屬性必須設定為外掛程式的設定節點上允許的MIME類型字串 `cq:editConfig` 影像元件的節點。

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
