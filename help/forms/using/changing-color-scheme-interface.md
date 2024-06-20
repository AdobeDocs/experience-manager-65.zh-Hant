---
title: 變更介面的色彩配置
description: 如何選擇性地修改AEM Forms工作區使用者介面部分的色彩配置。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 變更介面的色彩配置 {#changing-the-color-scheme-of-the-interface}

您可以修改AEM Forms工作區使用者介面部分的色彩配置以符合您的需求。 以下是一些代表性色彩配置自訂的範例。 除了本文章中討論的步驟之外，請參閱 [AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md).

## 頂端導覽列 {#top-navigation-bar}

### 使用背景影像 {#using-background-image}

更新AEM Forms工作區頂端的導覽列。

1. 建立背景影像以更新顏色。 將檔案命名為newBackground.jpg。
1. 使用WebDAV使用者端上傳/apps/ws/images資料夾中的背景影像檔案。

   >[!NOTE]
   >
   >如需詳細資訊，請參閱 [WebDAV存取](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=en).

1. 新增下列樣式，以參照/apps/ws/css/newStyle.css中的新背景影像。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### 在CSS中使用color屬性 {#using-color-property-in-css}

1. 在/apps/ws/css的newStyle.css中新增以下樣式

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## 類別元件 {#category-component}

類別元件會在左側面板中顯示您工作的各種類別。 若要變更其顏色，請在下列位置定義背景顏色： `.category` CSS檔案的元素。

## 任務元件 {#task-component}

工作會顯示在稱為TaskList元件的中間面板中。 若要變更其顏色，請修改樣式表中與.task選取器關聯的樣式。
