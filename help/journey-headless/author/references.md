---
title: 了解如何在內容片段中使用參考
description: 了解如何在內容片段、內容、其他片段和其他資產（媒體）中使用參考。 介紹無頭式CMS製作的巢狀片段的必要性和機制。
index: true
hide: false
hidefromtoc: false
source-git-commit: 9661061a98c31fbb74bd0716dbedc7abef298f44
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 2%

---

# 了解如何在內容片段中使用參考 {#author-headless-references}

## 迄今為止的故事 {#story-so-far}

在 [AEM無頭內容製作歷程](overview.md) the [簡介](introduction.md) 涵蓋與無頭製作相關的基本概念和術語。

您已了解無頭式CMS製作的基本知識，並熟悉如何使用AEMaaCS製作，尤其是製作內容片段。

本文以這些為基礎，讓您了解如何使用參考來為您的AEM無頭專案製作您自己的內容。

## 目標 {#objective}

* **對象**:進階
* **目標**:介紹無頭式CMS製作的參考使用方式。 可用的參考類型及其用途：

   * 內容參考資料
   * 資產/媒體參考
   * 片段參考
   * 從文字區塊內的臨機參考

## 參考內容 {#what-are-references}

參考只是連接資源的機制，無論是其他內容、資產（如影像中）或其他片段皆然。 雖然非常相似，但還是有一些差異。

有些參考有專用的資料類型（例如內容參考和片段參考），有些則只是新增為文字區塊內的參考（資產參考和臨機參考）。

![內容片段 — 參考](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## 內容參考資料 {#content-references}

內容參考就是這麼做的 — 可讓您參考任何其他內容。 這會開啟一個瀏覽器，讓您選取內容項目。

## 資產/媒體參考 {#assets-media-references}

可在文字區塊中參考資產（例如影像或媒體），方法是使用 **插入資產** 選項。 這會開啟一個瀏覽器，供您選取資產。

![內容片段 — 插入資產](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## 片段參考 {#fragment-references}

「片段參考」同樣會這麼做 — 可讓您參考其他片段。 這個重要性的原因需要多一點解釋。

例如，您可能已定義下列內容片段模型：

* 城市
* 公司
* 人員
* 獎勵

看起來很簡單，但公司當然有CEO和員工…….這些都是人，每個人都被定義為人。

一個人可以獲得一個獎（或者兩個）。

* 我的公司 — 公司
   * CEO — 人員
   * 員工 — 人員
      * 個人獎 — 獎

這只是先來的。 根據複雜性，獎項可能是特定於公司，或者公司可以在特定城市中設定其主要辦事處。

如您（作者）和無頭式應用程式所了解，透過片段參考可呈現這些相互關係。

身為作者，您不負責定義這些關係（建立內容片段模型時由內容架構師完成），但您必須知道如何辨識和編輯參照。

### 如何製作巢狀片段 {#author-nested-fragment}

製作片段參考相當簡單(不過通常欄位不會標示為 **片段參考**)。 您可以直接輸入參考，或（更可能）選取資料夾圖示以開啟瀏覽器，供您導覽並選取所需片段。

![內容片段 — 參考](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

內容片段模型控制項的定義：

* 是否可選擇添加多個引用
* 您可選取的內容片段模型類型；「內容片段模型」會定義參考所允許的片段模型，因此AEM只會根據這些模型顯示片段。

### 如何導覽巢狀片段 {#navigate-nested-fragment}

使用 **結構樹** 內容片段編輯器的索引標籤，您可以導覽至片段所參考的片段，然後導覽其可能包含的任何參考。 選取參考會開啟該片段以供編輯。

>[!NOTE]
>
>使用主面板中的階層連結，您可以導覽回起始點。

![內容片段結構樹](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## 臨機參考 {#adhoc-references}

臨機參考可新增為文字區塊內的簡單連結：

![內容片段 — 臨機參考](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## 下一步 {#whats-next}

現在您已了解內容片段中的參考和結構，下一步是 [了解中繼資料和標籤的相關資訊](metadata-tagging.md). 這將介紹並討論如何定義內容片段的中繼資料和標籤。

## 其他資源 {#additional-resources}

* [使用內容片段](/help/assets/content-fragments/content-fragments.md)

   * [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)

      * [將設定套用至資產資料夾](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [建立內容片段](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [變化 — 編寫內容片段](/help/assets/content-fragments/content-fragments-variations.md)

   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [內容片段模型 — 資料類型](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [內容片段模型 — 屬性](/help/assets/content-fragments/content-fragments-models.md#properties)


* 快速入門手冊
   * [建立資產資料夾無頭快速入門手冊](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [AEM無頭式內容架構者歷程](/help/journey-headless/architect/overview.md)

* [AEM無頭翻譯歷程](/help/journey-headless/translation/overview.md)
