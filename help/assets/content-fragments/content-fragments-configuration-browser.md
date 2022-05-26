---
title: 內容片段 — 配置瀏覽器
description: 瞭解如何在配置瀏覽器中啟用某些內容片段功能，以利用功AEM能強大的無頭傳送功能。
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
source-git-commit: 8dc8eff86ff25534a578dd227033aa185853d930
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 17%

---

# 內容片段 — 配置瀏覽器{#content-fragments-configuration-browser}

瞭解如何在配置瀏覽器中啟用某些內容片段功能，以利用功AEM能強大的無頭傳送功能。

## 為實例啟用內容片段功能 {#enable-content-fragment-functionality-instance}

在使用內容片段之前，您需要使用 **配置瀏覽器** 啟用：

* **內容片段模型**  — 強制
* **GraphQL持久查詢**  — 可選

>[!CAUTION]
>
>如果未啟用 **內容片段模型**:
>
>* 這樣 **建立** 的子菜單。
>* 你將無法 [選擇「站點」配置以建立相關端點](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)。


要啟用內容片段功能，您需要：

* 通過配置瀏覽器啟用內容片段功能
* 將配置應用到Assets資料夾

### 在配置瀏覽器中啟用內容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

至 [使用某些內容片段功能](#creating-a-content-fragment-model) 你 **必須** 首先通過 **配置瀏覽器**:

>[!NOTE]
>
>有關詳細資訊，請參閱 [配置瀏覽器：](/help/sites-administering/configurations.md#using-configuration-browser)。

>[!CAUTION]
>
>子配置（嵌套在配置中的配置）支援與內容片段一起使用，但不能用於GraphQL查詢。

1. 導覽至「 **工具**」、「 **一般**」，然後開啟「 **設定瀏覽器**」。

1. 使用 **建立** 開啟對話框，在其中：

   1. 指定 **標題**。
   1. 要啟用其使用，請選擇
      * **內容片段模型**
      * **GraphQL持久查詢**

      ![定義配置](assets/cfm-conf-01.png)


1. 選擇 **建立** 的子菜單。

<!-- 1. Select the location appropriate to your website. -->

### 將配置應用到您的資產資料夾 {#apply-the-configuration-to-your-assets-folder}

當配置 **全球** 為內容片段功能啟用，然後應用於任何「資產」資料夾。

若要搭配可比的「資產」檔案夾使用其他設定 (例如排除全域)，您必須定義連線。若要這麼做，請在適當資 **料夾的「資料夾屬性** 」的「雲端服務 **」標籤** 中選取適當的「設定 **** 」。

![應用配置](assets/cfm-conf-02.png)
