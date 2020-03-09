---
title: 支援最適化表單本地化的新地區
seo-title: 支援最適化表單本地化的新地區
description: AEM Forms可讓您新增本地化最適化表單的地區設定。 依預設，支援的地區設定是英文、法文、德文和日文。
seo-description: AEM Forms可讓您新增本地化最適化表單的地區設定。 依預設，支援的地區設定是英文、法文、德文和日文。
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
translation-type: tm+mt
source-git-commit: dbfadb0b49c83c38aa2cb55c32517ad70bbd79d0

---


# 支援最適化表單本地化的新地區{#supporting-new-locales-for-adaptive-forms-localization}

## 關於地區字典 {#about-locale-dictionaries}

最適化表單的本地化需要兩種語言環境字典：

**表單特定字典** ：包含最適化表單中使用的字串。 例如，標籤、欄位名稱、錯誤訊息、說明說明等。 它作為一組XLIFF檔案來管理，用於每個區域設定，您可以在中訪問 `https://<host>:<port>/libs/cq/i18n/translator.html`。

**全域字典** :AEM用戶端資料庫中有兩種全域字典，管理為JSON物件。 這些字典包含預設錯誤訊息、月名、貨幣符號、日期和時間模式等。 您可以在CRXDe Lite中找到這些字典，網址為/libs/fd/xfaforms/clientlibs/I18N。 這些位置包含每個地區設定的個別資料夾。 由於全域字典通常不會經常更新，因此在每個地區設定中保留個別的JavaScript檔案可讓瀏覽器快取這些字典，並減少在同一伺服器上存取不同最適化表單時的網路頻寬使用。

### 自適應表單的定位 {#how-localization-of-adaptive-form-works}

呈現最適化表單時，它會依指定順序查看下列參數，以識別所要求的地區設定：

* 請求參 `afAcceptLang`數若要覆寫使用者的瀏覽器地區設定，您可以傳遞 `afAcceptLang` 請求參數以強制地區設定。 例如，下列URL將強制在日文地區中轉換表單：
   `https://[server]:[port]/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* 為用戶設定的瀏覽器區域設定，該設定在使用標題的請求中指 `Accept-Language` 定。

* AEM中指定之使用者的語言設定。

一旦識別了地區設定，最適化表單就會挑選特定表單的字典。 如果找不到所請求地區的表單特定字典，則使用英文（英文）字典。

如果所請求地區的用戶端程式庫不存在，則會檢查地區中是否存在語言程式碼的用戶端程式庫。 例如，如果請求的地區設定為 `en_ZA` （南非英文），而用戶端程式庫不存在，則最適化表單會使用用戶端程式庫 `en_ZA``en` （英文）語言（如果存在）。 但是，如果這些表單都不存在，則最適化表單會使用字典進行地區 `en` 設定。

## 新增不支援地區設定的本地化支援 {#add-localization-support-for-non-supported-locales}

AEM Forms目前支援以英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文——巴西(pt-BR)、中文(zh-CN)、中文——台灣(zh-TW)和韓文(ko-KR)語言環境將調適性表單內容本地化。

若要在最適化表單執行時期新增語言環境支援：

1. [將地區設定新增至GuideLocalizationService服務](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [為地區設定新增XFA用戶端程式庫](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [為地區設定新增最適化表單用戶端程式庫](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [新增字典的地區設定支援](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [重新啟動伺服器](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 將地區設定新增至指南本地化服務 {#add-a-locale-to-the-guide-localization-service-br}

1. 前往 `https://[server]:[port]/system/console/configMgr`.
1. 按一下可編輯指 **南本地化服務元件** 。
1. 將要添加的區域設定添加到支援的區域設定清單中。

![指南本地化服務](assets/configservice.png)

### 為地區設定新增XFA用戶端程式庫 {#add-xfa-client-library-for-a-locale-br}

在下面建立類型 `cq:ClientLibraryFolder` 的節 `etc/<folderHierarchy>`點（具有類別），並 `xfaforms.I18N.<locale>`將下列檔案添加到客戶端庫：

* **I18N.js** ，定 `xfalib.locale.Strings` 義 `<locale>` 中的定義 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`。

* **js.txt** ，包含下列項目：

```
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 為地區設定新增最適化表單用戶端程式庫 {#add-adaptive-form-client-library-for-a-locale-br}

在下建立類型 `cq:ClientLibraryFolder` 的節 `etc/<folderHierarchy>`點，其類別為 `guides.I18N.<locale>` ，從屬關係為， `xfaforms.3rdparty`和 `xfaforms.I18N.<locale>``guide.common`。&quot;

將下列檔案新增至用戶端程式庫：

* **i18n** .js定義 `guidelib.i18n`，具有「日曆符號」的模式 `datePatterns`, `timePatterns`, `dateTimeSymbols`,XP規格的XP，在Set SpecificationLace中說明的 `numberPatterns``numberSymbols``currencySymbols``typefaces``<locale>`[](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)XFA規格， 您也可以查看中為其他受支援地區設定定義的方式 `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`。
* **LogMessages.js** 定義 `guidelib.i18n.strings` 和 `guidelib.i18n.LogMessages` ，如 `<locale>` 中定義 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`。
* **js.txt** ，包含下列項目：

```
i18n.js
LogMessages.js
```

### 新增字典的地區設定支援 {#add-locale-support-for-the-dictionary-br}

執行此步驟 `<locale>` 時，僅當添加 `en`不是、 `de`、 `es`、、 `fr`、 `it`、 `pt-br``zh-cn``zh-tw``ja``ko-kr`或。

1. 在下 `nt:unstructured` 建立 `languages` 節 `etc`點（如果尚未存在）。

1. 將多值字串屬性新增 `languages` 至節點（如果尚未出現）。
1. 添加缺 `<locale>` 省區域設定 `de`值、 、 `es`、 `fr`、 `it``pt-br``zh-cn``zh-tw``ja``ko-kr`、 Locade Not present 、 Locade Not。

1. 將添加 `<locale>` 到屬性的 `languages` 值中 `/etc/languages`。

將出 `<locale>` 現在 `https://[server]:[port]/libs/cq/i18n/translator.html`。

### Restart the server {#restart-the-server}

重新啟動AEM伺服器，讓新增的地區設定生效。

## 新增西班牙文支援的范常式式庫 {#sample-libraries-for-adding-support-for-spanish}

新增西班牙文支援的範例用戶端程式庫

[取得檔案](assets/sample.zip)
