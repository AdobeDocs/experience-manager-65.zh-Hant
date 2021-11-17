---
title: '[!DNL Experience Manager Assets] integration with [!DNL Adobe Workfront]'
description: 介紹 [!DNL Assets] 和 [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
source-git-commit: 8d39e1c86e5185a181400f10b7822a57c9d3aeae
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager Assets] 整合 [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] 是一種工作管理應用程式，可幫助您在一個位置管理工作的整個生命週期。 整合 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 讓組織通過內在連接工作和數字資產管理來提高內容速度和上市時間。 在Workfront中管理其工作的內容中，使用者可存取所需的檔案和影像。

此 [!DNL Workfront for Experience Manager enhanced connector] 通過端到端工作流支援增強的業務流程，並提供個性化的端到端客戶體驗和集中儲存。 如需 [!DNL enhanced connector]，請參閱 [新增功能 [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] 讓您的組織：

* 在Workfront中自動建立連結的Experience Manager資料夾，並根據WorkfrontPortfolio、方案和專案組織資料夾。
* 將Workfront專案中繼資料與連結的Experience Manager資料夾同步。
* Experience Manager中繼資料會以新版本更新。
* 使用Workfront工作流程，根據可設定條件設定Experience Manager物件狀態。
* 將資產發佈至Experience Manager發佈環境或Brand Portal。

請參閱平台支援和 [enhanced connector的必要條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>Adobe需要部署，並配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services],Adobe不支援。
>
>Adobe可發行 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此連接器冗餘；如果發生此情況，客戶可能需要從使用此連接器進行轉變。

## 比較不同的整合 [!DNL Assets] 和 [!DNL Workfront] {#feature-parity-matrix}

以下是可透過以下各種整合功能的詳細資訊： [!DNL Assets] 和 [!DNL Workfront].

| 功能 | 說明 | [!DNL Workfront]與[!DNL Assets Essentials] | [!DNL Workfront] for [!DNL Experience Manager] 連接器 | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| 部署方法 | 適合 [!DNL Assets] 提供。 | Assets Essentials | Cloud Service, Adobe Managed Services，內部部署 | Cloud Service, Adobe Managed Services，內部部署 |
| 從 [!DNL Workfront] to [!DNL Assets] | WF文檔的最新版本可以上載到AEM Assets，該文檔將作為新版本連結。 | ✓ | ✓ | ✓ |
| 手動將AEM資料夾連結至Workfront物件 | 現有的AEM資料夾可以連結為Workfront資料夾，其子資產可以連結為新的Workfront檔案。 | ✓ | ✓ | ✓ |
| 連結 [!DNL Assets] 至Workfront物件 | AEM中的現有資產可以連結至新Workfront檔案，或連結為現有檔案的新版本。 | ✓ | ✓ | ✓ |
| 新增至連結資料夾的資產會自動傳送至AEM | 如果將檔案新增至連結的資料夾，則相關聯的資產會自動上傳至AEM Assets做為新資產。 | ✓ | ✓ | ✓ |
| 從Workfront下載連結的AEM Assets | 在Workfront中連結資產時，使用者可以下載資產的位元組。 | ✓ | ✓ | ✓ |
| 從Workfront中搜尋AEM Assets | Workfront中的AEM Assets選取器允許資產的全文搜尋。 | ✓ | ✓ | ✓ |
| 從Workfront檢視並導覽AEM資料夾階層 | Workfront中的AEM Assets選取器可瀏覽受使用者在AEM中設定之相關存取控制和權限所限制的AEM Assets階層。 | ✓ | ✓ | ✓ |
| 取消連結Workfront中的AEM Assets資產 | 可從相關聯的Workfront檔案中取消連結來自AEM的現有連結資產。 這不會刪除AEM內的原始資產。 | ✓ | ✓ | ✓ |
| 從Workfront將新版本控制資產新增至AEM Assets | 在Workfront的檔案上新增新增的版本時，使用者可將新版本傳送至AEM，以取代現有版本。 | ✓ | ✓ | ✓ |
| 按一下「將使用者導向AEM」時在Workfront中連結的資產 | 系統會將使用者導向至AEM，從Workfront內預覽連結的資產。 | ✓ | ✓ | 自訂 |
| 在Workfront中自動建立連結的AEM資料夾 | 使用物件狀態在Workfront中自動建立連結的AEM資料夾。 根據WorkfrontPortfolio、方案和專案自動組織AEM資料夾。 | 否 | 否 | ✓ |
| 注釋同步 | 自動同步資產的註解 [!DNL Workfront] to [!DNL Assets] | 否 | ✓ | ✓ |
| 將Workfront資產中繼資料對應至AEM Assets | Workfront物件和自訂表單屬性可對應至AEM資產中繼資料屬性。 值會在初始上傳/連結時推送。 | ✓ | ✓ | ✓ |
| 在Workfront中自動建立檔案自訂Forms | 使用AEM工作流程將自訂表單附加至Workfront檔案、工作和問題。 | 否 | 手動新增自訂表單，然後自動同步即可運作 | ✓ |
| AEM Assets與Workfront元資料雙向自動更新 | 自動更新AEM Assets和Workfront之間的中繼資料。 | 否 | ✓ | ✓ |
| 將Workfront中繼資料對應至AEM Assets資料夾 | 將Workfront專案中繼資料與連結的AEM資料夾同步。 | 否 | 否 | ✓ |
| AEM中繼資料更新為新版本 | 可進行AEM中的設定，以判斷Workfront中新版本的資產是否也會隨對其中繼資料所做的任何變更推送。 | 否 | 否 | ✓ |
| 變更Workfront中的自訂Forms時自動更新AEM中繼資料 | Workfront的設定方式為將指定的AEM資產中繼資料屬性對應至檔案自訂表單。 最初連結資產或更新資產時，這些中繼資料屬性的值會複製到對應的Workfront檔案自訂表單欄位。 請務必謹慎防止變更從AEM傳回至AEM，如同是源自Workfront的變更。 | 否 | ✓ | ✓ |
| 在連結的資產上建立新校樣版本 | 在Workfront中連結資產時，會自動產生校樣。 | 否 | ✓ | 自訂 |
| 在Workfront物件上設定狀態 | 使用AEM工作流程，根據可設定條件設定Workfront物件狀態 | 否 | 否 | ✓ |
| 將資產發佈至AEM發佈環境或Brand Portal | 為Workfront使用者提供自動將連結資產發佈至AEM發佈環境或Brand Portal的選項。 | 否 | 否 | ✓ |
