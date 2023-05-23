---
title: 配置重定向頁
seo-title: Configuring redirect page
description: 在填寫自適應表單後，可以將用戶重定向到表單作者在建立表單時可以配置的網頁。
seo-description: After filling an adaptive form, users can be redirected to a webpage that form authors can configure while creating the form.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
feature: Adaptive Forms
exl-id: be1a774f-5681-443f-b195-28e89a020547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 配置重定向頁{#configuring-redirect-page}

表單作者可以為每個表單配置一個頁面，在提交表單後，表單用戶將重定向到該頁面。

1. 在編輯模式下，選擇一個元件，然後按一下 ![欄位級](assets/field-level.png) > **自適應窗體容器**，然後按一下 ![招商](assets/cmppr.png)。

1. 在提要欄中，按一下 **提交**。

1. 在「提交」部分的「感謝頁」下提供重定向頁的URL。
1. （可選）在「提交操作」下，對於「提交至REST」終結點操作，可以配置要傳遞到重定向頁的參數。

![重定向頁面配置](assets/thank-you-setting-1.png)

重定向頁面配置

表單作者可以使用傳遞到「感謝」頁的以下參數。 對於所有可用的提交操作， `status` 和 `owner` 傳遞參數。 除了這兩個參數外，還為以下提交操作傳遞了一些附加參數：

* **儲存內容操作** （不建議使用）: `contentPath` — 傳遞已提交資料所儲存的儲存庫中節點的路徑。

* **儲存PDF操作** （不建議使用）: `contentPath` — 傳遞已提交的資料和到儲存在儲存庫中的PDF檔案的節點的路徑。

* **提交到Forms工作流**:傳遞從表單工作流返回的輸出參數。

* **提交到REST終結點**:將傳遞為欄位內映射添加的參數。 `status` 和 `owner` 此提交操作中未傳遞參數。 有關詳細資訊，請參見 [配置「提交至REST端點」提交操作](../../forms/using/configuring-submit-actions.md)。
