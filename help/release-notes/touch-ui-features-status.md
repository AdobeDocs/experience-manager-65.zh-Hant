---
title: Touch UI功能狀態
description: ' [!DNL Adobe Experience Manager] Touch-Enabled UI的發行說明。'
translation-type: tm+mt
source-git-commit: d938f52766154b68df2f6db2c8c49a0ad97e7e6d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 14%

---


# 觸控式UI功能狀態{#touch-ui-feature-status}

AEM 6.4以上版本[已過時](../release-notes/deprecated-removed-features.md)的Classic UI。 Adobe不會進一步增強Classic UI，並鼓勵使用者運用觸控式UI中的強大新功能。

從6.0版開始，AEM推出新的使用者介面，稱為「觸控式UI」（簡稱「觸控式UI」），其與[!DNL Adobe Experience Cloud]和整體Adobe使用者介面方針一致。 幾乎達到功能對等，這已成為AEM中的標準UI，其舊版案頭導向介面稱為「傳統UI」。

雖然大部份的功能都存在於觸控式使用者介面中，但有些功能尚未完整，將會在未來版本中新增。

下列清單顯示AEM 6.5中實作之功能的目前狀態。

如需升級至AEM 6.5的客戶建議，請參閱[客戶的使用者介面建議](/help/sites-deploying/ui-recommendations.md)。

>[!NOTE]
>
>本頁僅涵蓋與傳統UI的功能奇偶校驗。 未列出新增至Touch-enabled UI且不存在於Classic UI中的功能，以及它的獨特功能。

>[!NOTE]
>
>這份清單力求完整，但並非完整。

## 圖例 {#legend}

* **完整**:此功能可在觸控式UI中完整使用。
* **主要**:此功能大部分可在觸控式UI中使用。
* **遺漏**:此功能不在觸控式使用者介面中，必須使用傳統使用者介面才能執行此動作。
* **已取代**:此功能已取代為運作不同的新實作。
* **已移除**:此功能不再存在於觸控式UI中，也不會被取代。

## 功能狀態：網站管理員{#feature-status-sites-admin}

這是傳統UI網站管理員(`/siteadmin`)擁有的功能清單，以及觸控式UI(`/sites.html`)的狀態。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 導覽網站階層 | 完成 | AEM 6.4推出[內容樹狀檢視](/help/sites-authoring/basic-handling.md#content-tree)。 |
| 啟動工作流程 | 完成 |  |
| 建立新頁面 | 完成 |  |
| 建立新網站 | 完成 |  |
| 建立新的啟動 | 完成 |  |
| 建立新的即時副本 | 完成 |  |
| 建立資料夾 | 完成 |  |
| 顯示出版物狀態 | 完成 | 從AEM 6.5開始，工作流程狀態會顯示在清單檢視中。 |
| 搜尋 | 完成 |  |
| 複製和貼上頁面（複製） | 完成 |  |
| 移動頁面 | 完成 |  |
| 發佈頁面 | 完成 |  |
| 無複製權限的發佈頁面 | 完成 |  |
| 稍後發佈 | 完成 |  |
| 發佈樹狀結構 | 完成 |  |
| 取消發佈頁面 | 完成 |  |
| 取消發佈頁面，但無複製權限 | 完成 |  |
| 稍後取消發佈 | 完成 |  |
| 刪除 | 完成 |  |
| 鎖定／解鎖 | 完成 |  |
| 檢視／編輯屬性 | 完成 |  |
| 設定頁面上的權限 | 完成 |  |
| 版本記錄 | 完成 |  |
| 還原版本 | 完成 |  |
| 恢復樹狀結構和恢復已刪除的頁 | 遺失 | 使用Classic UI。 |
| 顯示舊版與目前版本的差異 | 完成 |  |
| 即時複製動作（推出） | 完成 |  |
| 查看語言副本 | 完成 |  |
| 尋找和取代 | 遺失 | 使用Classic UI。 |
| 通知收件匣（JCR事件） | 遺失 | 使用Classic UI。 將會以不同的實作取代。 |
| 引用 | 完成 | 顯示新增至AEM 6.5的傳入頁面連結。 |

## 功能狀態：頁面編輯器{#feature-status-page-editor}

這是傳統UI頁面編輯器(`/cf#`)擁有的功能清單，以及觸控式編輯器(`/editor.html`)的狀態。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 編輯網頁 | 完成 |  |
| 編輯行動網頁 | 完成 |  |
| 編輯透過Design Importer匯入的內容 | 完成 |  |
| 編輯電子郵件 | 完成 |  |
| 編輯混合行動應用程式 | 完成 |  |
| 編輯表單 | 完成 |  |
| 編輯選件 | 完成 |  |
| 編輯工作流程模型 | 完成 |  |
| 模式：編輯和預覽 | 完成 |  |
| 互動式預覽 | 完成 |  |
| 模式：編輯設計 | 完成 |  |
| 模式：腳手架 | 完成 |  |
| 模式：即時副本狀態 | 完成 |  |
| 新增註解 | 完成 |  |
| 編輯屬性 | 完成 |  |
| 推廣頁面 | 完成 |  |
| 開始和顯示工作流程 | 完成 |  |
| 工作流包處理 | 大部分 | 可在觸控式UI中完全存取。 傳統UI中仍會顯示多個工作流程裝載。 |
| 鎖定／解鎖頁面 | 完成 |  |
| 發佈頁面 | 完成 |  |
| 取消發佈頁面 | 完成 |  |
| 複製頁面 | 已移除 | 使用網站管理員來複製頁面[。](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page) |
| 移動頁面 | 已移除 | 使用網站管理員移動頁面[。](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page) |
| 刪除頁面 | 已移除 | 使用網站管理員來刪除頁面[。](/help/sites-authoring/managing-pages.md#deleting-a-page) |
| 顯示偏好設定 | 已移除 | 使用網站管理員查看[詳細參考清單](/help/sites-authoring/author-environment-tools.md#references)。 |
| 稽核記錄 | 已移除 | 使用網站管理員和[開啟活動邊欄](/help/sites-authoring/author-environment-tools.md#events-timeline)。 |
| 建立版本 | 已移除 | 使用網站管理員建立新版本[。](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version) |
| 還原版本 | 已移除 | 使用站點管理器恢復版本[。](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version) |
| 交換機啟動 | 已移除 | 使用網站管理員在啟動[之間切換。](/help/sites-authoring/launches-promoting.md) |
| 翻譯頁面 | 已移除 | 使用網站管理員將頁面新增至轉譯專案[。](/help/sites-administering/tc-manage.md) |
| 時間彎曲（選擇日期／時間，並依看起來瀏覽網站） | 完成 |  |
| 設定權限 | 完成 |  |
| 用戶端內容UI | 已取代 | 使用[ContextHub](/help/sites-authoring/ch-previewing.md) UI，繼續使用。 |
| 適用於各種媒體類型的內容搜尋器 | 完成 |  |
| 元件清單 | 完成 |  |
| 複製和貼上元件 | 完成 |  |
| 剪貼簿中的元件清單 | 遺失 |  |
| 還原／重做 | 完成 |  |
| 將內容拖曳至元件預留位置 | 完成 |  |
| 使用元件自動建立功能，將內容直接拖曳至parsys預留位置 | 完成 |  |

## 功能狀態：文字、表格和影像編輯器{#feature-status-text-table-and-image-editors}

這是傳統UI文字、表格和影像編輯器的功能清單，以及觸控式UI的狀態。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| RTF 編輯器 | 完成 | 可用於就地、對話和全螢幕。 |
| 啟用／禁用RTE插件 | 完成 | 可以使用[模板編輯器](/help/sites-authoring/templates.md)完成。 |
| 對純文字檔案使用RTE | 完成 |  |
| RTE插件：連結與錨點 | 完成 |  |
| RTE插件：字元地圖 | 完成 |  |
| RTE插件：複製／貼上 | 完成 |  |
| RTE插件：從Microsoft Word貼上 | 完成 |  |
| RTE插件：尋找和取代 | 完成 |  |
| RTE插件：文字格式（粗體， ...） | 完成 |  |
| RTE插件：下標和上標 | 完成 |  |
| RTE插件：對齊 | 完成 |  |
| RTE插件：清單（項目符號／數字） | 完成 |  |
| RTE插件：段落格式 | 完成 |  |
| RTE插件：文字樣式 | 完成 |  |
| RTE插件：來源編輯器（編輯HTML） | 完成 | 僅在對話框和全螢幕中提供。 |
| RTE插件：拼字檢查器 | 完成 |  |
| RTE插件：表（嵌入式表編輯器） | 完成 |  |
| RTE插件：還原／重做 | 完成 |  |
| RTE插件：允許串聯影像 | 完成 |  |
| 表格編輯器 | 完成 | 可用於就地、對話和全螢幕。 |
| 將影像拖曳至表格儲存格 | 完成 | 可用串聯 |
| 影像編輯器 | 完成 | 可用於就地、對話和全螢幕。 |
| 啟用／停用IPE增效模組 | 完成 | AEM 6.3在[範本編輯器](/help/sites-authoring/templates.md)中引入了UI。 |
| IPE外掛程式：裁切 | 完成 |  |
| IPE外掛程式：翻轉 | 完成 |  |
| IPE外掛程式：還原／重做 | 完成 |  |
| IPE外掛程式：影像地圖 | 完成 |  |
| IPE外掛程式：旋轉 | 完成 |  |
| IPE外掛程式：縮放 | 完成 |  |

## 功能狀態：工具{#feature-status-tools}

這是傳統UI擁有的各種工具清單，以及觸控式UI中的狀態。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 任務管理 | 已取代 | 6.0推出專案和工作。 |
| 工作流程收件匣 | 完成 |  |
| 頁面範本設定工作流程(`/etc/workflow/wcm/templates.html`) | 遺失 | 使用Classic UI。 |
| 標籤管理員UI | 完成 |  |
| MSM/Blueprint Control Center | 完成 |  |
| Blueprint Manager UI | 完成 |  |
| 推出設定UI | 遺失 | 使用Classic UI。 |
| 使用者、群組和權限UI | 基本完整 | 若要進行進階權限編輯，請使用Classic UI。 |
| 清除版本(`/etc/versioning/purge.html`) | 遺失 | 使用Classic UI。 |
| 外部連結檢查程式 (`/etc/linkchecker.html`) | 遺失 | 使用Classic UI。 |
| 批量編輯器(`/etc/importers/bulkeditor.html`) | 遺失 | 使用Classic UI。 |
| 上傳縮圖以新增或覆寫這些縮圖 | 遺失 | 使用Classic UI。 |
