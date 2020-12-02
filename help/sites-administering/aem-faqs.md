---
title: AEM常見問答集
seo-title: AEM 6.4常見問題
description: 使用這些常見問答集來瞭解、設定和疑難排解AEM中的常見工作流程或問題。
seo-description: 使用這些常見問答集來瞭解、設定和疑難排解AEM中的常見工作流程或問題。
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 0%

---


# AEM常見問答{#aem-faqs}

瞭解某些AEM疑難排解和設定問題的答案。

## 網站 {#sites}

### 如何配置無二進位分發？{#how-do-i-configure-binary-less-distribution}

通過共用資料儲存進行部署時支援無二進位分發，並且涉及使用基於Vault的分發包導出器(工廠PID:`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`)套件產生器。

在啟用無二進位模式後，分發的內容封裝會包含二進位檔的參考，而非實際二進位檔。

#### 如何啟用無二進位散發？{#how-do-i-enable-binary-less-distribution}

若要啟用無二進位散發，請使用共用的blob存放區進行部署。
在OSGI配置中檢查`useBinaryReferences`屬性，並檢查您的代理使用的工廠PID(`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)*。

#### 在AEM網站主控台中導覽頁面階層時，如何自訂錯誤訊息？{#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

檢查個人設定（JS尚未微調）的「網路」面板（Chrome瀏覽器）。

檢視`Initiator`欄，以判斷請求的啟動者。 它提供進行AJAX調用的檔案和行號。 之後，您可以追蹤錯誤處理功能，並依需求變更錯誤訊息。

#### 如何在AEM中建立內容作者的語言復本時啟用權限？{#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

若要建立語言複製功能，內容作者需要`/content/projects`位置的權限。

如果作者也需要管理專案，因應措施是將作者新增至`project-administrators`群組。

#### 如何在建立專案的語言副本時變更格式？{#how-to-change-the-format-while-creating-language-copy-for-a-project}

在建立翻譯專案之前，先在根目錄中建立語言根目錄和語言副本。

例如，
在`/content/geometrixx`建立名稱為`fr_LU`的語言根目錄(標題為法文（盧森堡）)。 隨後，從參考面板建立頁面的語言副本，並導航至`Create & Translate`中的`Create structure only`選項。 最後，建立翻譯項目，然後將語言副本添加到翻譯作業。

如需詳細資訊，請參閱下列其他資源：

* [準備翻譯內容](/help/sites-administering/tc-prep.md)
* [管理翻譯專案](/help/sites-administering/tc-manage.md)

#### 如何審核AEM功能，例如登入嘗試和ACL或權限變更？{#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM已推出記錄管理變更的功能，以提供更佳的疑難排解和稽核。 預設情況下，資訊記錄在`error.log`檔案中。 為了更輕鬆地進行監控，建議將監控重新導向至個別的記錄檔。
若要將輸出重新導向至個別的記錄檔，請參閱[如何在AEM](/help/sites-administering/audit-user-management-operations.md)中檢查使用者管理作業。

#### 如何依預設啟用SSL?{#how-to-enable-ssl-by-default}

Adobe Experience Manager(AEM)6.4隨附於SSL精靈，並提供使用者介面來設定Jetty和Granite Jetty SSL支援。

若要依預設啟用SSL，請參閱[SSL依預設](/help/sites-administering/ssl-by-default.md)。

#### 從行動應用程式使用AEM的Content Services時，建議使用什麼架構，最好是React Native?{#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Content Services是以Sling Models為基礎，而AEM開發人員必須為匯出的每個元件提供Sling Model pojo。

若要瞭解如何從React應用程式使用AEM內容服務，請參閱[ AEM Content Services](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)教學課程。

此外，如果開發人員想要匯出元件樹狀結構，他們也可以實作`ComponentExporter`和`ContainerExporter`介面，並使用`ModelFactory`來重複子元件並傳回其模型表示法。 請參閱以下資源：

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling::Sling Models](https://sling.apache.org/documentation/bundles/models.html)

#### 如何停用AEM 6.4調查快顯視窗？{#how-to-disable-aem-survey-pop-up}

您可以使用Touch UI或Web Console來選擇加入使用統計資料收集。 如需詳細指示，請參閱[選擇匯總使用統計資料收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)。

#### 是否有好的資源來強調升級至AEM 6.4的主要功能？{#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

請參閱[瞭解升級AEM的理由](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html)，說明考慮升級至最新版Adobe Experience Manager之客戶的主要功能高階細分。

## 資產 {#assets}

### 上傳MP4檔案（例如使用拖放方法）時，「資產」工作流程為何會重複執行？{#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

如果使用者，上傳影片檔案在資產節點下沒有刪除權限，則刪除區塊節點會失敗，而上傳會重新啟動。

#### 一次可使用AEM 6.4操作的數位資產數目上限為何？{#what-is-the-maximum-number-of-digital-assets-that-can-be-operated-with-aem-at-a-time}

Adobe Experience Manager(AEM)6.5目前可讓您一次上傳最多2 GB的資產。

如需可搭配AEM 6.5運作的資產數目上限的詳細資訊，請參閱「資產調整指南」[。](/help/assets/assets-sizing-guide.md)

#### 建立語言副本時OOTB配置的預設設定是什麼？{#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

透過傳統UI建立語言復本時，資產不會移至新語言階層下方，而是從語言主版使用。

但是，當您透過Touch UI（**References** -> **更新語言副本**）建立語言副本時，會以新語言建立新的DAM資料夾，並從中參考資產。

這是OOTB配置的預設設定。 您可以在翻譯配置中設定&#x200B;**翻譯頁面資產** = **不翻譯**。
對於AEM 6.4,**Tools** > **Cloud Services** > **Translation Cloud服務**。

#### 如何停用造成AEM SegmentStore(AEM 6.3.1.1)指數成長的AEM元件？{#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

您可以停用OSGi元件停用程式。 要使用此服務，請參見[OSGi Component Disabler](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html)。

因應措施是，您也可以透過UI或在每次AEM重新啟動後透過`curl`命令（範例）手動停用元件。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### 如何使用AEM 6.5例項設定資產分析？{#how-to-configure-asset-insights-with-aem-instance}

若要設定並設定透過Adobe Activation(DTM)部署的Experience Manager資產前瞻分析，請參閱「如何使用AEM Assets[設定資產前瞻分析」。](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html)

#### 如何自訂管理控制台？{#how-to-customize-admin-consoles}

AEM提供多種機制，讓您自訂製作執行個體的控制台和頁面製作功能。 要瞭解如何建立自定義控制台並自定義控制台的預設視圖，請參閱[自定義控制台](/help/sites-developing/customizing-consoles-touch.md)。

#### CoralUI 2和CoralUI 3元件之間有何差異？{#what-is-the-difference-between-coralui-and-coralui-based-components}

Granite UI Foundation的一組新Sling元件是為Coral3建立，位於[/libs/granite/ui/components/coral/foundation下方。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) 其中一組是以CoralUI 2為基礎的元件，另一組是以CoralUI 3為基礎的元件。新集將不只是舊集的複製貼上，而是會加以清理（例如，簡化、移除已過時的功能）。 因此，建議頁面僅使用以CoralUI 3為基礎或以CoralUI 2為基礎的集合。

如需詳細資訊，請參閱[CoralUI 3-based](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)移轉指南。

#### 如何自訂AEM Assets中的搜尋元件？{#how-to-customize-the-search-component-in-aem-assets}

若要瞭解搜尋大幅提升／排名和進一步實作資訊，請參閱[簡易搜尋實作指南](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)。

「簡單搜尋」實作是2017年峰會實驗室AEM Search Demystified的教材。

#### AEM Assets和AEM MediaLibrary之間有何差異？{#what-is-the-difference-between-aem-assets-and-aem-medialibrary}

AEM Assets是AEM Platform上的應用程式，可讓我們的客戶在網路儲存庫中管理其數位資產（影像、視訊、檔案和音訊片段），而AEM Media Library是AEM WCM內容儲存庫的指定部分，其中影像和其他共用資源都儲存在此處。

如需詳細資訊，請參閱[AEM Assets與AEM MediaLibrary](/help/assets/medialibrary.md)。

#### 是否可建立WordPress增效模組，讓客戶存取Adobe Asset Picker以選取影像？{#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

是的，使用WordPress的客戶可以使用Adobe Asset Picker從其AEM Assets伺服器選取影像，以新增至其WordPress網站上的貼文。

如需詳細資訊，請參閱[資產選擇器](../assets/search-assets.md#assetpicker)。

#### 是否可以在AEM Assets中擴充搜尋Facet，以新增其他謂語？{#is-it-possible-to-extend-the-search-facets-in-aem-assets-to-add-additional-predicates}

Adobe Experience Manager(AEM)Assets的企業部署可儲存許多資產。 您可以新增謂語至預設表單，或使用包含您選擇之刻面的自訂表單。

請參閱[搜尋Facets](/help/assets/search-facets.md)以瞭解更多資訊。
