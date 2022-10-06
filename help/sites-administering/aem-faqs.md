---
title: AEM常見問題集
seo-title: AEM 6.4 frequently asked questions
description: 請使用這些常見問題集來了解、設定和疑難排解AEM中的常見工作流程或問題。
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

# AEM常見問題集 {#aem-faqs}

了解AEM疑難排解和設定問題的答案。

## Sites {#sites}

### 如何配置無二進位分發？ {#how-do-i-configure-binary-less-distribution}

通過共用資料儲存進行部署時支援無二進位分發，並且涉及使用基於保管庫的分發包導出器(工廠PID: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`)套件產生器。

啟用無二進位模式後，分發的內容包將包含對二進位檔的引用，而不是實際的二進位檔。

#### 如何啟用無二進位分發？ {#how-do-i-enable-binary-less-distribution}

要啟用無二進位分發，請使用共用Blob儲存區進行部署。
檢查 `useBinaryReferences` 屬性(位於OSGI設定中，且工廠PID為 `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* 你的探員用的。

#### 在AEM sites控制台中導覽頁面階層時，如何自訂錯誤訊息？ {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

檢查個人設定（JS尚未縮制）的「網路」面板（Chrome瀏覽器）。

檢視 `Initiator` 欄，以判斷請求的發起者。 它提供進行AJAX呼叫的檔案和行號。 之後，您可以追蹤錯誤處理函式，並根據需求變更錯誤訊息。

#### 如何在AEM中建立內容作者的語言副本時啟用權限？ {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

若要建立語言復本功能，內容作者需要下列位置的權限： `/content/projects` 位置。

若其中一項要求作者也管理專案，因應措施是將作者新增至 `project-administrators` 群組。

#### 如何在建立專案的語言副本時變更格式？ {#how-to-change-the-format-while-creating-language-copy-for-a-project}

在建立翻譯專案之前，先在根中建立語言根和語言副本。

例如，在建立語言根 `/content/geometrixx` 名稱為 `fr_LU` (並標題為法文（盧森堡）)。 接著，從「參考」面板建立頁面的語言副本，並導覽至 `Create structure only` 選項 `Create & Translate`. 最後，建立翻譯專案，然後將語言副本新增至翻譯工作。

如需詳細資訊，請參閱下列其他資源：

* [準備翻譯內容](/help/sites-administering/tc-prep.md)
* [管理翻譯專案](/help/sites-administering/tc-manage.md)

#### 如何稽核AEM功能，例如登入嘗試、ACL或權限變更？ {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM已導入記錄管理變更的功能，以便更妥善地進行疑難排解和稽核。 依預設，資訊會記錄在 `error.log` 檔案。 為了更方便進行監控，建議將其重新導向至單獨的日誌檔案。
若要將輸出重新導向至個別的記錄檔，請參閱 [如何在AEM中稽核使用者管理作業](/help/sites-administering/audit-user-management-operations.md).

#### 預設如何啟用SSL? {#how-to-enable-ssl-by-default}

Adobe Experience Manager(AEM)6.4隨SSL精靈提供，並提供使用者介面以設定Jetty和Granite Jetty SSL支援。

若要依預設啟用SSL，請參閱 [預設為SSL](/help/sites-administering/ssl-by-default.md).

#### 從行動應用程式使用AEM Content Services（最好是React Native）時，建議使用什麼架構？ {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

內容服務以Sling模型為基礎，AEM開發人員必須為每個已匯出的元件提供Sling模型地標。

若要了解如何從React應用程式使用AEM內容服務，請參閱 [開始使用AEM Content Services](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) 教學課程。

此外，如果開發人員想要匯出一樹狀的元件，他們也可以實作 `ComponentExporter` 和 `ContainerExporter` 介面以及使用 `ModelFactory` 迭代子元件並返回其模型表示。 請參閱下列資源：

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling ::Sling模型](https://sling.apache.org/documentation/bundles/models.html)

#### 如何停用AEM 6.4調查快顯視窗？ {#how-to-disable-aem-survey-pop-up}

您可以使用觸控式UI或Web主控台，選擇加入使用量統計資料收集。 如需詳細指示，請參閱 [選擇匯總的使用情況統計資訊收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### 是否有正確的資源，強調升級至AEM 6.4的關鍵功能？ {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

請參閱 [了解升級AEM的理由](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) 說明考慮升級至最新版Adobe Experience Manager之客戶的主要功能高階劃分。

## Assets {#assets}

### 上傳MP4檔案（例如，使用拖放方法）時，為何「資產」工作流程會重複？ {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

如果使用者上傳影片檔案在資產節點下沒有刪除權限，則刪除區塊節點會失敗，上傳會重新啟動。

#### 建立語言副本時，OOTB設定的預設設定為何？ {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

透過觸控式UI建立語言副本時(**參考** -> **更新語言副本**)，則會以新語言建立新的DAM資料夾，並從中參照資產。

這是OOTB配置的預設設定。 您可以設定 **轉換頁面資產** = **不翻譯** 在翻譯設定中。
若使用AEM 6.4, **工具** > **Cloud Services** > **翻譯雲端服務**.

#### 如何停用造成AEM SegmentStore(AEM 6.3.1.1)指數增長的AEM元件？ {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

您可以停用「OSGi元件停用」。 若要使用此服務，請參閱 [OSGi元件禁用程式](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

您也可以透過UI或 `curl` 命令（如下），在每次AEM重新啟動後。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### 如何自訂管理控制台？ {#how-to-customize-admin-consoles}

AEM提供多種機制，讓您可自訂製作例項的主控台和頁面製作功能。 若要了解如何建立自訂主控台以及自訂主控台的預設檢視，請參閱 [自訂主控台](/help/sites-developing/customizing-consoles-touch.md).

#### CoralUI 2和CoralUI 3型元件有何不同？ {#what-is-the-difference-between-coralui-and-coralui-based-components}

Granite UI Foundation的一組全新Sling元件已針對Coral3建立，位於 [/libs/granite/ui/components/coral/foundation。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) 有一組是以CoralUI 2為基礎的元件，另一組則是以CoralUI 3為基礎的元件。 新集將不只是舊集的複製貼上，而是會加以清理（例如精簡、移除已棄用的功能）。 因此，建議頁面僅使用CoralUI 3型或CoralUI 2型組。

若要深入了解，請參閱 [移轉至CoralUI 3型](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### 如何在AEM Assets中自訂搜尋元件？ {#how-to-customize-the-search-component-in-aem-assets}

若要了解搜尋提升/排名和進一步實作資訊，請參閱 [簡單搜尋實作指南](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

簡單搜尋實作是2017年Summit lab AEM Search Demystified的資料。

#### 是否可以為WordPress建立外掛程式，讓客戶存取Adobe資產選擇器以選取影像？ {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

是的，使用WordPress的Adobe可以使用AEM Assets資產選擇器從其伺服器中選擇影像，以將其添加到其WordPress網站上的帖子。

請參閱 [資產選擇器](../assets/search-assets.md#assetpicker) 以取得更多資訊。
