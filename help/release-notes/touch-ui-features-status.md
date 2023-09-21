---
title: 觸控式 UI 功能狀態
description: 特定版本注意事項 [!DNL Adobe Experience Manager] 觸控式UI。
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 15%

---

# 觸控式 UI 功能狀態 {#touch-ui-feature-status}

Adobe Experience Manager (AEM) 6.4以後 [已棄用傳統UI](../release-notes/deprecated-removed-features.md). Adobe不再對傳統UI做任何增強功能，而是鼓勵使用者使用觸控式UI提供的強大新功能。

從6.0版開始，AEM推出了稱為「觸控式UI」（稱為「觸控式UI」）的新使用者介面，此介面與 [!DNL Adobe Experience Cloud] 以及整體Adobe使用者介面准則。 隨著功能接近同位，這成為AEM中的標準UI，具有稱為「傳統UI」的舊式案頭導向介面。

雖然大部分的功能都存在於觸控式UI中，但有些功能尚不完整，且會在未來版本中新增。

下列清單顯示AEM 6.5中已實作之功能的狀態。

如需升級至AEM 6.5之客戶的建議，請參閱 [客戶適用的使用者介面建議](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>本頁僅說明傳統UI的功能對等原則。 系統不會列出傳統UI中未提供的觸控式UI新增及專屬功能。

>[!NOTE]
>
>此清單力求完整，但並非詳盡無遺。

## 圖例 {#legend}

* **完成**：觸控式UI可完全使用此功能。
* **大部分**：此功能主要在觸控式UI中提供。
* **遺失**：觸控式UI中未出現此功能，因此必須使用傳統UI來執行此動作。
* **已取代**：功能已由運作方式不同的新實作所取代。
* **已移除**：觸控式UI中不再有此功能，且將無法取代。

## 功能狀態：網站管理員 {#feature-status-sites-admin}

這是傳統UI網站管理員(`/siteadmin`)在觸控式UI中擁有和狀態(`/sites.html`)。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 導覽網站階層 | 完成 | AEM 6.4推出了 [內容樹狀檢視](/help/sites-authoring/basic-handling.md#content-tree). |
| 啟動工作流程 | 完成 |  |
| 建立新頁面 | 完成 |  |
| 建立新網站 | 完成 |  |
| 建立新的啟動 | 完成 |  |
| 建立新的即時副本 | 完成 |  |
| 建立資料夾 | 完成 |  |
| 顯示發佈狀態 | 完成 | 從AEM 6.5開始，工作流程狀態會顯示在清單檢視中。 |
| 搜尋 | 完成 |  |
| 複製並貼上頁面（複製） | 完成 |  |
| 移動頁面 | 完成 |  |
| 發佈頁面 | 完成 |  |
| 發佈沒有復寫許可權的頁面 | 完成 |  |
| 稍後發佈 | 完成 |  |
| 發佈樹狀結構 | 完成 |  |
| 取消發佈頁面 | 完成 |  |
| 取消發佈沒有復寫許可權的頁面 | 完成 |  |
| 稍後取消發佈 | 完成 |  |
| 刪除 | 完成 |  |
| 鎖定/解鎖 | 完成 |  |
| 檢視/編輯屬性 | 完成 |  |
| 設定頁面許可權 | 完成 |  |
| 版本記錄 | 完成 |  |
| 還原版本 | 完成 |  |
| 還原樹狀結構並還原已刪除的頁面 | 遺失 | 使用傳統UI。 |
| 顯示舊版本和目前版本之間的差異 | 完成 |  |
| 即時副本動作（轉出） | 完成 |  |
| 檢視語言副本 | 完成 |  |
| 尋找和取代 | 遺失 | 使用傳統UI。 |
| 通知收件匣（JCR事件） | 遺失 | 使用傳統UI。 已取代為未來的其他實作。 |
| 參考 | 完成 | 顯示新增至AEM 6.5的傳入頁面連結。 |

## 功能狀態：頁面編輯器 {#feature-status-page-editor}

這是傳統UI頁面編輯器的功能清單(`/cf#`)在已啟用觸控功能( )中具有和狀態`/editor.html`)。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 編輯網頁 | 完成 |  |
| 編輯行動網頁 | 完成 |  |
| 編輯透過設計匯入工具匯入的內容 | 完成 |  |
| 編輯電子郵件 | 完成 |  |
| 編輯混合行動應用程式 | 完成 |  |
| 編輯Forms | 完成 |  |
| 編輯選件 | 完成 |  |
| 編輯工作流程模型 | 完成 |  |
| 模式：編輯和預覽 | 完成 |  |
| 回應式預覽 | 完成 |  |
| 模式：編輯設計 | 完成 |  |
| 模式：支架 | 完成 |  |
| 模式：即時副本狀態 | 完成 |  |
| 新增註解 | 完成 |  |
| 編輯屬性 | 完成 |  |
| 轉出頁面 | 完成 |  |
| 開始和顯示工作流程 | 完成 |  |
| 工作流程封裝處理 | 大部分 | 可在觸控式UI中存取。 傳統UI中仍會顯示多個工作流程裝載。 |
| 鎖定/解除鎖定頁面 | 完成 |  |
| 發佈頁面 | 完成 |  |
| 取消發佈頁面 | 完成 |  |
| 複製頁面 | 已移除 | 使用網站管理員 [複製頁面](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| 移動頁面 | 已移除 | 使用網站管理員 [移動頁面](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| 刪除頁面 | 已移除 | 使用網站管理員 [刪除頁面](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| 顯示偏好設定 | 已移除 | 使用網站管理員來檢視 [詳細參考清單](/help/sites-authoring/author-environment-tools.md#references). |
| 稽核記錄 | 已移除 | 使用網站管理員和 [開啟活動邊欄](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| 建立版本 | 已移除 | 使用網站管理員 [建立新版本](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| 還原版本 | 已移除 | 使用網站管理員 [還原版本](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| 切換啟動 | 已移除 | 使用網站管理員 [在啟動之間切換](/help/sites-authoring/launches-promoting.md). |
| 翻譯頁面 | 已移除 | 使用網站管理員 [新增頁面至翻譯專案](/help/sites-administering/tc-manage.md). |
| 時間扭曲（選擇日期/時間並瀏覽當時的網站） | 完成 |  |
| 設定許可權 | 完成 |  |
| Client Context UI | 已取代 | 使用 [ContextHub](/help/sites-authoring/ch-previewing.md) UI向後。 |
| 各種媒體型別的內容尋找器 | 完成 |  |
| 元件清單 | 完成 |  |
| 複製和貼上元件 | 完成 |  |
| 剪貼簿中的元件清單 | 遺失 |  |
| 還原/取消復原 | 完成 |  |
| 將內容拖曳至元件預留位置 | 完成 |  |
| 透過自動建立元件將內容直接拖曳至Parsys預留位置 | 完成 |  |

## 功能狀態：文字、表格和影像編輯器 {#feature-status-text-table-and-image-editors}

這是傳統UI文字、表格和影像編輯器所擁有的功能清單，以及觸控式UI中的狀態。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| RTF 編輯器 | 完成 | 可在原位、對話方塊及全熒幕中使用。 |
| 啟用/停用RTE外掛程式 | 完成 | 您可以透過以下方式完成 [範本編輯器](/help/sites-authoring/templates.md). |
| 針對純文字使用RTE | 完成 |  |
| RTE外掛程式：連結和錨點 | 完成 |  |
| RTE外掛程式：字元對應 | 完成 |  |
| RTE外掛程式：複製/貼上 | 完成 |  |
| RTE外掛程式：從Microsoft® Word貼上 | 完成 |  |
| RTE外掛程式：尋找和取代 | 完成 |  |
| RTE外掛程式：文字格式（粗體、...） | 完成 |  |
| RTE外掛程式：下標與上標 | 完成 |  |
| RTE外掛程式：調整 | 完成 |  |
| RTE外掛程式：清單（專案符號/編號） | 完成 |  |
| RTE外掛程式：段落格式 | 完成 |  |
| RTE外掛程式：文字樣式 | 完成 |  |
| RTE外掛程式：來源編輯器(編輯HTML) | 完成 | 僅於對話方塊和全熒幕中使用。 |
| RTE外掛程式：拼字檢查 | 完成 |  |
| RTE外掛程式：表格（內嵌表格編輯器） | 完成 |  |
| RTE外掛程式：還原/重做 | 完成 |  |
| RTE外掛程式：允許內嵌影像 | 完成 |  |
| 表格編輯器 | 完成 | 可在原位、對話方塊及全熒幕中使用。 |
| 將影像拖曳至表格儲存格 | 完成 | 可內嵌使用 |
| 影像編輯器 | 完成 | 可在原位、對話方塊及全熒幕中使用。 |
| 啟用/停用IPE外掛程式 | 完成 | AEM 6.3在中引入了UI [範本編輯器](/help/sites-authoring/templates.md). |
| IPE外掛程式：裁切 | 完成 |  |
| IPE外掛程式：翻轉 | 完成 |  |
| IPE外掛程式：還原/重做 | 完成 |  |
| IPE外掛程式：影像地圖 | 完成 |  |
| IPE外掛程式：旋轉 | 完成 |  |
| IPE外掛程式：縮放 | 完成 |  |

## 功能狀態：工具 {#feature-status-tools}

這是傳統UI所擁有的各種工具清單，以及觸控式UI中的狀態。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 任務管理 | 已取代 | 6.0引進了專案和任務。 |
| 工作流程收件匣 | 完成 |  |
| 頁面範本設定的工作流程(`/etc/workflow/wcm/templates.html`) | 遺失 | 使用傳統UI。 |
| 標籤管理員UI | 完成 |  |
| MSM/Blueprint控制中心 | 完成 |  |
| Blueprint Manager UI | 完成 |  |
| 轉出設定UI | 遺失 | 使用傳統UI。 |
| 使用者、群組和許可權UI | 大部分完成 | 如需進階許可權編輯，請使用傳統UI。 |
| 清除版本(`/etc/versioning/purge.html`) | 遺失 | 使用傳統UI。 |
| 外部連結檢查程式 (`/etc/linkchecker.html`) | 遺失 | 使用傳統UI。 |
| 大量編輯器(`/etc/importers/bulkeditor.html`) | 遺失 | 使用傳統UI。 |
| 上傳縮圖以新增或覆寫縮圖 | 遺失 | 使用傳統UI。 |
