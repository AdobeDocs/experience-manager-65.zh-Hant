---
title: 影像編輯器
description: 影像編輯器是AEM的一項核心功能，元件可使用它來協助內容作者操控影像。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: af6cf1e0-8901-4621-9f72-e791cb8d68ae
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 2%

---

# 影像編輯器{#image-editor}

影像編輯器是AEM的一項核心功能，元件可使用它來協助內容作者操控影像。

>[!CAUTION]
>
>若要使用本文所述之影像編輯器的功能，必須安裝[功能套件24267](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267)。

## 影像地圖的相對單位 {#relative-units-for-image-map}

「影像編輯器」會以絕對和相對單位保留影像地圖區域。 在回應式影像元件的使用者端上，當提供相對單位作為資料屬性以動態調整影像地圖（相對於影像大小）的大小時，這些單位就相當實用。

### imageMap屬性 {#imagemap-property}

影像編輯器會將影像地圖座標以`imageMap`屬性的形式保留至JCR。 其格式如下。

屬性會依下列方式儲存地圖區域：

`[area1][area2][...]`

區域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

範例：

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支援SVG影像 {#support-for-svg-images}

影像編輯器支援可縮放向量圖形(SVG)。

* 支援從DAM拖放SVG資產以及從本機檔案系統上傳SVG檔案。

## 依MIME型別啟用外掛程式 {#enabling-plugins-by-mime-type}

在某些情況下，由於伺服器端處理缺乏支援，因此必須限制特定MIME型別的編寫動作。 例如，可能不允許編輯SVG影像。

在個別外掛程式的設定節點上設定`supportedMimeTypes`屬性，MIME型別即可選擇性地啟用影像編輯器中的外掛程式。

### 範例 {#example}

舉例來說，我們假設只有GIF、JPEG、PNG、WEBP和TIFF影像才允許裁切功能。

然後，必須在影像元件的`cq:editConfig`節點上的外掛程式的設定節點上，將`supportedMimeTypes`屬性設定為允許的MIME型別字串。

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
