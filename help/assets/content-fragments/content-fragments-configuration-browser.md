---
title: 內容片段 — 設定瀏覽器
description: 瞭解如何在設定瀏覽器中啟用某些內容片段功能，以便利用AEM強大的Headless傳送功能。
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
source-git-commit: ad0f0bd8b0c230e002c734adca87da22bfa3a7cd
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 27%

---

# 內容片段 — 設定瀏覽器{#content-fragments-configuration-browser}

瞭解如何在設定瀏覽器中啟用某些內容片段功能，以便利用AEM強大的Headless傳送功能。

## 為您的執行個體啟用內容片段功能 {#enable-content-fragment-functionality-instance}

在使用內容片段之前，您需要使用 **設定瀏覽器** 若要啟用：

* **內容片段模型**  — 必要
* **GraphQL持續查詢**  — 選擇性

>[!CAUTION]
>
>如果您未啟用 **內容片段模型**：
>
>* 此 **建立** 選項將不可用於建立新模型。
>* 您將無法 [選取Sites設定以建立相關的端點](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint).


若要啟用內容片段功能，您需要：

* 透過設定瀏覽器啟用內容片段功能
* 將設定套用至您的資產資料夾

### 在設定瀏覽器中啟用內容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

至 [使用特定內容片段功能](#creating-a-content-fragment-model) 您 **必須** 首先透過 **設定瀏覽器**：

>[!NOTE]
>
>如需詳細資訊，另請參閱 [設定瀏覽器：](/help/sites-administering/configurations.md#using-configuration-browser).

1. 導覽至「 **工具**」、「 **一般**」，然後開啟「 **設定瀏覽器**」。

1. 使用 **建立** 若要開啟對話方塊，您可以：

   1. 指定 **標題**.
   1. 若要啟用其使用，請選取
      * **內容片段模型**
      * **GraphQL持續查詢**

      ![定義設定](assets/cfm-conf-01.png)


1. 選取 **建立** 以儲存定義。

<!-- 1. Select the location appropriate to your website. -->

### 套用設定到資產資料夾 {#apply-the-configuration-to-your-assets-folder}

設定時 **全域** 已啟用內容片段功能，然後套用至任何資產資料夾。

若要搭配可比的「資產」檔案夾使用其他設定 (例如排除全域)，您必須定義連線。若要這麼做，請在適當資 **料夾的「資料夾屬性** 」的「雲端服務 **」標籤** 中選取適當的「設定 **** 」。

![套用設定](assets/cfm-conf-02.png)
