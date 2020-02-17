---
title: 更改介面的顏色配置
seo-title: 更改介面的顏色配置
description: 如何選擇性修改AEM Forms工作區使用者介面部分的色彩配置。
seo-description: 如何選擇性修改AEM Forms工作區使用者介面部分的色彩配置。
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 更改介面的顏色配置 {#changing-the-color-scheme-of-the-interface}

您可以修改AEM Forms工作區使用者介面部分的色彩配置，以符合您的需求。 以下是代表性色彩配置自訂的一些範例。 除了本文章討論的步驟外，請參閱「AEM Forms工 [作區自訂的一般步驟」](/help/forms/using/generic-steps-html-workspace-customization.md)。

## 頂端導覽列 {#top-navigation-bar}

### 使用背景影像 {#using-background-image}

若要更新AEM Forms工作區頂端的導覽列。

1. 建立背景影像以更新顏色。 將檔案命名為newBackground.jpg。
1. 使用WebDAV用戶端上傳/apps/ws/images檔案夾中的背景影像檔案。

   >[!NOTE]
   >
   >如需WebDAV存取的詳細資訊，請參閱 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

1. 在/apps/ws/css/newStyle.css中新增下列樣式，以參考新的背景影像。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### 在CSS中使用顏色屬性 {#using-color-property-in-css}

1. 在newStyle.css中新增下列樣式，網址為/apps/ws/css

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## 類別元件 {#category-component}

類別元件會在左側面板中顯示您的工作的各種類別。 若要變更其顏色，請在CSS檔案的元 `.category` 素中定義背景顏色。

## 任務元件 {#task-component}

任務顯示在名為TaskList元件的中間面板中。 要更改其顏色，請修改樣式表中與。task選擇器關聯的樣式。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
