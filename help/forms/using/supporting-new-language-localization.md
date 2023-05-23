---
title: 支援新語言環境以實現自適應表單本地化
seo-title: Supporting new locales for adaptive forms localization
description: AEM Forms允許您添加新區域設定來本地化自適應表單。 預設情況下，支援的語言環境為英語、法語、德語和日語。
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

# 支援新語言環境以實現自適應表單本地化{#supporting-new-locales-for-adaptive-forms-localization}

## 關於區域設定詞典 {#about-locale-dictionaries}

自適應表單的本地化依賴於兩種語言環境詞典：

**表單特定詞典** 包含自適應表單中使用的字串。 例如，標籤、欄位名、錯誤消息、幫助說明等。 它作為一組XLIFF檔案管理，用於每個區域設定，您可以在 `https://<host>:<port>/libs/cq/i18n/translator.html`。

**全局詞典** 客戶端庫中有兩個全局字典，作為JSON對象AEM管理。 這些詞典包含預設錯誤消息、月名、貨幣符號、日期和時間模式等。 您可以在CRXDe Lite中找到這些詞典，地址為/libs/fd/xfaforms/clientlibs/I18N。 這些位置包含每個區域設定的單獨資料夾。 由於全局詞典通常不會頻繁更新，因此為每個區域設定保留單獨的JavaScript檔案使瀏覽器能夠快取它們，並減少訪問同一伺服器上不同自適應表單時的網路頻寬使用。

### 自適應表單的定位 {#how-localization-of-adaptive-form-works}

有兩種方法來標識自適應表單的區域設定。 在呈現自適應表單時，它通過以下方式標識所請求的區域設定：

* 看著 `[local]` 的子菜單。 URL的格式為 `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`。 使用 `[local]` 選擇器允許快取自適應窗體。

* 按指定順序查看以下參數：

   * 請求參數 `afAcceptLang`
要覆蓋用戶的瀏覽器區域設定，可以通過 
`afAcceptLang` 請求參數以強制區域設定。 例如，以下URL將強制以日文區域設定呈現表單：
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * 用戶的瀏覽器區域設定，該設定在請求中使用 `Accept-Language` 標題。

   * 中指定的用戶的語言設AEM置。

   * 預設情況下，瀏覽器區域設定處於啟用狀態。 要更改瀏覽器區域設定，
      * 開啟配置管理器。 URL為 `http://[server]:[port]/system/console/configMgr`
      * 查找並開啟 **[!UICONTROL 自適應形式與交互通信Web通道]** 配置。
      * 更改 **[!UICONTROL 使用瀏覽器區域設定]** 選項  **[!UICONTROL 保存]** 配置。

一旦識別了區域設定，自適應表單就會挑選特定於表單的字典。 如果找不到所請求區域設定的特定於表單的詞典，則使用詞典來編寫自適應表單的語言。

如果不存在區域設定資訊，則以表單的原始語言傳送自適應表單。 原始語言是自適應形式開發時使用的語言。

如果請求的區域設定的客戶端庫不存在，則它會檢查客戶端庫中是否存在語言代碼。 例如，如果請求的區域設定為 `en_ZA` （南非英語）和 `en_ZA` 不存在，自適應表單將使用 `en` （英語）語言（如果存在）。 但是，如果不存在這些字典，則自適應表單將 `en` 區域設定。

## 添加對不支援的語言環境的本地化支援 {#add-localization-support-for-non-supported-locales}

AEM Forms目前支援以英語(en)、西班牙語(es)、法語(fr)、義大利語(it)、德語(de)、日語(ja)、葡萄牙語 — 巴西語(pt-BR)、中文(zh-CN)、中文 — 台灣語(zh-TW)和韓語(ko-KR)語言環境本地化自適應表單內容。

要在自適應表單運行時添加對新區域設定的支援，請執行以下操作：

1. [將區域設定添加到GuideLocalizationService服務](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [為區域設定添加XFA客戶端庫](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [為區域設定添加自適應表單客戶端庫](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [為字典添加區域設定支援](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [重新啟動伺服器](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 將區域設定添加到指南本地化服務 {#add-a-locale-to-the-guide-localization-service-br}

1. 前往 `https://'[server]:[port]'/system/console/configMgr`.
1. 按一下可編輯 **指南本地化服務** 元件。
1. 將要添加的區域設定添加到支援的區域設定清單中。

![指南本地化服務](assets/configservice.png)

### 為區域設定添加XFA客戶端庫 {#add-xfa-client-library-for-a-locale-br}

建立類型的節點 `cq:ClientLibraryFolder` 在 `etc/<folderHierarchy>`，與類別 `xfaforms.I18N.<locale>`，並將下列檔案添加到客戶端庫：

* **I18N.js** 定義 `xfalib.locale.Strings` 為 `<locale>` 定義 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`。

* **js.txt** 包含以下內容：

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 為區域設定添加自適應表單客戶端庫 {#add-adaptive-form-client-library-for-a-locale-br}

建立類型的節點 `cq:ClientLibraryFolder` 在 `etc/<folderHierarchy>`，在類別中 `guides.I18N.<locale>` 和依賴項 `xfaforms.3rdparty`。 `xfaforms.I18N.<locale>` 和 `guide.common`。&quot;

將下列檔案添加到客戶端庫：

* **i18n.js** 定義 `guidelib.i18n`，具有&quot;calendarSymbols&quot;的圖案， `datePatterns`。 `timePatterns`。 `dateTimeSymbols`。 `numberPatterns`。 `numberSymbols`。 `currencySymbols`。 `typefaces` 為 `<locale>` 按照中所述的XFA規範 [區域設定規範](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)。 您還可以查看如何為中其他受支援的語言環境定義 `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`。
* **LogMessages.js** 定義 `guidelib.i18n.strings` 和 `guidelib.i18n.LogMessages` 為 `<locale>` 定義 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`。
* **js.txt** 包含以下內容：

```text
i18n.js
LogMessages.js
```

### 為字典添加區域設定支援 {#add-locale-support-for-the-dictionary-br}

僅在 `<locale>` 您正在添加的 `en`。 `de`。 `es`。 `fr`。 `it`。 `pt-br`。 `zh-cn`。 `zh-tw`。 `ja`。 `ko-kr`。

1. 建立 `nt:unstructured` 節點 `languages` 在 `etc`的子菜單。

1. 添加多值字串屬性 `languages` 到節點（如果尚未出現）。
1. 添加 `<locale>` 預設區域設定 `de`。 `es`。 `fr`。 `it`。 `pt-br`。 `zh-cn`。 `zh-tw`。 `ja`。 `ko-kr`的子菜單。

1. 添加 `<locale>` 到 `languages` 物業 `/etc/languages`。

的 `<locale>` 在 `https://'[server]:[port]'/libs/cq/i18n/translator.html`。

### 重新啟動伺服器 {#restart-the-server}

重新啟AEM動伺服器，使添加的區域設定生效。

## 添加對西班牙語支援的示例庫 {#sample-libraries-for-adding-support-for-spanish}

用於添加對西班牙語的支援的示例客戶端庫

[取得檔案](assets/sample.zip)
