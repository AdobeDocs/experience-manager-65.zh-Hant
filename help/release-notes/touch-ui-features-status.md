---
title: 觸控式 UI 功能狀態
description: 專屬於 [!DNL Adobe Experience Manager] 觸控式UI。
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 14%

---

# 觸控式 UI 功能狀態 {#touch-ui-feature-status}

AEM 6.4以上 [已棄用傳統UI](../release-notes/deprecated-removed-features.md). Adobe不會對傳統UI進行進一步的增強，建議使用者運用觸控式UI中提供的強大新功能。

從6.0版開始，AEM推出新的使用者介面，稱為與 [!DNL Adobe Experience Cloud] 和整體Adobe使用者介面准則。 在達到幾乎相同功能後，這便成為AEM中標準的UI，其舊版案頭導向介面稱為「傳統UI」。

雖然大部分的功能都存在於觸控式UI中，但有些功能尚未完整，且將會在未來版本中新增。

下列清單顯示AEM 6.5中實作之功能的目前狀態。

如需升級至AEM 6.5的客戶建議，請參閱 [客戶適用的使用者介面建議](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>此頁面僅涵蓋傳統UI的同等功能。 傳統UI中不存在的觸控式UI新增及獨特的功能並未列出。

>[!NOTE]
>
>這份清單力求完整，但並非詳盡無遺。

## 圖例 {#legend}

* **完成**:觸控式UI已完全提供此功能。
* **多數**:此功能大多可在觸控式UI中使用。
* **遺失**:觸控式UI中不存在此功能，必須使用傳統UI執行此動作。
* **已更換**:功能已更換為運作方式不同的新實作。
* **已移除**:觸控式UI中已不存在此功能，且將不會取代。

## 功能狀態：網站管理員 {#feature-status-sites-admin}

這是傳統UI網站管理員(`/siteadmin`)在觸控式UI中具有和狀態(`/sites.html`)。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 導覽網站階層 | 完成 | AEM 6.4導入 [內容樹視圖](/help/sites-authoring/basic-handling.md#content-tree). |
| 啟動工作流程 | 完成 |  |
| 建立新頁面 | 完成 |  |
| 建立新網站 | 完成 |  |
| 建立新啟動 | 完成 |  |
| 建立新LiveCopy | 完成 |  |
| 建立資料夾 | 完成 |  |
| 顯示發佈狀態 | 完成 | 從AEM 6.5開始，工作流程狀態會顯示在清單檢視中。 |
| 搜尋 | 完成 |  |
| 複製並貼上頁面（複製） | 完成 |  |
| 移動頁面 | 完成 |  |
| 發佈頁面 | 完成 |  |
| 沒有復寫權限的發佈頁面 | 完成 |  |
| 稍後發佈 | 完成 |  |
| 發佈樹 | 完成 |  |
| 取消發佈頁面 | 完成 |  |
| 取消發佈頁面，不具有復寫權限 | 完成 |  |
| 稍後取消發佈 | 完成 |  |
| 刪除 | 完成 |  |
| 鎖定/解除鎖定 | 完成 |  |
| 檢視/編輯屬性 | 完成 |  |
| 在頁面上設定權限 | 完成 |  |
| 版本記錄 | 完成 |  |
| 還原版本 | 完成 |  |
| 還原樹並還原已刪除的頁 | 遺失 | 使用傳統UI。 |
| 顯示舊版和當前版本之間的差異 | 完成 |  |
| Livecopy動作（轉出） | 完成 |  |
| 請參閱語言副本 | 完成 |  |
| 查找和替換 | 遺失 | 使用傳統UI。 |
| 通知收件匣（JCR事件） | 遺失 | 使用傳統UI。 將取代為不同的實作。 |
| 引用 | 完成 | 顯示新增至AEM 6.5的傳入頁面連結。 |

## 功能狀態：頁面編輯器 {#feature-status-page-editor}

這是傳統UI頁面編輯器(`/cf#`)具有且狀態為觸控式(`/editor.html`)。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 編輯網頁 | 完成 |  |
| 編輯行動網頁 | 完成 |  |
| 編輯透過設計匯入工具匯入的內容 | 完成 |  |
| 編輯電子郵件 | 完成 |  |
| 編輯混合式行動應用程式 | 完成 |  |
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
| 工作流程套件處理 | 多數 | 可在觸控式UI中完全存取。 傳統UI中仍會顯示多個工作流程裝載。 |
| 鎖定/解除鎖定頁面 | 完成 |  |
| 發佈頁面 | 完成 |  |
| 取消發佈頁面 | 完成 |  |
| 複製頁面 | 已移除 | 使用網站管理員 [複製頁面](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| 移動頁面 | 已移除 | 使用網站管理員 [移動頁面](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| 刪除頁面 | 已移除 | 使用網站管理員 [刪除頁面](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| 顯示偏好設定 | 已移除 | 使用網站管理員來查看 [詳細參考清單](/help/sites-authoring/author-environment-tools.md#references). |
| 稽核記錄 | 已移除 | 使用網站管理員和 [開啟活動邊欄](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| 建立版本 | 已移除 | 使用網站管理員 [建立新版本](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| 還原版本 | 已移除 | 使用網站管理員 [還原版本](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| 交換機啟動 | 已移除 | 使用網站管理員 [切換啟動](/help/sites-authoring/launches-promoting.md). |
| 翻譯頁面 | 已移除 | 使用網站管理員 [新增頁面至翻譯專案](/help/sites-administering/tc-manage.md). |
| 時間扭曲（選擇日期/時間，並依看到的方式瀏覽網站） | 完成 |  |
| 設定權限 | 完成 |  |
| 用戶端內容UI | 已更換 | 使用 [ContextHub](/help/sites-authoring/ch-previewing.md) UI之後。 |
| 各種媒體類型的內容尋找器 | 完成 |  |
| 元件清單 | 完成 |  |
| 複製和貼上元件 | 完成 |  |
| 剪貼簿中的元件清單 | 遺失 |  |
| 還原/重做 | 完成 |  |
| 將內容拖曳至元件預留位置 | 完成 |  |
| 透過自動建立元件，將內容直接拖曳至parsys預留位置 | 完成 |  |

## 功能狀態：文字、表格和影像編輯器 {#feature-status-text-table-and-image-editors}

這是傳統UI文字、表格和影像編輯器所具備的功能清單，以及觸控式UI中的狀態。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| RTF 編輯器 | 完成 | 就地、對話方塊和全螢幕皆可使用。 |
| 啟用/停用RTE外掛程式 | 完成 | 可使用 [範本編輯器](/help/sites-authoring/templates.md). |
| 使用RTE進行純文字檔案 | 完成 |  |
| RTE外掛程式：連結和錨點 | 完成 |  |
| RTE外掛程式：字元圖 | 完成 |  |
| RTE外掛程式：複製/貼上 | 完成 |  |
| RTE外掛程式：從Microsoft Word貼上 | 完成 |  |
| RTE外掛程式：查找和替換 | 完成 |  |
| RTE外掛程式：文字格式（粗體、 ...） | 完成 |  |
| RTE外掛程式：子和上標 | 完成 |  |
| RTE外掛程式：正文 | 完成 |  |
| RTE外掛程式：清單（項目符號/數字） | 完成 |  |
| RTE外掛程式：段落格式 | 完成 |  |
| RTE外掛程式：文字樣式 | 完成 |  |
| RTE外掛程式：原始碼編輯器(編輯HTML) | 完成 | 僅限對話方塊和全螢幕使用。 |
| RTE外掛程式：拼字檢查程式 | 完成 |  |
| RTE外掛程式：表（嵌入式表編輯器） | 完成 |  |
| RTE外掛程式：還原/重做 | 完成 |  |
| RTE外掛程式：允許線上影像 | 完成 |  |
| 表格編輯器 | 完成 | 就地、對話方塊和全螢幕皆可使用。 |
| 將影像拖曳至表格儲存格 | 完成 | 可用線上 |
| 影像編輯器 | 完成 | 就地、對話方塊和全螢幕皆可使用。 |
| 啟用/禁用IPE插件 | 完成 | AEM 6.3在 [範本編輯器](/help/sites-authoring/templates.md). |
| IPE插件：裁切 | 完成 |  |
| IPE插件：翻轉 | 完成 |  |
| IPE插件：還原/重做 | 完成 |  |
| IPE插件：影像圖 | 完成 |  |
| IPE插件：旋轉 | 完成 |  |
| IPE插件：縮放 | 完成 |  |

## 功能狀態：工具 {#feature-status-tools}

這是傳統UI擁有的各種工具清單，以及觸控式UI中的狀態。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 任務管理 | 已更換 | 6.0介紹項目和任務。 |
| 工作流程收件匣 | 完成 |  |
| 頁面範本設定的工作流程(`/etc/workflow/wcm/templates.html`) | 遺失 | 使用傳統UI。 |
| 標籤管理員UI | 完成 |  |
| MSM/Blueprint控制中心 | 完成 |  |
| Blueprint管理器UI | 完成 |  |
| 轉出設定UI | 遺失 | 使用傳統UI。 |
| 使用者、群組和權限UI | 基本完成 | 若要進行進階權限編輯，請使用傳統UI。 |
| 清除版本(`/etc/versioning/purge.html`) | 遺失 | 使用傳統UI。 |
| 外部連結檢查程式 (`/etc/linkchecker.html`) | 遺失 | 使用傳統UI。 |
| 大量編輯器(`/etc/importers/bulkeditor.html`) | 遺失 | 使用傳統UI。 |
| 上傳縮圖以新增或覆寫這些縮圖 | 遺失 | 使用傳統UI。 |
