---
title: 更改介面的顏色方案
seo-title: Changing the color scheme of the interface
description: 如何有選擇地修改AEM Forms工作區用戶介面部分的顏色方案。
seo-description: How to modify the color scheme of AEM Forms workspace user interface portions selectively.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# 更改介面的顏色方案 {#changing-the-color-scheme-of-the-interface}

可以修改AEM Forms工作區用戶介面部分的顏色方案以滿足您的要求。 下面是一些代表性顏色方案自定義的示例。 除本文中討論的步驟外，請參見 [AEM Forms工作區定製的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md)。

## 頂部導航欄 {#top-navigation-bar}

### 使用背景影像 {#using-background-image}

更新位於AEM Forms工作區頂部的導航欄。

1. 建立背景影像以更新顏色。 將檔案命名為newBackground.jpg。
1. 使用WebDAV客戶端在/apps/ws/images資料夾中上載背景影像檔案。

   >[!NOTE]
   >
   >有關WebDAV訪問的詳細資訊，請參見 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant)。

1. 通過添加以下樣式，在/apps/ws/css/newStyle.css中引用新的背景影像。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### 在CSS中使用color屬性 {#using-color-property-in-css}

1. 在/apps/ws/css的newStyle.css中添加以下樣式

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## 類別元件 {#category-component}

類別元件在左側面板中顯示任務的各種類別。 要更改其顏色，請在 `.category` CSS檔案的元素。

## 任務元件 {#task-component}

任務顯示在名為TaskList元件的中間面板中。 要更改其顏色，請修改與樣式表中的.task選擇器關聯的樣式。
