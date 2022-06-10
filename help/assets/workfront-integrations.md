---
title: '"[!DNL Experience Manager Assets] 整合 [!DNL Adobe Workfront]"'
description: 介紹在 [!DNL Assets] 和 [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
source-git-commit: 57304cfb7706377fa5dd7cce0e5863839ffee553
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager Assets] 整合 [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] 是工作管理應用程式，協助您在一個地方管理整個工作生命週期。整合 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 使公司能夠通過將工作與數字資產管理內在地聯繫起來，提高內容的速度和上市時間。 在管理Workfront工作的範圍內，用戶可以訪問所需的檔案和影像。

的 [!DNL Workfront for Experience Manager enhanced connector] 通過端到端工作流實現增強的業務流程，並提供個性化的端到端客戶體驗和中央儲存。 Adobe提供了標準連接器和增強連接器，以整合這兩種解決方案。 有關比較，請參閱下面支援的功能，並參見 [在 [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)。

[!DNL Workfront for Experience Manage enhanced connector] 使您的組織能夠：

* 在Workfront自動建立連結的Experience Manager資料夾，並根據WorkfrontPortfolio、程式和項目組織資料夾。
* 將Workfront項目元資料與連結的Experience Manager資料夾同步。
* Experience Manager元資料更新為新版本。
* 使用Workfront工作流根據可配置條件設定Experience Manager對象狀態。
* 將資產發佈到Experience Manager或發佈到Brand Portal。

查看平台支援和 [增強連接器的先決條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)。

>[!IMPORTANT]
>
>* Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅通過認證合作夥伴或 [!DNL Adobe Professional Services]。 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services]，它不受Adobe支援。
>
>* Adobe可以發佈更新 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使這個連接器冗餘；如果發生這種情況，可能需要客戶從使用此連接器進行過渡。
>
>* Adobe支援增強的連接器1.7.4版和更高版本。 不支援以前的預發行版和自定義版本。 要檢查增強的連接器版本，請導航至 `digital.hoodoo` 組在的左窗格中可用 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant)。
>
>* 請參閱 [Workfront的Experience Manager Assets增強型連接器合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 有關考試的資訊，請參見 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。


## 比較不同的整合 [!DNL Assets] 和 [!DNL Workfront] {#feature-parity-matrix}

以下是通過不同類型的整合提供的功能的詳細資訊 [!DNL Assets] 和 [!DNL Workfront]。

| 功能 | 說明 | [!DNL Workfront] 和 [!DNL Assets Essentials] | [!DNL Workfront] 為 [!DNL Experience Manager] 連接器 | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| 部署方法 | 適合 [!DNL Assets] 提供。 | Assets Essentials | Cloud Service、Adobe托管服務、內部部署 | Cloud Service、Adobe托管服務、內部部署 |
| 從 [!DNL Workfront] 至 [!DNL Assets] | WF文檔的最新版本可以上載到AEM Assets，該文檔將作為文檔的新版本連結。 | ✓ | ✓ | ✓ |
| 手動將文AEM件夾連結到Workfront對象 | 現有AEM資料夾可以作為Workfront資料夾連結，其子資產則作為新Workfront文檔連結。 | ✓ | ✓ | ✓ |
| 連結 [!DNL Assets] 到Workfront物體 | 中的現AEM有資產可以連結到新的Workfront文檔或作為現有文檔的新版本。 | ✓ | ✓ | ✓ |
| 添加到連結資料夾的資產將自動發送AEM到 | 如果文檔添加到連結的資料夾，則關聯的資產將自動作為新資產上載到AEM Assets。 | ✓ | ✓ | ✓ |
| 從Workfront內下載連結的AEM Assets | 在Workfront連結資產時，用戶可以下載資產的位元組。 | ✓ | ✓ | ✓ |
| 在Workfront內搜尋AEM Assets | Workfront的AEM Assets選擇器允許對資產進行全文搜索。 | ✓ | ✓ | ✓ |
| 從Workfront內查AEM看和導航資料夾層次結構 | Workfront的AEM Assets選擇器允許瀏覽受用戶在中設定的關聯訪問控制和權限限制的AEM Assets層次結構AEM。 | ✓ | ✓ | ✓ |
| 取消與AEM Assets在Workfront的資產連結 | 可以從關聯的AEMWorkfront文檔中取消連結現有連結資產。 這不會刪除的原始資AEM產。 | ✓ | ✓ | ✓ |
| 將新版本化資產從Workfront添加到AEM Assets | 在Workfront的文檔上添加新添加的版本時，用戶可以將新版本發送AEM到以替換現有版本。 | ✓ | ✓ | ✓ |
| 按一下直接用戶到時在Workfront連結的資AEM產 | 用戶將從AEMWorkfront內預覽連結的資產。 | ✓ | ✓ | 自訂 |
| 在Workfront自AEM動建立連結資料夾 | 使用對象狀AEM態在Workfront自動建立連結資料夾。 根據Workfront的AEMPortfolio、程式和項目自動組織資料夾。 | 否 | 否 | ✓ |
| 注釋同步 | 自動同步資產注釋 [!DNL Workfront] 至 [!DNL Assets] | 否 | ✓ | ✓ |
| 將Workfront資產元資料映射到AEM Assets | Workfront對象和自定義表單屬性可映射到AEM資產元資料屬性。 初始上載/連結時將推送值。 | ✓ | ✓ | ✓ |
| 在Workfront自動建立文檔自定義Forms | 使用工作流將自定義表單附加到Workfront文檔、任務AEM和問題。 | 否 | 手動添加自定義表單，然後自動同步工作 | ✓ |
| AEM Assets與Workfront元資料雙向自動更新 | 自動更新AEM Assets和Workfront之間的元資料。 | 否 | ✓ | ✓ |
| 將Workfront元資料映射到AEM Assets資料夾 | 將Workfront項目元資料與連結的文AEM件夾同步。 | 否 | 否 | ✓ |
| 元AEM資料更新與新版本 | 可以進行AEM中的配置，以確定Workfront新版本化的資產是否也會推送對其元資料所做的任何更改。 | 否 | 否 | ✓ |
| 自動更新AEMWorkfront自定義Forms的元資料 | Workfront被配置為AEM將指定的資產元資料屬性映射到文檔自定義窗體。 當資產初始連結時，或當資產更新時，這些元資料屬性的值被複製到相應的Workfront文檔自定義表單域。 必須小心，防止這一變AEM化被退回AEM，彷彿是源自Workfront的變化。 | 否 | ✓ | ✓ |
| 在連結資產上建立新證明版本 | 在將Workfront的資產連結時，可自動生成證明。 | 否 | ✓ | 自訂 |
| 設定Workfront對象的狀態 | 使用工作流設定基於Workfront對象狀態的可配AEM置條件 | 否 | 否 | ✓ |
| 將資產發佈到AEM發佈環境或Brand Portal | 為Workfront用戶提供自動將連結資產發佈到AEM發佈環境或Brand Portal的選項。 | 否 | 否 | ✓ |
