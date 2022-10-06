---
title: 內容片段 — 設定瀏覽器
description: 了解如何在設定瀏覽器中啟用特定內容片段功能，以運用AEM強大的無頭傳送功能。
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
source-git-commit: 8dc8eff86ff25534a578dd227033aa185853d930
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 17%

---

# 內容片段 — 設定瀏覽器{#content-fragments-configuration-browser}

了解如何在設定瀏覽器中啟用特定內容片段功能，以運用AEM強大的無頭傳送功能。

## 為您的執行個體啟用內容片段功能 {#enable-content-fragment-functionality-instance}

使用內容片段之前，您需要使用 **配置瀏覽器** 啟用：

* **內容片段模型** 必填
* **GraphQL持久查詢**  — 可選

>[!CAUTION]
>
>如果您未啟用 **內容片段模型**:
>
>* the **建立** 建立新模型時將無法使用選項。
>* 你將無法 [選擇Sites配置以建立相關端點](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint).


若要啟用內容片段功能，您需要：

* 透過設定瀏覽器啟用內容片段功能的使用
* 將設定套用至資產資料夾

### 在設定瀏覽器中啟用內容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

結束日期 [使用特定內容片段功能](#creating-a-content-fragment-model) you **必須** 首先透過 **配置瀏覽器**:

>[!NOTE]
>
>如需詳細資訊，另請參閱 [配置瀏覽器：](/help/sites-administering/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>支援與內容片段搭配使用的子設定（在設定內巢狀的設定），但無法用於GraphQL查詢。

1. 導覽至「 **工具**」、「 **一般**」，然後開啟「 **設定瀏覽器**」。

1. 使用 **建立** 開啟對話框，其中：

   1. 指定 **標題**.
   1. 啟用其使用選擇
      * **內容片段模型**
      * **GraphQL持久查詢**

      ![定義配置](assets/cfm-conf-01.png)


1. 選擇 **建立** 以儲存定義。

<!-- 1. Select the location appropriate to your website. -->

### 將設定套用至資產資料夾 {#apply-the-configuration-to-your-assets-folder}

設定時 **全球** 已啟用內容片段功能，然後套用至任何「資產」資料夾。

若要搭配可比的「資產」檔案夾使用其他設定 (例如排除全域)，您必須定義連線。若要這麼做，請在適當資 **料夾的「資料夾屬性** 」的「雲端服務 **」標籤** 中選取適當的「設定 **** 」。

![套用設定](assets/cfm-conf-02.png)
