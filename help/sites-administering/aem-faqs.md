---
title: 常見問AEM題
seo-title: AEM 6.4 frequently asked questions
description: 使用這些常見問題瞭解、配置和排除中的常見工作流或問題AEM。
seo-description: Use these FAQs to understand, configure, and troubleshoot common workflows or issues in AEM.
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---

# 常見問AEM題 {#aem-faqs}

瞭解一些故障排AEM除和配置問題的答案。

## Sites {#sites}

### 如何配置無二進位分發？ {#how-do-i-configure-binary-less-distribution}

通過共用資料儲存部署支援無二進位分發，並且涉及使用基於Vault的分發包導出器(工廠PID: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`)包生成器。

啟用無二進位模式後，分發的內容包包含對二進位檔案的引用，而不是實際二進位檔案。

#### 如何啟用無二進位分發？ {#how-do-i-enable-binary-less-distribution}

要啟用無二進位分發，請使用共用Blob儲存區進行部署。
檢查 `useBinaryReferences` OSGI配置中的屬性( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* 你的探員在用的。

#### 如何在站點控制台中導航頁面層次結構時自定義AEM錯誤消息？ {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

檢查個人設定（JS尚未微型化）的「Network（網路）」面板（Chrome瀏覽器）。

查看 `Initiator` 列以確定請求的啟動器。 它提供從中進行呼叫的檔案和AJAX行號。 稍後，您可以跟蹤錯誤處理功能並根據需要更改錯誤消息。

#### 如何在中為內容作者建立語言副本時啟用權AEM限？ {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

要建立語言複製功能，內容作者需要在 `/content/projects` 位置。

如果您要求作者也管理項目，則解決方法是將作者添加到 `project-administrators` 組。

#### 如何在為項目建立語言副本時更改格式？ {#how-to-change-the-format-while-creating-language-copy-for-a-project}

在建立翻譯項目之前，在根內建立語言根和語言副本。

例如，在 `/content/geometrixx` 名稱為 `fr_LU` (並稱法語（盧森堡）)。 隨後，從「參考」面板建立頁面的語言副本並導航至 `Create structure only` 選項 `Create & Translate`。 最後，建立翻譯項目，然後將語言副本添加到翻譯作業。

有關詳細資訊，請參閱以下附加資源：

* [準備翻譯內容](/help/sites-administering/tc-prep.md)
* [管理翻譯項目](/help/sites-administering/tc-manage.md)

#### 如何審AEM核權能，如登錄嘗試和ACL或權限更改？ {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM引入了記錄管理更改的功能，以便更好地進行故障排除和審核。 預設情況下，資訊將記錄在 `error.log` 的子菜單。 為了使監控更輕鬆，建議將它們重定向到單獨的日誌檔案。
要將輸出重定向到單獨的日誌檔案，請參見 [如何審核中的用戶管理操AEM作](/help/sites-administering/audit-user-management-operations.md)。

#### 預設情況下如何啟用SSL? {#how-to-enable-ssl-by-default}

Adobe Experience Manager(AEM)6.4附帶SSL嚮導，並提供一個用戶介面來配置Jetty和Granite Jetty SSL支援。

要預設啟用SSL，請參見 [預設情況下為SSL](/help/sites-administering/ssl-by-default.md)。

#### 使用移動應用中的內容服AEM務時，建議使用什麼體系結構？ {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

內容服務基於Sling模型，開發人AEM員必須為導出的每個元件提供Sling模型程式。

要瞭解如何從React應AEM用程式使用內容服務，請參見 [開始使用AEMContent Services](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) 教程。

此外，如果開發人員希望導出元件樹，他們也可以實施 `ComponentExporter` 和 `ContainerExporter` 介面以及使用 `ModelFactory` 迭代子元件並返回其模型表示。 請參閱以下資源：

[1] [Adobe — 營銷 — 雲/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling ::吊具模型](https://sling.apache.org/documentation/bundles/models.html)

#### 如何禁AEM用6.4調查彈出窗口？ {#how-to-disable-aem-survey-pop-up}

您可以選擇使用「Touch UI」或「Web控制台」來收集使用情況統計資訊。 有關詳細說明，請參見 [選擇聚合使用情況統計資訊收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)。

#### 是否有一個好的資源突出了升級到AEM6.4的關鍵功能？ {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

請參閱 [瞭解升級的理AEM由](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) 描述了考慮升級到最新版Adobe Experience Manager的客戶的關鍵功能的高級細分。

## Assets {#assets}

### 為什麼在上載MP4檔案（例如，使用拖放方法）時資產工作流會重複？ {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

如果用戶在資產節點下上載影片檔案沒有刪除權限，則刪除區塊節點將失敗，並且上載將重新啟動。

#### 建立語言副本時OOTB配置的預設設定是什麼？ {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

通過Touch UI建立語言副本時(**引用** -> **更新語言副本**)，在新語言下建立新的DAM資料夾，並從中引用資產。

這是OOTB配置的預設設定。 可以設定 **翻譯頁面資產** = **不翻譯** 在翻譯配置中。
為AEM6.4, **工具** > **Cloud Services** > **翻譯雲服務**。

#### 如何禁用導AEM致SegmentStore(AEM6.3.1.1)指AEM數增長的元件？ {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

可以禁用OSGi元件禁用程式。 要使用此服務，請參閱 [OSGi元件禁用程式](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html)。

作為解決方法，您還可以通過UI或通過 `curl` 命令（下例），每次重新啟AEM動後。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### 如何自定義管理控制台？ {#how-to-customize-admin-consoles}

提AEM供各種機制，使您能夠自定義創作實例的控制台和頁面創作功能。 要瞭解如何建立自定義控制台並自定義控制台的預設視圖，請參閱 [自定義控制台](/help/sites-developing/customizing-consoles-touch.md)。

#### 基於CoralUI 2和CoralUI 3的元件有何區別？ {#what-is-the-difference-between-coralui-and-coralui-based-components}

為Coral3建立了Granite UI基金會的一組新Sling元件，位於 [/libs/granite/ui/components/coral/foundation。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) 有一組用於基於CoralUI 2的元件，另一組用於基於CoralUI 3的元件。 新集將不僅是舊集的複製貼上，而是將對其進行清理（例如，簡化、刪除不建議使用的功能）。 因此，建議頁面只使用基於CoralUI 3或基於CoralUI 2的集。

要瞭解更多詳細資訊，請參閱 [遷移指南 — 基於CoralUI 3](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)。

#### 如何在AEM Assets自定義搜索元件？ {#how-to-customize-the-search-component-in-aem-assets}

要瞭解有關搜索提升/排名和進一步實施資訊，請參閱 [簡單搜索實現指南](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)。

簡單搜索實現是2017年Summit實驗室搜索已解密AEM的材料。

#### 是否可以為WordPress構建插件，允許客戶訪問Adobe資產選取器以選擇映像？ {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

是的，使用WordPress的客戶可以使用Adobe資產選取器從其AEM Assets伺服器中選擇影像以添加到其WordPress站點上的帖子。

請參閱 [資產選擇器](../assets/search-assets.md#assetpicker) 的子菜單。
