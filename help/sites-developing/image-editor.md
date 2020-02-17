---
title: 影像編輯器
seo-title: 影像編輯器
description: 影像編輯器是AEM的核心部分，可由元件運用，以利內容作者控制影像。
seo-description: 影像編輯器是AEM的核心部分，可由元件運用，以利內容作者控制影像。
uuid: de6ac71b-380a-4b67-b697-ac34a79a9cc4
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: f6347492-cf48-4835-b8fd-ce9a75a09abe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 影像編輯器{#image-editor}

影像編輯器是AEM的核心部分，可由元件運用，以利內容作者控制影像。

>[!CAUTION]
>
>若要使用本文所述的影像編輯器功能， [必須安裝功能套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267) 24267。

## 影像地圖的相對單位 {#relative-units-for-image-map}

「影像編輯器」會將影像對映區域保留為絕對和相對單位。 當在響應式影像元件中作為用於動態地調整客戶端上的影像映射（相對於影像大小）的資料屬性提供相對單位時，該相對單位是有用的。

### imageMap屬性 {#imagemap-property}

影像地圖座標會由影像編輯器以屬 `imageMap` 性形式保留至JCR。 其格式如下。

屬性會儲存地圖區域，如下所示：

`[area1][area2][...]`

區域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

範例:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支援SVG影像 {#support-for-svg-images}

影像編輯器支援可縮放向量圖形(SVG)。

* 支援從DAM拖放SVG資產，以及從本機檔案系統上傳SVG檔案。

## 依MIME類型啟用外掛程式 {#enabling-plugins-by-mime-type}

在某些情況下，編寫動作必須針對特定MIME類型加以限制，因為伺服器端處理缺乏支援。 例如，可能不允許編輯SVG影像。

在個別外掛程式的設定節點上設定屬性，即可依MIME類型 `supportedMimeTypes` 選擇性啟用影像編輯器中的外掛程式。

### 例如 {#example}

例如，假設裁切功能僅適用於GIF、JPEG、PNG、WEBP和TIFF影像。

然 `supportedMimeTypes` 後，必須將屬性設定為映像元件節點上插件的配置節點上允許的 `cq:editConfig` MIME類型的字串。

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

