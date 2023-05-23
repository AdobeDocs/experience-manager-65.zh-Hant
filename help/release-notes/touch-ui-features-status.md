---
title: 觸控式 UI 功能狀態
description: 特定於 [!DNL Adobe Experience Manager] 啟用觸摸的UI。
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 15%

---

# 觸控式 UI 功能狀態 {#touch-ui-feature-status}

AEM6.4版起 [不建議使用經典UI](../release-notes/deprecated-removed-features.md)。 Adobe不會對經典用戶介面進行進一步的增強，並且鼓勵用戶利用啟用觸摸的用戶介面中提供的強大新功能。

從6.0版開始AEM，引入了一個稱為「觸摸式用戶介面」（簡稱「觸摸式用戶介面」）的新用戶介面，該介面與 [!DNL Adobe Experience Cloud] 以及總體Adobe用戶介面指南。 在幾乎達到功能奇偶校驗後，這已成為標準UI,AEM其中帶有傳統、面向案頭的介面，稱為「經典UI」。

雖然大多數功能都在啟用觸摸的UI中，但有些功能尚未完整，將在將來的版本中添加。

以下清單顯示6.5中實現的權能AEM的當前狀態。

有關升級到6.5的客戶AEM的建議，請參見 [客戶的用戶介面建議](/help/sites-deploying/ui-recommendations.md)。

>[!NOTE]
>
>此頁僅涵蓋與經典UI的功能奇偶校驗。 未列出添加到Touch-enabled UI且在Classic UI中不存在的功能，以及它所獨有的功能。

>[!NOTE]
>
>這份清單力求完整，但並非詳盡無遺。

## 圖例 {#legend}

* **完成**:該功能在啟用觸摸的用戶介面中完全可用。
* **大多**:該功能大多在啟用觸摸的用戶介面中可用。
* **缺少**:該功能不在啟用觸摸的UI中，必須使用經典UI來執行此操作。
* **已更換**:該功能被一個新實現替換，該新實現的工作方式不同。
* **已刪除**:啟用觸摸的UI中不再存在該功能，將不會被替換。

## 功能狀態：站點管理 {#feature-status-sites-admin}

這是經典UI站點管理員(`/siteadmin`)具有和啟用觸摸的UI中的狀態(`/sites.html`)。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 導航站點層次結構 | 完成 | AEM 6.4 [內容樹視圖](/help/sites-authoring/basic-handling.md#content-tree)。 |
| 啟動工作流程 | 完成 |  |
| 建立新頁面 | 完成 |  |
| 建立新網站 | 完成 |  |
| 新建啟動 | 完成 |  |
| 新建livecopy | 完成 |  |
| 建立資料夾 | 完成 |  |
| 顯示發佈狀態 | 完成 | 從AEM6.5開始，工作流狀態顯示在清單視圖中。 |
| 搜尋 | 完成 |  |
| 複製和貼上頁（重複） | 完成 |  |
| 移動頁面 | 完成 |  |
| 發佈頁面 | 完成 |  |
| 發佈頁面（無複製權限） | 完成 |  |
| 稍後發佈 | 完成 |  |
| 發佈樹 | 完成 |  |
| 取消發佈頁面 | 完成 |  |
| 取消發佈頁面，但無複製權限 | 完成 |  |
| 稍後取消發佈 | 完成 |  |
| 刪除 | 完成 |  |
| 鎖定/解鎖 | 完成 |  |
| 檢視/編輯屬性 | 完成 |  |
| 設定頁面上的權限 | 完成 |  |
| 版本歷史記錄 | 完成 |  |
| 還原版本 | 完成 |  |
| 還原樹並還原已刪除的頁 | 缺少 | 使用傳統用戶介面。 |
| 顯示舊版本與當前版本之間的差異 | 完成 |  |
| Livecopy操作（滾出） | 完成 |  |
| 請參閱語言副本 | 完成 |  |
| 查找和替換 | 缺少 | 使用傳統用戶介面。 |
| 通知收件箱（JCR事件） | 缺少 | 使用傳統用戶介面。 將替換為不同的實施。 |
| 引用 | 完成 | 顯示添加到6.AEM5的傳入頁面連結。 |

## 功能狀態：頁面編輯器 {#feature-status-page-editor}

這是經典UI頁面編輯器(`/cf#`)具有並且處於啟用觸摸(`/editor.html`)。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 編輯網頁 | 完成 |  |
| 編輯移動網頁 | 完成 |  |
| 編輯通過設計導入程式導入的內容 | 完成 |  |
| 編輯電子郵件 | 完成 |  |
| 編輯混合移動應用 | 完成 |  |
| 編輯Forms | 完成 |  |
| 編輯優惠 | 完成 |  |
| 編輯工作流模型 | 完成 |  |
| 模式：編輯和預覽 | 完成 |  |
| 響應預覽 | 完成 |  |
| 模式：編輯設計 | 完成 |  |
| 模式：腳手架 | 完成 |  |
| 模式：即時複製狀態 | 完成 |  |
| 添加註釋 | 完成 |  |
| 編輯屬性 | 完成 |  |
| 滾出頁 | 完成 |  |
| 啟動和顯示工作流 | 完成 |  |
| 工作流包處理 | 大多 | 完全可在啟用觸摸的UI中訪問。 傳統UI中仍顯示多個工作流負載。 |
| 鎖定/解鎖頁 | 完成 |  |
| 發佈頁面 | 完成 |  |
| 取消發佈頁面 | 完成 |  |
| 複製頁面 | 已移除 | 使用站點管理員 [複製頁](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page)。 |
| 移動頁面 | 已移除 | 使用站點管理員 [移動頁](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page)。 |
| 刪除頁面 | 已移除 | 使用站點管理員 [刪除頁](/help/sites-authoring/managing-pages.md#deleting-a-page)。 |
| 顯示偏好設定 | 已移除 | 使用站點管理員查看 [詳細參考清單](/help/sites-authoring/author-environment-tools.md#references)。 |
| 稽核記錄 | 已移除 | 使用站點管理和 [開放式活動軌道](/help/sites-authoring/author-environment-tools.md#events-timeline)。 |
| 建立版本 | 已移除 | 使用站點管理員 [建立新版本](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version)。 |
| 還原版本 | 已移除 | 使用站點管理員 [恢復版本](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version)。 |
| 交換機啟動 | 已移除 | 使用站點管理員 [在啟動之間切換](/help/sites-authoring/launches-promoting.md)。 |
| 翻譯頁 | 已移除 | 使用站點管理員 [將頁面添加到翻譯項目](/help/sites-administering/tc-manage.md)。 |
| 時間曲線（選擇日期/時間，然後按所查找的方式瀏覽網站） | 完成 |  |
| 設定權限 | 完成 |  |
| 客戶端上下文UI | 已更換 | 使用 [上下文中心](/help/sites-authoring/ch-previewing.md) UI正在向前。 |
| 用於各種媒體類型的Content Finder | 完成 |  |
| 元件清單 | 完成 |  |
| 複製和貼上元件 | 完成 |  |
| 剪貼簿中的元件清單 | 缺少 |  |
| 還原/取消復原 | 完成 |  |
| 將內容拖到元件佔位符中 | 完成 |  |
| 將內容直接拖到具有元件自動建立的parsys佔位符中 | 完成 |  |

## 功能狀態：文本、表和影像編輯器 {#feature-status-text-table-and-image-editors}

這是經典UI文本、表和影像編輯器具有的功能以及啟用觸摸的UI中的狀態的清單。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| RTF 編輯器 | 完成 | 可用就地、對話框和全屏。 |
| 啟用/禁用RTE插件 | 完成 | 可以使用 [模板編輯器](/help/sites-authoring/templates.md)。 |
| 將RTE用於純文字檔案 | 完成 |  |
| RTE插件：連結和錨點 | 完成 |  |
| RTE插件：字元映射 | 完成 |  |
| RTE插件：複製/貼上 | 完成 |  |
| RTE插件：從MicrosoftWord貼上 | 完成 |  |
| RTE插件：查找和替換 | 完成 |  |
| RTE插件：文本格式（粗體， ...） | 完成 |  |
| RTE插件：下標和上標 | 完成 |  |
| RTE插件：正確 | 完成 |  |
| RTE插件：清單（項目符號/數字） | 完成 |  |
| RTE插件：段落格式 | 完成 |  |
| RTE插件：文本樣式 | 完成 |  |
| RTE插件：原始碼編輯器(編輯HTML) | 完成 | 僅在對話框和全屏中可用。 |
| RTE插件：拼寫檢查器 | 完成 |  |
| RTE插件：表（嵌入式表編輯器） | 完成 |  |
| RTE插件：撤消/重做 | 完成 |  |
| RTE插件：允許聯機影像 | 完成 |  |
| 表編輯器 | 完成 | 可用就地、對話框和全屏。 |
| 將影像拖到表格單元格中 | 完成 | 可用串聯 |
| 影像編輯器 | 完成 | 可用就地、對話框和全屏。 |
| 啟用/禁用IPE插件 | 完成 | AEM6.3在 [模板編輯器](/help/sites-authoring/templates.md)。 |
| IPE插件：裁剪 | 完成 |  |
| IPE插件：翻轉 | 完成 |  |
| IPE插件：撤消/重做 | 完成 |  |
| IPE插件：影像映射 | 完成 |  |
| IPE插件：旋轉 | 完成 |  |
| IPE插件：縮放 | 完成 |  |

## 功能狀態：工具 {#feature-status-tools}

這是經典UI擁有的各種工具以及啟用觸摸的UI中的狀態的清單。

| 功能 | 狀態 | 評論 |
|--- |--- |--- |
| 任務管理 | 已更換 | 6.0介紹了項目和任務。 |
| 工作流收件箱 | 完成 |  |
| 工作流到頁面模板配置(`/etc/workflow/wcm/templates.html`) | 缺少 | 使用傳統用戶介面。 |
| 標籤管理員UI | 完成 |  |
| MSM/藍圖控制中心 | 完成 |  |
| 藍圖管理器UI | 完成 |  |
| 推出配置UI | 缺少 | 使用傳統用戶介面。 |
| 用戶、組和權限UI | 基本完成 | 要進行高級權限編輯，請使用「經典」UI。 |
| 清除版本(`/etc/versioning/purge.html`) | 缺少 | 使用傳統用戶介面。 |
| 外部連結檢查程式 (`/etc/linkchecker.html`) | 缺少 | 使用傳統用戶介面。 |
| 批量編輯器(`/etc/importers/bulkeditor.html`) | 缺少 | 使用傳統用戶介面。 |
| 上載縮略圖以添加或覆蓋這些縮略圖 | 缺少 | 使用傳統用戶介面。 |
