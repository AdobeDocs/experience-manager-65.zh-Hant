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
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 更改介面{#changing-the-color-scheme-of-the-interface}的顏色配置

您可以修改AEM Forms工作區使用者介面部分的色彩配置，以符合您的需求。 以下是一些代表性色彩配置自訂的範例。 除了本文討論的步驟之外，請參閱[AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md)。

## 頂端導覽列{#top-navigation-bar}

### 使用背景影像{#using-background-image}

更新AEM Forms工作區頂端的導覽列。

1. 建立背景影像以更新顏色。 將檔案命名為newBackground.jpg。
1. 使用WebDAV客戶端上載/apps/ws/images資料夾中的背景影像檔案。

   >[!NOTE]
   >
   >有關WebDAV訪問的詳細資訊，請參閱[https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

1. 在/apps/ws/css/newStyle.css中新增下列樣式，以參考新的背景影像。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### 在CSS {#using-color-property-in-css}中使用color屬性

1. 在newStyle.css中，在/apps/ws/css中新增下列樣式

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## 類別元件{#category-component}

類別元件會在左側面板中顯示您的工作的各種類別。 若要變更其顏色，請在CSS檔案的`.category`元素中定義背景顏色。

## 任務元件{#task-component}

任務顯示在名為TaskList Component的中間面板中。 要更改其顏色，請修改與樣式表中的.task選擇器關聯的樣式。
