---
title: 內容片段 — 設定瀏覽器
description: 瞭解如何在設定瀏覽器中啟用某些內容片段功能，以使用Adobe Experience Manager強大的Headless傳送功能。
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 20%

---

# 內容片段 — 設定瀏覽器{#content-fragments-configuration-browser}

瞭解如何在設定瀏覽器中啟用某些內容片段功能，以使用Adobe Experience Manager (AEM)強大的Headless傳送功能。

## 為您的執行個體啟用內容片段功能 {#enable-content-fragment-functionality-instance}

在使用內容片段之前，請使用&#x200B;**設定瀏覽器**&#x200B;來啟用下列專案：

* **內容片段模型** — 必要
* **GraphQL持續查詢** — 選擇性

>[!CAUTION]
>
>如果未啟用&#x200B;**內容片段模型**：
>
>* **建立**&#x200B;選項將無法用於建立模型。
>* 您無法[選取Sites設定以建立相關的端點](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)。

若要啟用內容片段功能，您必須執行下列動作：

* 透過設定瀏覽器啟用內容片段功能
* 將設定套用至您的Assets資料夾

### 在設定瀏覽器中啟用內容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

若要[使用某些內容片段功能](#creating-a-content-fragment-model)，您&#x200B;**必須**&#x200B;先透過&#x200B;**設定瀏覽器**&#x200B;啟用它們：

>[!NOTE]
>
>如需詳細資訊，請參閱[設定瀏覽器： ](/help/sites-administering/configurations.md#using-configuration-browser)。

1. 導覽至「 **工具**」、「 **一般**」，然後開啟「 **設定瀏覽器**」。

1. 使用&#x200B;**建立**&#x200B;開啟對話方塊，您可以：

   1. 指定&#x200B;**標題**。
   1. 若要啟用其使用，請選取
      * **內容片段模型**
      * **GraphQL持續查詢**

      ![定義設定](assets/cfm-conf-01.png)

1. 選取&#x200B;**建立**&#x200B;以儲存定義。

<!-- 1. Select the location appropriate to your website. -->

### 套用設定到資產資料夾 {#apply-the-configuration-to-your-assets-folder}

當設定&#x200B;**global**&#x200B;啟用內容片段功能時，則套用至任何Assets資料夾。

若要搭配可比的Assets資料夾使用其他設定（即不包括全域），您必須定義連線。 若要這麼做，請在適當資 **料夾的「資料夾屬性** 」的「雲端服務 **」標籤** 中選取適當的「設定 **&#x200B;**&#x200B;」。

![套用組態](assets/cfm-conf-02.png)
