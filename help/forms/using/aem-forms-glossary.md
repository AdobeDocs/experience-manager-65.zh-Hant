---
title: AEM Forms字彙表
description: AEM Forms字彙表提供Adobe Experience Manager Forms (AEM Forms)中使用之重要辭彙、定義和概念的完整清單，協助使用者瞭解並使用調適型表單和相關功能。
feature: Adaptive Forms
role: Admin, User, Developer
hidefromtoc: true
hide: true
source-git-commit: 37f471e09c13b7ab036ab1043d11dfed98da1d97
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 1%

---

# AEM Forms字彙表

## [調適型表單](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form)

動態、回應式表單，可根據使用者的裝置和輸入調整版面和簡報，提升各種平台的使用者體驗。 包括條件式邏輯、動態資料繫結和規則型行為。

## [最適化表單版本設定](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/adaptive-forms-core-components/add-versioning-reviews-comments)

能夠使用JCR節點版本設定來管理存放庫中的多個表單版本。 確保稽核軌跡以及最適化表單的輕鬆回覆。

## [Adobe Analytics Forms整合](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation)

透過Adobe Analytics提供使用者互動（例如欄位流失、每個區段逗留時間）的詳細分析，以啟用資料導向的表單設計最佳化。

## [AEM Forms附加元件套件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi)

以套件形式部署至Adobe Experience Manager (AEM)的應用程式，包含由AEM Sling架構管理的服務（API提供者）和servlet或JSP。

## [JEE上的AEM Forms](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)

AEM Forms的部署選項，可運用Java Enterprise Edition (JEE)伺服器，提供企業級擴充性、交易管理，以及複雜企業工作流程的支援。

## [上的AEM Forms OSGi](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/deploying/introduction/technical-requirements)

OSGi環境上的AEM Forms是標準的AEM Author或部署了AEM Forms套件的AEM Publish 。 您可以在單一伺服器環境、伺服陣列和叢集設定中，在OSGi上執行AEM Forms。 叢集設定僅適用於AEM編寫執行個體。

## [AEM Forms中的Adobe Sign](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms)

RESTful服務，提供安全無縫的數位簽名工作流程。 它使用OAuth型驗證與AEM Forms整合，實現自動簽名收集和即時追蹤。

## [AEM Forms Document Services 6.5](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services)

AEM Forms網頁層提供的API，供HTTP型使用者端遠端使用，例如行動SDK表單。AEM Forms中的功能，可建立、組裝、散發及封存PDF檔案、新增數位簽章，以及解碼條碼Forms。

| **服務名稱** | **說明** | **檔案連結** |
|------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Forms 服務** | 使用範本和XML呈現PDF forms、整合表單資料以供匯入/匯出，以及支援以片段為基礎的呈現。 | [Forms服務檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **輸出服務** | 透過將資料與PDF、PCL或PostScript等格式的範本合併來產生檔案。 | [輸出服務檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **組合器服務** | 合併、重新排列、驗證及增加PDF和XDP檔案。 | [組合器服務檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/use-document-services/assembler-service) |
| **ConvertPDF服務** | 將PDF檔案轉換為PostScript或PNG、JPEG或TIFF等影像格式。 | [ConvertPDF服務檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/use-document-services/using-convertpdf-service) |
| **條碼式Forms服務** | 從TIFF和PDF檔案中的條碼擷取資料，以自動化資料擷取程式。 | [條碼式Forms服務檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/use-document-services/using-barcoded-forms-service) |
| **DocAssurance服務** | 加密、解密、數位簽署和套用PDF的檔案安全性原則。 | [DocAssurance服務檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services#doc-assurance-service) |
| **PDF Generator服務** | 將原生檔案格式(例如：Microsoft Word、Excel)轉換為PDF檔案。 | [PDF Generator服務檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/use-document-services/aem-document-services-programmatically#pdfgeneratorservice) |

## [Formsas a Cloud Service通訊API](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction)

AEM Formsas a Cloud Service提供管理表單和通訊工作流程的進階工具，支援無縫數位表單建立、資料擷取和個人化通訊。 雲端通訊API可透過HTTP提供安全的隨選和批次檔案產生、操作、驗證以及與外部系統的整合，以確保簡化和安全作業。

| **服務名稱** | **說明** | **檔案連結** |
|-------------------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **檔案產生** | 將範本(XFA或PDF)與XML資料結合，以產生PDF和列印格式（如PS、PCL、DPL、IPL和ZPL格式）的檔案。 | [檔案產生檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=zh-Hant#document-generation) |
| **檔案操作** | 組合、重新排列PDF檔案。 | [檔案操作檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation) |
| **檔案轉換** | 將PDF轉換為PDF/A並檢查PDF/A合規性。 | [檔案轉換檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-conversion) |
| **檔案Assurance** | 新增或移除簽名欄位、簽署、認證、加密、解密並套用使用許可權至PDF檔案。 | [檔案Assurance檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#doc-assurance) |
| **數位簽章** | 整合Adobe Sign以安全地簽署表單和檔案。 | [數位簽章檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=zh-Hant#digital-signatures) |


## [AEM Forms Workbench](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/install-workbench)

適用於建立、編輯和部署工作流程，以及管理以表單為中心的業務流程的案頭應用程式。 它提供與後端服務與系統的整合。

## [原型](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/developing/archetype/overview)

AEM中的範本或模式，用於產生具有預先定義結構的新專案，有助於標準化、快速設定和遵守AEM開發最佳實務。

## [作者執行個體](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

內容建立者和管理員在發佈內容前設計、建立和管理內容的環境。 支援版本設定、預覽和測試。

## [製作前端](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

在AEM Forms中製作和管理表單的使用者介面。

## [最適化表單區塊](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-references/form-components)

一種封裝單元，可在邏輯上將相關元件和中繼資料分組，以多步驟表單進行動態資料處理和輕鬆擴充。

## [核心元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/introduction)

現成可重複使用的建置區塊，可用於建立表單，包括表單欄位、版面容器、按鈕和其他互動式元素。

## [通信管理](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/letters-correspondences/cm-overview)

此模組可讓企業使用預先定義的範本、規則和資料來源來建立、管理和提供個人化通訊。 包括信件範本、客戶通訊和批次產生。

## [CRX (Content repository extreme)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/use-aem-forms-workspace/html-workspace-architecture)

AEM中的內建Java Content Repository (JCR)，可儲存結構化和非結構化資料，實現內容、範本和設定的階層式儲存。

## [自訂元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/customize-adaptive-forms-core-components)

延伸AEM Forms功能的定製元件，使用Sling模型、Sightly (HTL)和Java開發。 通常用於唯一的業務邏輯或進階使用者端互動。

## [自訂XCI （XML組態資訊）](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/administrator-help/configure-forms/specifying-xci-configuration-options)

在Adobe Experience Manager (AEM) Forms中，自訂XCI （XML設定資訊）檔案可讓管理員定義表單與檔案的特定轉譯屬性。 透過在管理控制檯中設定XCI設定，您可以使用自訂選項覆寫系統預設值，確保量身定製的處理和表單呈現。

## [資料整合](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/form-data-model/data-integration)

將外部資料來源（例如資料庫、網站服務或REST API）緊密整合至表單和工作流程，以啟用動態和個人化的使用者體驗。

## [資料來源](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/form-data-model/configure-data-sources)

用於將外部資料整合至表單的介面，包括關聯式資料庫的JDBC、Web服務的REST端點，以及SAP系統的OData。 透過AEM Forms資料整合框架管理。

## [檔案片段](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/letters-correspondences/lists)

可重複使用的檔案元件，例如頁首、頁尾、免責宣告或條款，這些元件可動態地包含在表單或通訊中，以確保一致性。

## [記錄檔案(DoR)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms)

AEM Forms中的功能，可產生不可編輯的已提交表單封存版本(通常為PDF格式)，保留精確的內容和版面作為交易記錄。

## [Edge Delivery Services](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/overview)

針對AEM Forms最佳化內容傳送，確保減少表單、主題和使用者端資料庫等資產的延遲，以供作者快速更新及發佈內容。

## [Forms整合](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/form-data-model/data-integration)

涉及使用OSGi套件組合和聯結器將AEM Forms連線至企業系統(例如SAP、Salesforce)，支援雙向資料流程和即時更新。

## [表單檢閱](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms)

工作流程導向功能，可讓利害關係人在發佈前檢閱最適化表單、新增註解及核准變更。 使用AEM收件匣和任務管理。

## [表單資料模型(FDM)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model)

一種表現層，可將最適化表單連線至後端資料來源，藉此實現與RESTful Web服務、SOAP服務和OData的整合。 FDM可讓表單作者將表單欄位直接對應到後端資料結構，確保使用者輸入與外部系統無縫同步。

## [表單本地化](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization)

最適化表單的程式，可支援多種語言和區域設定，確保不同受眾可存取表單且方便使用。

## [表單入口網站](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/use-forms-portal/creating-form-portal-page)

Forms Portal元件為Web開發人員提供元件，以便在使用Forms (AEM)編寫的網站上建立和自訂Adobe Experience Manager Portal。 它可讓使用者在網頁和行動平台上有效率地探索、存取及提交表單。

## [表單轉譯與提交前端](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

AEM Forms的一般使用者介面，可讓使用者透過網頁瀏覽器檢視及提交表單。

## [表單集](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/html5-forms/formset-in-aem-forms)

將相關表單集合在一起，以單一實體形式呈現給使用者，以便將複雜的資料收集程式細分為可管理的區段。

## [Forms Designer](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/using-communications/installing-configuring-designer)

獨立的應用程式，用來設計XDP表單的表單範本，並在AEM Forms中使用它來產生記錄檔案。

## [以Forms為中心的工作流程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow)

AEM Forms中一組管理業務流程的自動化或手動步驟，例如檔案核准、內容發佈或使用者通知。

## [互動式通訊](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/getting-started/interactive-communications-overview)

用於管理高度個人化的多頻道通訊的自訂實施。 它結合來自各種來源（例如CRM或ERP系統）的資料，以跨格式（例如Web、行動裝置、電子郵件和列印）傳遞通訊。

## [JCR （Java內容存放庫）](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr)

階層式、標準型存放庫，可在AEM中儲存內容、設定和中繼資料，支援結構化和非結構化資料儲存。

## [個字母](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/letters-correspondences/create-letter#create-a-letter-template)

利用AEM Forms檔案服務產生客戶通訊。 信件是使用XDP範本、資料模型和可重複使用的片段組合所建立，以確保在高容量情況下可擴充性。

## [AEM Forms中的中繼資料](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/manage-administer-aem-forms/manage-form-metadata)

中繼資料可讓您有效率地分類及擷取資產。 AEM Forms包含每種資產型別的預先定義中繼資料，並可進行自訂。 它還提供工具，讓您順暢地建立、管理和交換中繼資料。

## [PDF Generator](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/forms/document-services/using-pdfg-in-aem-forms)

AEM Forms中的一種工具，可將各種檔案格式（例如：Word、Excel、PowerPoint）轉換為PDF檔案，並提供加密、浮水印和合併等功能。

## [Publish執行個體](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

AEM中向一般使用者提供即時內容的環境。 它以最佳化的效能提供表單、頁面和其他數位體驗。

## [規則編輯器](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components)

最適化Forms中的視覺化工具，可讓作者定義表單欄位的自訂規則和邏輯，例如可見度、驗證和資料預先填入，而不需要編碼專業知識。

## [草寫簽章](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble)

AEM Forms中的一項功能，可讓使用者使用滑鼠或觸控式裝置，直接在表單上繪製簽名，以電子方式簽署表單。

## [在AEM Forms中提交動作](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/configuring-submit-actions)

在表單提交時執行的伺服器端或使用者端動作。 例如REST API呼叫、叫用工作流程，或將資料寫入JCR （Java內容存放庫）。

## [主題](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components)

CSS導向的樣式架構已套用至調適型表單，將LESS/SASS用於前置處理器。 主題可確保符合品牌指南與協助工具標準，您可以自訂主題、變更其設計元素、版面、顏色、印刷樣式，有時甚至是基礎程式碼。

## [範本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components)

調適型表單的藍圖包含結構元素（欄位、版面）和預先設定的指令碼，您可以建立和自訂新範本，或使用現有的現成範本。

## [網頁層](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

包含建置在通用和表單服務上的JSP或servlet，提供製作前端、表單轉譯和提交前端及REST API等功能。

## [XDP （XML資料封裝）](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/manage-administer-aem-forms/get-xdp-pdf-documents-aem)

AEM Forms中使用的一種檔案格式，用於設計和建構表單，可支援動態內容和互動時，以PDF或HTML的形式呈現。

## [XFA (XML Forms架構)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-an-xfa-form-template)

建立互動式與動態PDF forms的舊版技術。 XFA表單可提供進階功能，例如動態版面調整、指令碼以及與後端系統的緊密整合。

## [XML或JSON結構描述](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-xml-or-json-schema)

標準化結構，用來定義表單和工作流程中XML或JSON資料的格式和組織。 這些架構可確保一致的資料處理，並實現與外部系統的互通性。

<!--

## **Custom Properties**  

Developer-defined metadata attributes added to components or forms for advanced behaviors, accessed via Sling APIs or Groovy scripts for dynamic processing.

## **Embedding** 

Integrating adaptive forms into AEM Sites or external web pages using `<iframe>` or SPA (Single Page Application) models. Embedding supports seamless session handling and cross-origin resource sharing (CORS).

## **CDN (Content Delivery Network)**  

Distributed networks (e.g., Akamai) used for caching and delivering forms-related resources, ensuring high availability and faster load times for geographically distributed users.


## **Dispatcher**  

An AEM caching and load balancing tool configured to optimize delivery of adaptive forms. Its filter rules ensure secure access control while caching frequently accessed forms and assets.

## **Editors**  

Tools like the Adaptive Forms Editor, Theme Editor, and Rule Editor, enabling developers and content authors to customize forms and their behavior without extensive coding.

## **Responsive UI**  

An implementation of media queries and flexible grids, ensuring adaptive forms render seamlessly across various screen sizes and devices.

## **Custom Functions**  

JavaScript-based utilities or REST microservices that provide additional logic (e.g., complex field validation or data pre-population), extending the out-of-the-box capabilities of AEM Forms.

## **Package Manager**  

AEM's CRX Package Manager facilitates importing/exporting adaptive forms, data schemas, or configurations as .zip files, enabling modular deployment in distributed environments.

## **UE (User Experience)**  

Design principles and optimizations applied in AEM Forms to enhance usability, including accessibility features (ARIA roles, tab navigation) and intuitive layouts.

## **Forms Submission Services**

Back-end services for handling form submissions, integrating with the AEM Workflow engine, third-party APIs, or direct JCR persistence.


Foundation components
e-signing
adobe sign
letters
submit action
data sources
adaptive form block
edge delivery services
forms integration
custom component 
themes
template 
custom properties
embedding
CDN
Dispatcher
editors
responsive UI
custom functions
package manager
communication APIs
UE
Forms submission services
Form review
Forms Versioning
Adobe analytics forms integration specific

## **AEM Forms Foundation Components**  
Core reusable elements within AEM Forms, built on Granite UI, enabling developers to create complex forms. They provide robust features like data bindings, field validations, and support for multilingual content.


## **e-Signing**  
An implementation of digital signature standards (e.g., PKCS #7) within AEM Forms, integrated with Adobe Sign APIs to ensure secure and legally binding electronic signatures.

## Workspace

A browser-based interface for users to interact with AEM Forms workflows, tasks, and approvals.

## Sling

A REST-based web framework used in AEM to map request URLs to content resources, enabling efficient content rendering and delivery.

-->
