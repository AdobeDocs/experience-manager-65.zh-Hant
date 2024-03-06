---
title: AEM常見問題集
description: 使用這些常見問題集來瞭解、設定和疑難排解AEM中的常見工作流程或問題。
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---

# AEM常見問題集 {#aem-faqs}

瞭解部分AEM疑難排解和設定問題的答案。

## Sites {#sites}

### 如何設定無二進位檔的分發？ {#how-do-i-configure-binary-less-distribution}

透過共用資料存放區進行部署時，支援無二進位分送，而且其中會涉及使用儲存庫型散發套件匯出程式(原廠PID： `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`)封裝產生器。

啟用無二進位模式後，發佈的內容套件會包含對二進位檔的參照，而不是實際的二進位檔。

#### 如何啟用無二進位分送？ {#how-do-i-enable-binary-less-distribution}

若要啟用無二進位檔的分發，請使用共用的blob存放區進行部署。
檢查 `useBinaryReferences` OSGI設定中的屬性，具有原廠PID ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* 您的代理程式正在使用。

#### 如何在AEM中為內容作者建立語言副本時啟用許可權？ {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

若要建立語言複製功能，內容作者需要下列許可權： `/content/projects` 位置。

如果這也需要作者管理專案，解決方法是將作者新增到 `projects-administrators` 群組。

#### 在建立專案的語言副本時，如何變更格式？ {#how-to-change-the-format-while-creating-language-copy-for-a-project}

在建立翻譯專案之前，請先在根內建立語言根和語言副本。

例如，在下列位置建立語言根： `/content/geometrixx` 名稱為 `fr_LU` (法文（盧森堡）)。 接著，從「參考」面板建立頁面的語言副本，並導覽至 `Create structure only` 中的選項 `Create & Translate`. 最後，建立翻譯專案，然後將語言副本新增至翻譯工作。

如需詳細資訊，請參閱下列其他資源：

* [準備翻譯內容](/help/sites-administering/tc-prep.md)
* [管理翻譯專案](/help/sites-administering/tc-manage.md)

#### 如何稽核AEM功能，例如，登入嘗試以及ACL或許可權變更？ {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM已引入記錄管理變更的功能，以便進行更好的疑難排解和稽核。 依預設，資訊會記錄在 `error.log` 檔案。 為了更輕鬆地進行監視，建議將它們重新導向到單獨的記錄檔。
若要將輸出重新導向至個別的記錄檔，請參閱 [如何在AEM中稽核使用者管理作業](/help/sites-administering/audit-user-management-operations.md).

#### 如何預設啟用SSL？ {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4隨附SSL精靈，並提供使用者介面以設定Jetty和Granite Jetty SSL支援。

若要依預設啟用SSL，請參閱 [SSL預設值](/help/sites-administering/ssl-by-default.md).

#### 從行動應用程式（最好是React Native）使用AEM Content Services時，建議使用什麼架構？ {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

內容服務以Sling模型為基礎，AEM開發人員必須為匯出的每個元件提供Sling模型pojo。

若要瞭解如何從React應用程式使用AEM內容服務，請參閱 [開始使用AEM內容服務](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) 教學課程。

此外，如果開發人員想要匯出元件的樹狀結構，也可以實作 `ComponentExporter` 和 `ContainerExporter` 介面並使用 `ModelFactory` 反複子元件並傳回其模型表示。 請參閱下列資源：

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling ：： Sling模型](https://sling.apache.org/documentation/bundles/models.html)

#### 如何停用AEM 6.4意見調查快顯視窗？ {#how-to-disable-aem-survey-pop-up}

您可以使用Touch UI或Web Console來選擇使用狀況統計資料的收集。 如需詳細指示，請參閱 [選擇加入彙總的使用狀況統計資料的收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### 是否有重點說明要升級至AEM 6.4的主要功能的有用資源？ {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

另請參閱 [瞭解升級AEM的原因](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) 說明考慮升級至最新版Adobe Experience Manager之客戶的主要功能概要說明。

## Assets {#assets}

### 為何上傳MP4檔案時（例如使用拖放方法）「資產」工作流程會自我重複？ {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

如果使用者上傳影片檔案時沒有資產節點底下的刪除許可權，則刪除區塊節點會失敗，而上傳會重新啟動。

#### 建立語言副本時，現成設定的預設設定為何？ {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

當您透過Touch UI建立語言副本時(**引用** > **更新語言副本**)，則會以新語言建立新的DAM資料夾，並從中參考資產。

這是現成組態的預設設定。 您可以設定 **翻譯頁面資產** = **不翻譯** 位於翻譯設定中。
對於AEM 6.4， **工具** > **Cloud Service** > **翻譯雲端服務**.

#### 如何停用造成AEM SegmentStore (AEM 6.3.1.1)呈指數式增長的AEM元件？ {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

您可以停用OSGi元件停用程式。 若要使用此服務，請參閱 [OSGi元件停用器](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

暫行解決方法是您也可以透過UI或透過手動停用元件。 `curl` 命令（如下所示），在每次重新啟動AEM之後。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### 如何自訂Admin Console？ {#how-to-customize-admin-consoles}

AEM提供各種機制，讓您能夠自訂編寫執行個體的主控台和頁面編寫功能。 若要瞭解如何建立自訂主控台及自訂主控台的預設檢視，請參閱 [自訂主控台](/help/sites-developing/customizing-consoles-touch.md).

#### CoralUI 2和CoralUI 3型元件有何不同？ {#what-is-the-difference-between-coralui-and-coralui-based-components}

系統會為Coral3建立一組新的Granite UI Foundation Sling元件，其位於 [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) 一組適用於CoralUI 2元件，另一組適用於CoralUI 3元件。 新集合不會只是複製貼上舊集合，而是會加以清除（例如，精簡、移除已棄用的功能）。 因此，建議頁面僅使用以CoralUI 3為基礎或以CoralUI 2為基礎的組合。

若要深入瞭解，請參閱 [CoralUI 3型移轉指南](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### 如何在AEM Assets中自訂搜尋元件？ {#how-to-customize-the-search-component-in-aem-assets}

若要瞭解搜尋提升/排名和進一步實作資訊，請參閱 [簡易搜尋實作指南](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

簡單搜尋實作是來自2017 Summit lab AEM Search Demystified的資料。

#### 是否能夠建置WordPress的外掛程式，讓客戶存取Adobe資產選擇器以選取影像？ {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

可以，使用WordPress的客戶可以使用Adobe資產選擇器，從其AEM Assets伺服器選取影像，以新增至其WordPress網站上的貼文。

請參閱 [資產選擇器](../assets/search-assets.md#assetpicker) 以取得詳細資訊。
