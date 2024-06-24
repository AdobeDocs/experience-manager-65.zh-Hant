---
title: 設定重新導向頁面
description: 填寫最適化表單後，使用者會被重新導向至表單作者可在建立表單時設定的網頁。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: be1a774f-5681-443f-b195-28e89a020547
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 21%

---

# 設定重新導向頁面{#configuring-redirect-page}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-redirect-page.html) |
| AEM 6.5 | 本文章 |

表單作者可為每個表單設定頁面，表單使用者在提交表單後會重新導向至該頁面。

1. 在編輯模式中，選取元件，然後按一下 ![欄位層級](assets/field-level.png) > **最適化表單容器**，然後按一下 ![cmppr](assets/cmppr.png).

1. 在側邊欄中，按一下 **提交**.

1. 在「提交」區段的「感謝您」頁面下提供重新導向頁面的URL。
1. 您可以選擇在提交動作底下，針對提交至REST端點動作，設定要傳遞至重新導向頁面的引數。

![重新導向頁面設定](assets/thank-you-setting-1.png)

重新導向頁面設定

表單作者可使用以下傳遞至「感謝您」頁面的引數。 對於所有可用的提交動作， `status` 和 `owner` 引數會傳遞。 除了這兩個引數以外，系統還會為下列提交動作傳遞一些其他引數：

* **存放區內容動作** （已棄用） ： `contentPath` — 儲存提交資料的存放庫中的節點路徑 — 會傳遞。

* **儲存PDF動作** （已棄用） ： `contentPath` — 已提交的資料，以及儲儲存儲存存庫中PDF檔案之節點的路徑 — 會被傳遞。

* **提交至Forms工作流程**：會傳遞從表單工作流程傳回的輸出引數。

* **提交至REST端點**：傳遞為欄位內與引數對應新增的引數。 `status` 和 `owner` 此提交動作中未傳遞引數。 如需詳細資訊，請參閱 [設定提交至REST端點提交動作](../../forms/using/configuring-submit-actions.md).
