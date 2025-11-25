---
title: 了解如何在 AEM 中建立內容片段模型
description: 了解使用內容片段模型建立 Headless CMS 內容模型的概念和機制。
exl-id: b377e01f-e392-4ef5-a259-73ce9ff941d0
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 92%

---

# 了解如何在 AEM 中建立內容片段模型 {#architect-headless-content-fragment-models}

## 目前進度 {#story-so-far}

在[AEM Headless 內容作者歷程](overview.md)的一開始，[AEM Headless 內容模型基本知識](basics.md)介紹了和 Headless 內容製作相關的基本概念和術語。

本文以這些內容為基礎，以便您了解如何為 AEM Headless 專案建立您自己的內容片段模型。

## 目標 {#objective}

* **客群**：初學者
* **目標**：使用內容片段模型為您的 Headless CMS 建立內容模型的概念和機制。

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools > General > Configuration Browser. You can either select to configure the global entry, or create a configuration. For example:

![Define configuration](/help/assets/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## 建立內容片段模型 {#creating-content-fragment-models}

然後可以建立內容片段模型並定義結構。您可以在「工具> Assets >內容片段模型」底下執行此操作。

![工具中的內容片段模型](assets/cfm-tools.png)

選取此選項後，導覽到模型的位置並選取&#x200B;**建立**。您可以在此處輸入各種關鍵詳細資料。

依預設，**啟用模型**&#x200B;會啟動。這表示模型儲存後立即可供使用 (用於建立內容片段)。如果需要可以停用 - 之後有機會可啟用 (或停用) 現有模型。

![建立內容片段模型](/help/assets/content-fragments/assets/cfm-models-02.png)

使用&#x200B;**建立**&#x200B;進行確認，然後您可以&#x200B;**開啟**&#x200B;模型以開始定義結構。

## 定義內容片段模型 {#defining-content-fragment-models}

當您首次開啟新模型時，您會看到 - 左側有一大片空白，右側有一長串&#x200B;**資料類型**：

![空白模型](/help/assets/content-fragments/assets/cfm-models-03.png)

那麼 -該怎麼做？

您可以將&#x200B;**資料類型**&#x200B;的執行個體拖曳到左側空間 - 您已經定義了模型！

![定義欄位](/help/assets/content-fragments/assets/cfm-models-04.png)

新增資料類型後，您需要為該欄位定義&#x200B;**屬性**。這些取決於所使用的類型。例如：

![資料屬性](/help/assets/content-fragments/assets/cfm-models-05.png)

您可以隨您所需新增多個欄位。例如：

![內容片段模型](/help/assets/content-fragments/assets/cfm-models-07.png)

### 您的內容作者 {#your-content-authors}

您的內容作者看不到您用於建立模型的實際資料類型和屬性。這表示您可能必須提供相關協助和資訊讓他們完成特定欄位。對於基本資訊，您可以使用欄位標籤和預設值，但可能需要考慮更複雜案例的專案特定文件。

>[!NOTE]
>
>請參閱其他資源 - 內容片段模型。

## 管理內容片段模型 {#managing-content-fragment-models}

<!-- needs more details -->

管理您的內容片段模型涉及：

* 啟用 (或停用) 它們 - 這使作者在建立內容片段時可以使用。
* 刪除 - 總是需要刪除，但您需要注意刪除已用於內容片段的模型，特別是已發佈的片段。

## 發佈 {#publishing}

<!-- needs more details -->

內容片段模型需要在任何相關內容片段發佈時/之前發佈。

>[!NOTE]
>
>如果作者嘗試發佈模型尚未發佈的內容片段，選取清單將指出此情況，並且模型將與片段一起發佈。

一旦模型發佈，就會被&#x200B;*鎖定*&#x200B;成作者的唯讀模式。這旨在防止可能導致現有 GraphQL 結構和查詢錯誤的變更，尤其是在發佈環境。它在主控台中顯示為&#x200B;**鎖定**。

當模型為&#x200B;**鎖定** (唯讀模式) 時，可以看到模型的內容和結構，但不能直接編輯；儘管您可以從主控台或模型編輯器管理&#x200B;**鎖定**&#x200B;模型。

## 後續步驟 {#whats-next}

現在您已經了解了基本知識，下一步是開始建立您自己的內容片段模型。

## 其他資源 {#additional-resources}

* [製作概念](/help/sites-authoring/author.md)

* [基本處理](/help/sites-authoring/basic-handling.md) — 此頁面主要以&#x200B;**網站**&#x200B;主控台為基礎，但許多/大部分的功能也可用來導覽至&#x200B;**Assets**&#x200B;主控台下的&#x200B;**內容片段模型**&#x200B;並對其執行動作。

* [使用內容片段](/help/assets/content-fragments/content-fragments.md)

   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [定義內容片段模型](/help/assets/content-fragments/content-fragments-models.md#defining-your-content-fragment-model)

      * [啟用或停用內容片段模型](/help/assets/content-fragments/content-fragments-models.md#enabling-disabling-a-content-fragment-model)

      * [允許資產資料夾中的內容片段模型](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

      * [刪除內容片段模型](/help/assets/content-fragments/content-fragments-models.md#deleting-a-content-fragment-model)

      * [發佈內容片段模型](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)

      * [取消發佈內容片段模型](/help/assets/content-fragments/content-fragments-models.md#unpublishing-a-content-fragment-model)

      * [鎖定的 (已發佈的) 內容片段模型](/help/assets/content-fragments/content-fragments-models.md#locked-published-content-fragment-models)

* 快速入門指南

   * [建立內容片段模型Headless快速入門手冊](/help/sites-developing/headless/getting-started/create-content-model.md)
