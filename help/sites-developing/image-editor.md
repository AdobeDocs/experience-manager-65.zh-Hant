---
title: 影像編輯器
description: 影像編輯器是其核心部AEM分，可供元件使用，以便於內容作者對影像的操作。
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

影像編輯器是其核心部AEM分，可供元件使用，以便於內容作者對影像的操作。

>[!CAUTION]
>
>要使用本文中描述的影像編輯器的功能， [功能包24267](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267) 必須安裝。

## 影像映射的相對單位 {#relative-units-for-image-map}

影像編輯器將影像映射區域保留為絕對和相對單位。 當提供相對單元作為資料屬性用於在響應影像元件中動態調整客戶端上的影像映射（相對於影像大小）的大小時，相對單元是有用的。

### imageMap屬性 {#imagemap-property}

將影像映射坐標保持為JCR `imageMap` 屬性。 它具有以下格式。

該屬性按如下方式儲存地圖區域：

`[area1][area2][...]`

區域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

範例:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支援SVG映像 {#support-for-svg-images}

影像編輯器支援可縮放向量圖形(SVG)。

* 支援從DAM拖放SVG資產和從本地檔案系統上載SVG檔案。

## 按MIME類型啟用插件 {#enabling-plugins-by-mime-type}

在某些情況下，由於在伺服器端處理中缺乏支援，某些MIME類型的創作操作必須受到限制。 例如，可能不允許編輯SVG影像。

通過設定MIME類型，可以有選擇地啟用影像編輯器中的插件 `supportedMimeTypes` 單個插件的配置節點上的屬性。

### 範例 {#example}

例如，我們假設只應允許GIF、JPEG、PNG、WEBP和TIFF影像具有裁剪能力。

的 `supportedMimeTypes` 然後，必須將屬性設定為插件配置節點上允許的MIME類型的字串 `cq:editConfig` 影像元件的節點。

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
