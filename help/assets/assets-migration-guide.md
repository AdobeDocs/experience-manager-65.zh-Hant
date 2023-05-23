---
title: 批量遷移資產
description: 介紹如何將資產引入 [!DNL Adobe Experience Manager]、應用元資料、生成格式副本並激活它們以發佈實例。
contentOwner: AG
role: Architect, Admin
feature: Migration,Renditions,Asset Management
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1799'
ht-degree: 8%

---

# 如何批量遷移資產 {#assets-migration-guide}

將資產遷移到 [!DNL Adobe Experience Manager]，需要考慮幾個步驟。 將資產和元資料從其當前首頁中提取出來不在本文檔的範圍之內，因為它在實施之間差異很大，但本文檔介紹如何將這些資產引入 [!DNL Experience Manager]、應用其元資料、生成格式副本並激活它們以發佈實例。

## 必備條件 {#prerequisites}

在實際執行此方法中的任何步驟之前，請審查並執行 [資產效能調整提示](performance-tuning-guidelines.md)。 許多步驟（如配置最大併發作業）都大大增強了伺服器在負載下的穩定性和效能。 在系統載入了資產後，其他步驟（如配置檔案資料儲存）的執行難度要大得多。

>[!NOTE]
>
>以下資產遷移工具不是 [!DNL Experience Manager] 且不受Adobe支援：
>
>* ACS工AEM具標籤製作器
>* ACS工AEM具CSV資產導入程式
>* ACS公域批量工作流管理器
>* ACS Commons快速操作管理器
>* 合成工作流
>
>本軟體為開放原始碼， [Apache v2授權涵蓋此軟體](https://adobe-consulting-services.github.io/pages/license.html)。若要提出問題或報告問題，請造訪ACS AEM工具和 [ACS AEM公域的GitHub](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)[問題](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)。

## 遷移到 [!DNL Experience Manager] {#migrating-to-aem}

將資產遷移到 [!DNL Experience Manager] 需要幾個步驟，應視為分階段的過程。 遷移的階段如下：

1. 禁用工作流。
1. 載入標籤。
1. 吸食資產。
1. 處理格式副本。
1. 激活資產。
1. 啟用工作流。

![chlimage_1-223](assets/chlimage_1-223.png)

### 禁用工作流 {#disabling-workflows}

在開始遷移之前，請禁用 [!UICONTROL DAM更新資產] 工作流。 最好將所有資產都接收到系統中，然後分批運行工作流。 如果在遷移進行時您已處於活動狀態，則可以安排這些活動在非工作時間運行。

### 載入標籤 {#loading-tags}

您可能已經準備好了要應用於映像的標籤分類。 而CSV資產導入程式和 [!DNL Experience Manager] 支援元資料配置檔案可以自動將標籤應用到資產的過程，標籤需要載入到系統中。 的 [ACS工AEM具標籤製作器](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) 功能，您可以使用載入到系統中的MicrosoftExcel電子錶格來填充標籤。

### 攝取資產 {#ingesting-assets}

在將資產納入系統時，效能和穩定性是一個重要問題。 因為您正在將大量資料載入到系統中，所以您希望確保系統能夠盡可能地運行，以最小化所需的時間量並避免系統超載，這可能導致系統崩潰，特別是在已在生產中的系統中。

將資產載入到系統中有兩種方法：使用HTTP的基於推的方法或使用JCR API的基於拖拉的方法。

#### 通過HTTP發送 {#pushing-through-http}

Adobe的Managed Services團隊使用一個名為Glutton的工具將資料載入到客戶環境中。 Glutton是一個小型Java應用程式，它將所有資產從一個目錄載入到 [!DNL Experience Manager] 部署。 您還可以使用諸如Perl指令碼之類的工具將資產發佈到儲存庫中，而不是Glutton。

使用通過https的方法有兩個主要缺點：

1. 資產需要通過HTTP傳輸到伺服器。 這需要相當多的開銷，而且非常耗時，因此延長了執行遷移所花費的時間。
1. 如果您具有必須應用於資產的標籤和自定義元資料，則此方法需要運行第二個自定義進程，以便在導入此元資料後將這些元資料應用於資產。

接收資產的另一種方法是從本地檔案系統中提取資產。 但是，如果無法將外部驅動器或網路共用裝載到伺服器以執行基於拉式的方法，則通過HTTP發佈資產是最佳選項。

#### 從本地檔案系統讀取 {#pulling-from-the-local-filesystem}

的 [ACS工AEM具CSV資產導入程式](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) 從檔案系統中提取資產，並從CSV檔案中提取資產元資料以導入資產。 Experience Manager資產管理器API用於將資產導入系統並應用配置的元資料屬性。 理想情況下，資產通過網路檔案裝載或通過外部驅動器裝載到伺服器上。

由於資產不需要通過網路傳輸，因此總體效能會大大提高，而且通常認為此方法是將資產載入到儲存庫中的最有效方法。 此外，由於該工具支援元資料接收，因此您可以在一個步驟中導入所有資產和元資料，而不是建立第二個步驟通過單獨的工具應用元資料。

### 處理格式副本 {#processing-renditions}

將資產載入到系統後，需要通過 [!UICONTROL DAM更新資產] 工作流以提取元資料並生成格式副本。 執行此步驟之前，需要複製和修改 [!UICONTROL DAM更新資產] 工作流以滿足您的需求。 現成工作流包含許多您可能不需要的步驟，如Dynamic MediaPTIFF生成或 [!DNL InDesign Server] 整合。

根據需要配置工作流後，您有兩個選項可以執行它：

1. 最簡單的方法是 [ACS公域的批量工作流管理器](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html)。 此工具允許您執行查詢並通過工作流處理查詢結果。 還有設定批大小的選項。
1. 您可搭配「合成工 [作流程」使用ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html)[](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)。雖然此方法涉及的範圍更廣，但它允許您刪除 [!DNL Experience Manager] 工作流引擎，同時優化伺服器資源的使用。 此外，Fast Action Manager還通過動態監控伺服器資源並調節系統上的負載，進一步提高了效能。ACS Commons功能頁上提供了示例指令碼。

### 激活資產 {#activating-assets}

對於具有發佈層的部署，您需要將資產激活到發佈場。 儘管Adobe建議運行多個單個發佈實例，但最好將所有資產複製到單個發佈實例，然後克隆該實例。 激活大量資產時，在觸發樹激活後，您可能需要進行干預。 原因如下：觸發激活時，項目將添加到Sling作業/事件隊列。 當此隊列的大小開始超過大約40,000個項目後，處理速度將急劇減慢。 當此隊列的大小超過100,000個項目後，系統穩定性開始受到影響。

要解決此問題，可使用 [快速操作管理器](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) 管理資產複製。 這在不使用Sling隊列的情況下工作，降低了開銷，同時限制了工作負載以防止伺服器過載。 使用FAM管理複製的示例顯示在功能的文檔頁面上。

將資產傳送至發佈農場的其他選項包括使 [用vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html)[或oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)，這些工具是Jackrabbit的一部份。另一個選項是使用開源工具 [!DNL Experience Manager] 基礎設施 [格拉比特](https://github.com/TWCable/grabbit)它聲稱效能比vlt快。

對於這些方法中的任何一種而言，注意的是，提交人案件上的資產沒有顯示為已激活。 要處理以正確激活狀態標籤這些資產的問題，您還需要運行一個指令碼，將這些資產標籤為已激活。

>[!NOTE]
>
>Adobe不維護或支援Grabbit。

### 克隆發佈 {#cloning-publish}

激活資產後，您可以克隆發佈實例以建立部署所需的盡可能多的副本。 克隆伺服器是相當簡單的，但需要記住一些重要步驟。 要克隆發佈：

1. 備份源實例和資料儲存。
1. 將實例和資料儲存的備份還原到目標位置。 以下步驟均引用此新實例。
1. 在下執行檔案系統搜索 `crx-quickstart/launchpad/felix` 為 `sling.id`。 刪除此檔案。
1. 在資料儲存的根路徑下，查找並刪除任何 `repository-XXX` 的子菜單。
1. 編輯 `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 和 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` 指向新環境上資料儲存的位置。
1. 啟動環境。
1. 更新作者上任何複製代理的配置以指向新實例上正確的發佈實例或調度程式刷新代理，以指向新環境的正確調度程式。

### 啟用工作流 {#enabling-workflows}

一旦完成遷移， [!UICONTROL DAM更新資產] 應重新啟用工作流，以支援生成格式副本和提取元資料，以用於日常系統使用。

## 跨 [!DNL Experience Manager] 部署 {#migrating-between-aem-instances}

雖然這種情況並不常見，但有時您需要從一個遷移大量資料 [!DNL Experience Manager] 部署到另一個位置；例如，當您執行 [!DNL Experience Manager] 升級、升級硬體或遷移到新的資料中心，如使用AMS遷移。

在這種情況下，您的資產已填充了元資料，並且已生成格式副本。 您只需將精力集中在將資產從一個實例移動到另一個實例上即可。 在之間遷移時 [!DNL Experience Manager] 部署，請執行以下步驟：

1. 禁用工作流：由於您正在遷移格式副本和我們的資產，因此您要禁用工作流啟動程式 [!UICONTROL DAM更新資產] 工作流。

1. 遷移標籤：因為您已在源中載入了標籤 [!DNL Experience Manager] 部署時，您可以在內容包中構建它們，並在目標實例上安裝該包。

1. 遷移資產：建議使用兩種工具將資產從一個 [!DNL Experience Manager] 部署到另一個：

   * **保管庫遠程副本** 或vlt rcp ，允許您跨網路使用vlt。 您可以指定源目錄和目標目錄，vlt從一個實例下載所有儲存庫資料並將其載入到另一個實例。 Vlt rcp在 [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **格拉比特** 是時代華納電纜公司為他們開發的開源內容同步工具 [!DNL Experience Manager] 執行。 由於它使用連續資料流，因此與vlt rcp相比，它具有更低的延遲，並聲稱其速度比vlt rcp快2到10倍。 Grabbit還僅支援增量內容的同步，這允許它在完成初始遷移過程後同步更改。

1. 激活資產：按照說明 [激活資產](#activating-assets) 記錄為初始遷移到 [!DNL Experience Manager]。

1. 克隆發佈：與新遷移一樣，載入單個發佈實例並克隆它比激活兩個節點上的內容更有效。 請參閱 [克隆發佈。](#cloning-publish)

1. 啟用工作流：完成遷移後，請重新啟用 [!UICONTROL DAM更新資產] 支援格式副本生成和元資料提取的工作流，用於持續的日常系統使用。
