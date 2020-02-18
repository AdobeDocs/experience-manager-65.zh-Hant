---
title: 設定重新導向頁面
seo-title: 設定重新導向頁面
description: 在填寫最適化表格後，可將使用者重新導向至表單作者在建立表格時可設定的網頁。
seo-description: 在填寫最適化表格後，可將使用者重新導向至表單作者在建立表格時可設定的網頁。
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# 設定重新導向頁面{#configuring-redirect-page}

表單作者可以為每個表單設定一個頁面，表單使用者在送出表單後會重新導向至該頁面。

1. 在編輯模式中，選取元件，然後按一下欄 ![位層級](assets/field-level.png) > **最適化表單容器**，然後按 ![一下cmppr](assets/cmppr.png)。

1. 在側欄中，按一下「 **提交」**。

1. 在「提交」區段的「感謝頁面」下方，提供重新導向頁面的URL。
1. （可選）在「提交操作」下，對於「提交到REST端點」操作，您可以配置要傳遞到重定向頁的參數。

![重新導向頁面設定](assets/thank-you-setting-1.png)

重新導向頁面設定

表單作者可以使用下列參數，這些參數會傳遞至「感謝」頁面。 對於所有可用的提交動作， `status` 會傳 `owner` 遞參數。 除了這兩個參數外，還會為下列提交動作傳遞一些額外參數：

* **儲存內容動作** （已過時）: `contentPath`-將傳遞已提交資料儲存在儲存庫中的節點路徑。

* **儲存PDF動作** （已過時）:將 `contentPath`傳遞已提交的資料和儲存在儲存庫中的PDF檔案節點的路徑。

* **提交至表單工作流程**:會傳遞從表單工作流程傳回的輸出參數。

* **提交到REST端點**:系統會傳遞為在欄位內映射至參數所新增的參數。 `status` 而參 `owner` 數不會在此提交動作中傳遞。 有關詳細資訊，請 [參閱配置提交到REST端點提交操作](../../forms/using/configuring-submit-actions.md)。

