---
title: 了解內容模型的基本知識
description: 了解使用內容片段進行 Headless CMS 內容模型的基本知識。
exl-id: a53fef09-6495-4bb7-8df1-ba3c113d88f6
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 94%

---

# 了解 AEM Headless 內容模型基本知識 {#content-modeling-headless-basics}

## 目前進度 {#story-so-far}

在[AEM Headless 內容架構師歷程](overview.md)一開始，[簡介](introduction.md)部分介紹了和建立 Headless 內容模型相關的基本概念和術語。

本文以這些基本知識為基礎，以便您了解如何為您的 AEM Headless 專案建立內容模型。

## 目標 {#objective}

* **客群**：初學者
* **目標**：介紹 Headless CMS 內容模型的概念。

## 使用內容片段模型建立內容模型 {#architect-content-fragment-models}

內容 (資料) 模型是一套既有的技術，通常在開發關聯式資料庫時使用，那麼內容模型對 AEM Headless 代表什麼？

### 原因為何？ {#why}

為確保您的應用程式能夠始終一致、有效率地從 AEM 要求和接收所需內容，這些內容必須結構化。

這表示您的應用程式預先知道回應採用的格式，因此知道如何處理回應。這比接收自由格式的內容要容易得多，自由格式的內容必須剖析以確定它包含什麼以及如何使用它。

### 運作方式簡介 {#how}

AEM 使用內容片段來提供將內容 Headless 傳遞到應用程式所需的結構。

您的內容模型結構：

* 是由您的內容片段模型的定義實現，
* 做為內容片段的基礎，內容片段用於產生內容。

>[!NOTE]
>
>內容片段模型也做為 AEM GraphQL 結構描述的基礎，用於擷取您的內容 - 在開發人員歷旅中有更多相關資訊。

對內容的要求是使用 AEM GraphQL API 發出的，這是標準 GraphQL API 的自訂實作。AEM GraphQL API 允許應用程式對您的內容片段執行 (複雜) 查詢，每個查詢都根據特定的模型類型。

然後，您的應用程式可以使用傳回的內容。

## 使用內容片段模型建立架構 {#create-structure-content-fragment-models}

內容片段模型提供多種機制，可讓您定義內容的結構。

內容片段模型描述一個實體。

>[!NOTE]
>必須在設定瀏覽器中啟用內容片段功能，以便您可以建立新模型。

>[!TIP]
>
>應該命名模型，以便內容作者在建立內容片段時知道要選取哪個模型。

在模型中：

1. **資料型別**&#x200B;可讓您定義個別屬性。
例如，將包含教師姓名的欄位定義為&#x200B;**文字** 並將他們的服務年限定義為&#x200B;**數字**。
1. 資料型別&#x200B;**內容參考**&#x200B;和&#x200B;**片段參考**&#x200B;可讓您建立與AEM中其他內容的關聯。
1. **片段參考**&#x200B;資料類型可讓您將內容片段巢狀化 (根據模型類型)，以實現多層結構。這對建立內容模型很重要。

例如：

![使用內容片段建立內容模型](assets/headless-modeling-01.png "使用內容片段建立內容模型")

## 資料類型 {#data-types}

AEM 提供以下資料類型用於建立內容模型：

* 單行文字
* 多行文字
* 數字
* 布林值
* 日期和時間
* 列舉
* 標記
* 內容參考
* 片段參考
* JSON 物件

>[!NOTE]
>
>更多詳細資訊位於「內容片段模型 - 資料類型」。

## 參考和巢狀內容 {#references-nested-content}

兩種資料類型允許您參考特定片段之外的內容：

* **內容參考**
這提供對任何類型之其他內容的簡單參考。
例如，您可以參考在指定之位置的影像。

* **片段參考**
這提供對其他內容片段的參考。
此類型的參考用於建立巢狀內容，引入建立內容模型時所需的關係。
可以設定此資料類型以允許片段作者：
   * 直接編輯參考的片段。
   * 根據適當的模型建立內容片段

>[!NOTE]
>
>您也可以使用文字區塊內的連結建立臨時參考。

## 結構階層 (巢狀片段) {#levels-of-structure-nested-fragments}

對於建立內容模型，**片段參考**&#x200B;資料類型可讓您建立多層結構和關係。

使用此參考，您可以&#x200B;*連接*&#x200B;各種內容片段模型來表示相互關係。這可讓 Headless 應用程式依照連接操作，並視需要存取內容。

>[!NOTE]
>
>這應該小心使用，最佳做法可以定義為&#x200B;*視需要進行巢狀，但層數盡可能少*。

片段參考可讓您參考其他片段。

例如，您可能定義了以下內容片段模型：

* 城市
* 公司
* 人員
* 獎項

看起來很簡單，但一家公司既有執行長也有員工...這些都是人，每一個都被定義為人員。

人員可以獲得一個獎項 (或兩個)。

* 我的公司 - 公司
   * CEO - 人員
   * 員工 - 人員
      * 人員獎項 - 獎項

這只是供初學者了解。根據複雜程度，獎項可以是特定於公司的，或者公司可以在特定城市設有主要辦公室。

可以使用片段參考來表示這些相互關係，因為您 (架構師)、您的內容作者和 Headless 應用程式都可理解。

## 下一步 {#whats-next}

現在您已經了解了基本知識，下一步是[了解如何在 AEM 建立內容片段模型](model-structure.md)。這將介紹和討論各種可用的參考，以及如何使用片段參考建立結構階層，這是建立 Headless 模型的關鍵部分。

## 其他資源 {#additional-resources}

* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)

   * [內容片段模型 - 資料類型](/help/assets/content-fragments/content-fragments-models.md#data-types)

* [製作概念](/help/sites-authoring/author.md)

* [基本處理](/help/sites-authoring/basic-handling.md) - 此頁面主要根據 **Sites** 主控台，但許多/大部分功能也和製作 **Assets** 主控台下的&#x200B;**內容片段**&#x200B;相關。

* [使用內容片段](/help/assets/content-fragments/content-fragments.md)
