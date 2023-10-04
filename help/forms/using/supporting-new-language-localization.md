---
title: 支援最適化表單本地化的全新地區設定
description: AEM Forms可讓您新增本地化最適化表單的地區設定。 支援的地區設定預設為英文、法文、德文和日文。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
feature: Adaptive Forms
role: Admin
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 2%

---

# 支援最適化表單本地化的全新地區設定{#supporting-new-locales-for-adaptive-forms-localization}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization.html) |
| AEM 6.5 | 本文章 |

## 關於地區字典 {#about-locale-dictionaries}

最適化表單本地化依賴兩種型別的地區詞典：

**表單特定字典** 包含最適化表單中使用的字串。 例如，標籤、欄位名稱、錯誤訊息、說明說明說明等。 它作為每個地區設定的一組XLIFF檔案進行管理，您可以在以下位置存取它： `https://<host>:<port>/libs/cq/i18n/translator.html`.

**全域字典** AEM使用者端資料庫中有兩個全域字典，以JSON物件形式管理。 這些字典包含預設錯誤訊息、月份名稱、貨幣符號、日期和時間模式等。 您可以在CRXDe Lite的/libs/fd/xfaforms/clientlibs/I18N找到這些字典。 這些位置包含每個地區設定的個別資料夾。 由於全域字典通常不會經常更新，因此針對每個地區設定保留個別的JavaScript檔案，可讓瀏覽器在存取相同伺服器上的不同最適化表單時，快取檔案並降低網路頻寬使用量。

### 最適化表單的本地化運作方式 {#how-localization-of-adaptive-form-works}

有兩種方法可識別最適化表單的地區設定。 轉譯適用性表單時，會透過識別要求的地區設定：

* 檢視 `[local]` 最適化表單URL中的選取器。 URL 的格式是：`http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`。使用 `[local]` 選擇器允許快取最適化表單。

* 依指定順序檢視下列引數：

   * 要求引數 `afAcceptLang`
若要覆寫使用者的瀏覽器地區設定，您可以傳遞 `afAcceptLang` 要求引數以強制地區設定。 例如，以下URL被強制以日文地區設定呈現表單：
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * 為使用者設定的瀏覽器地區設定，該設定是在使用 `Accept-Language` 標頭。

   * AEM中指定的使用者的語言設定。

   * 瀏覽器地區設定預設為啟用。 若要變更瀏覽器地區設定，
      * 開啟組態管理員。 URL為 `http://[server]:[port]/system/console/configMgr`
      * 找到並開啟 **[!UICONTROL 最適化表單和互動式通訊Web Channel]** 設定。
      * 變更狀態 **[!UICONTROL 使用瀏覽器地區設定]** 選項和  **[!UICONTROL 儲存]** 設定。

地區設定一經識別，最適化表單就會挑選表單專屬的字典。 如果找不到所要求地區設定的表單特定字典，則會使用最適化表單所編寫語言的字典。

如果沒有地區設定資訊出現，最適化表單會以表單的原始語言傳送。 原始語言是開發最適化表單時使用的語言。

如果要求的地區設定的使用者端程式庫不存在，它會檢查地區設定中存在的語言代碼的使用者端程式庫。 例如，如果要求的地區設定為 `en_ZA` （南非英文）和的客戶資料庫 `en_ZA` 不存在，調適型表單將使用使用者端程式庫 `en` （英文）語言（如果有的話）。 但是，如果兩者都不存在，則最適化表單會將該字典用於 `en` 地區設定。

## 新增不支援地區設定的本地化支援 {#add-localization-support-for-non-supported-locales}

AEM Forms目前支援英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)本地化內容。

若要在最適化表單執行階段新增對新地區設定的支援：

1. [新增語言環境至GuideLocalizationService服務](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [為地區設定新增XFA使用者端資料庫](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [為地區設定新增最適化表單使用者端資料庫](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [新增字典的地區設定支援](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [重新啟動伺服器](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 新增語言環境至指南本地化服務 {#add-a-locale-to-the-guide-localization-service-br}

1. 前往 `https://'[server]:[port]'/system/console/configMgr`。
1. 按一下以編輯 **指南本地化服務** 元件。
1. 將您想要新增的區域設定新增至支援的區域設定清單。

![GuideLocalizationService](assets/configservice.png)

### 為地區設定新增XFA使用者端資料庫 {#add-xfa-client-library-for-a-locale-br}

建立型別節點 `cq:ClientLibraryFolder` 在 `etc/<folderHierarchy>`，含類別 `xfaforms.I18N.<locale>`，並將下列檔案新增至使用者端資源庫：

* **I18N.js** 定義 `xfalib.locale.Strings` 針對 `<locale>` 如中的定義 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** 包含下列專案：

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 為地區設定新增最適化表單使用者端資料庫 {#add-adaptive-form-client-library-for-a-locale-br}

建立型別節點 `cq:ClientLibraryFolder` 在 `etc/<folderHierarchy>`，類別為 `guides.I18N.<locale>` 和相依關係為 `xfaforms.3rdparty`， `xfaforms.I18N.<locale>` 和 `guide.common`.&quot;

將下列檔案新增至使用者端資源庫：

* **i18n.js** 定義 `guidelib.i18n`，有「calendarSymbols」的模式， `datePatterns`， `timePatterns`， `dateTimeSymbols`， `numberPatterns`， `numberSymbols`， `currencySymbols`， `typefaces` 針對 `<locale>` 依據中所述的XFA規格 [地區設定組規格](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf). 您也可以在中檢視其他支援地區設定的定義方式 `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **logmessages.js** 定義 `guidelib.i18n.strings` 和 `guidelib.i18n.LogMessages` 針對 `<locale>` 如中的定義 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** 包含下列專案：

```text
i18n.js
LogMessages.js
```

### 新增字典的地區設定支援 {#add-locale-support-for-the-dictionary-br}

只有在 `<locale>` 您新增的內容不屬於 `en`， `de`， `es`， `fr`， `it`， `pt-br`， `zh-cn`， `zh-tw`， `ja`， `ko-kr`.

1. 建立 `nt:unstructured` 節點 `languages` 在 `etc`，如果尚未存在。

1. 新增多值字串屬性 `languages` 至節點（如果尚未出現）。
1. 新增 `<locale>` 預設地區設定值 `de`， `es`， `fr`， `it`， `pt-br`， `zh-cn`， `zh-tw`， `ja`， `ko-kr`，如果尚未存在。

1. 新增 `<locale>` 至的值 `languages` 屬性 `/etc/languages`.

此 `<locale>` 將顯示在 `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### 重新啟動伺服器 {#restart-the-server}

重新啟動AEM伺服器，讓新增的地區設定生效。

## 新增西班牙文支援的範常式式庫 {#sample-libraries-for-adding-support-for-spanish}

新增西班牙文支援的使用者端資料庫範例

[取得檔案](assets/sample.zip)
