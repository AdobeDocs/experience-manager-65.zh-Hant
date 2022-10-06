---
title: 支援最適化表單本地化的新地區設定
seo-title: Supporting new locales for adaptive forms localization
description: AEM Forms可讓您新增當地語系化最適化表單的地區設定。 預設情況下，支援的地區設定是英文、法文、德文和日文。
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. The supported locales by default are English, French, German, and Japanese.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
feature: Adaptive Forms
role: Admin
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# 支援最適化表單本地化的新地區設定{#supporting-new-locales-for-adaptive-forms-localization}

## 關於語言環境字典 {#about-locale-dictionaries}

最適化表單的本地化需要兩種語言環境字典：

**表單特定字典** 包含適用性表單中使用的字串。 例如，標籤、欄位名稱、錯誤訊息、說明說明等。 它作為一組XLIFF檔案來管理，用於每個區域設定，您可以在 `https://<host>:<port>/libs/cq/i18n/translator.html`.

**全域字典** AEM用戶端程式庫中有兩本全域字典，以JSON物件管理。 這些字典包含預設錯誤訊息、月份名稱、貨幣符號、日期和時間模式等。 您可以在CRXDe Lite中找到這些字典，網址為/libs/fd/xfaforms/clientlibs/I18N。 這些位置包含每個區域設定的單獨資料夾。 由於全域字典通常不會經常更新，因此為每個區域設定保留個別的JavaScript檔案，可讓瀏覽器快取，並減少在同一伺服器上存取不同最適化表單時的網路頻寬使用。

### 最適化表單的本地化運作方式 {#how-localization-of-adaptive-form-works}

有兩種方法可識別最適化表單的地區設定。 呈現最適化表單時，會依以下項目識別要求的地區設定：

* 看 `[local]` 最適化表單URL中的選取器。 URL的格式為 `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`. 使用 `[local]` 選取器允許快取最適化表單。

* 以指定順序查看下列參數：

   * 要求參數 `afAcceptLang`
若要覆寫使用者的瀏覽器地區設定，您可以傳遞 
`afAcceptLang` 要求參數以強制地區設定。 例如，下列URL將強制以日文地區來轉譯表單：
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * 為使用者設定的瀏覽器地區設定，使用 `Accept-Language` 頁首。

   * 在AEM中指定之使用者的語言設定。

   * 預設會啟用瀏覽器地區設定。 要更改瀏覽器區域設定，
      * 開啟配置管理器。 URL為 `http://[server]:[port]/system/console/configMgr`
      * 找出並開啟 **[!UICONTROL 最適化表單與互動式通訊Web通道]** 設定。
      * 變更 **[!UICONTROL 使用瀏覽器地區]** 選項和  **[!UICONTROL 儲存]** 設定。

識別地區設定後，適用性表單會挑選表單特定字典。 如果找不到所請求地區的表單特定字典，則會針對製作最適化表單的語言使用字典。

如果沒有地區設定資訊，則會以表單的原始語言傳送最適化表單。 原始語言是開發最適化表單時使用的語言。

如果所請求區域的客戶端庫不存在，則它檢查客戶端庫中是否存在語言代碼。 例如，如果請求的區域設定為 `en_ZA` （南非英語）和 `en_ZA` 不存在，適用性表單將使用的用戶端程式庫 `en` （英語）語言（如果存在）。 不過，如果兩者皆不存在，適用性表單會將字典用於 `en` 地區。

## 添加對不支援的語言環境的本地化支援 {#add-localization-support-for-non-supported-locales}

AEM Forms目前支援以英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)語言環境本地化最適化表單內容。

若要在適用性表單執行階段新增對新地區設定的支援：

1. [向GuideLocalizationService服務添加區域設定](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [為地區設定新增XFA用戶端程式庫](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [為區域設定新增最適化表單用戶端程式庫](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [為字典添加地區支援](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [重新啟動伺服器](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 向指南本地化服務添加區域設定 {#add-a-locale-to-the-guide-localization-service-br}

1. 前往 `https://'[server]:[port]'/system/console/configMgr`.
1. 按一下以編輯 **指南本地化服務** 元件。
1. 將要添加的區域設定添加到支援的區域設定清單中。

![指南本地化服務](assets/configservice.png)

### 為地區設定新增XFA用戶端程式庫 {#add-xfa-client-library-for-a-locale-br}

建立類型的節點 `cq:ClientLibraryFolder` 在 `etc/<folderHierarchy>`，包含類別 `xfaforms.I18N.<locale>`，並將下列檔案新增至用戶端程式庫：

* **I18N.js** 定義 `xfalib.locale.Strings` 針對 `<locale>` 定義 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** 包含下列項目：

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 為區域設定新增最適化表單用戶端程式庫 {#add-adaptive-form-client-library-for-a-locale-br}

建立類型的節點 `cq:ClientLibraryFolder` 在 `etc/<folderHierarchy>`，類別為 `guides.I18N.<locale>` 和依賴項 `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` 和 `guide.common`.&quot;

將以下檔案添加到客戶端庫：

* **i18n.js** 定義 `guidelib.i18n`，具有「日曆符號」的模式， `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` 針對 `<locale>` 根據 [地區設定規範](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf). 您也可以看到，如何針對 `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** 定義 `guidelib.i18n.strings` 和 `guidelib.i18n.LogMessages` 針對 `<locale>` 定義 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** 包含下列項目：

```text
i18n.js
LogMessages.js
```

### 為字典添加地區支援 {#add-locale-support-for-the-dictionary-br}

只有在 `<locale>` 您添加的不在 `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. 建立 `nt:unstructured` 節點 `languages` 在 `etc`，如果尚未存在。

1. 新增多值字串屬性 `languages` 至節點（如果尚未存在）。
1. 新增 `<locale>` 預設地區值 `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`，如果尚未存在。

1. 新增 `<locale>` 的值 `languages` 屬性 `/etc/languages`.

此 `<locale>` 將顯示於 `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### 重新啟動伺服器 {#restart-the-server}

重新啟動AEM伺服器，讓新增的地區設定生效。

## 新增西班牙文支援的范常式式庫 {#sample-libraries-for-adding-support-for-spanish}

新增西班牙文支援的用戶端程式庫範例

[取得檔案](assets/sample.zip)
