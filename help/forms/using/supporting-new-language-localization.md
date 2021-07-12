---
title: 支援最適化表單本地化的新地區設定
seo-title: 支援最適化表單本地化的新地區設定
description: AEM Forms可讓您新增當地語系化最適化表單的地區設定。 預設情況下，支援的地區設定是英文、法文、德文和日文。
seo-description: AEM Forms可讓您新增當地語系化最適化表單的地區設定。 預設情況下，支援的地區設定是英文、法文、德文和日文。
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
feature: 適用性表單
role: Admin
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# 支援最適化表單本地化的新地區設定{#supporting-new-locales-for-adaptive-forms-localization}

## 關於語言環境字典 {#about-locale-dictionaries}

最適化表單的本地化需要兩種語言環境字典：

**表單特定字** 典包含適用性表單中使用的字串。例如，標籤、欄位名稱、錯誤訊息、說明說明等。 它被作為一組XLIFF檔案來管理，用於每個區域設定，您可以在`https://<host>:<port>/libs/cq/i18n/translator.html`訪問它。

**全域** 字典AEM用戶端資料庫中有兩個全域字典，管理為JSON物件。這些字典包含預設錯誤訊息、月份名稱、貨幣符號、日期和時間模式等。 您可以在CRXDe Lite中找到這些字典，網址為/libs/fd/xfaforms/clientlibs/I18N。 這些位置包含每個區域設定的單獨資料夾。 由於全域字典通常不會經常更新，因此為每個區域設定保留個別的JavaScript檔案，可讓瀏覽器快取，並減少在同一伺服器上存取不同最適化表單時的網路頻寬使用。

### 最適化表單的本地化運作方式 {#how-localization-of-adaptive-form-works}

有兩種方法可識別最適化表單的地區設定。 呈現最適化表單時，會依以下項目識別要求的地區設定：

* 查看適用性表單URL中的`[local]`選取器。 URL的格式為`http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`。 使用`[local]`選擇器可快取最適化表單。

* 以指定順序查看下列參數：

   * 要求參數`afAcceptLang`
若要覆寫使用者的瀏覽器地區設定，您可以傳遞 
`afAcceptLang` 要求參數以強制地區設定。例如，下列URL將強制以日文地區來轉譯表單：
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * 為用戶設定的瀏覽器區域設定，使用`Accept-Language`標題在請求中指定。

   * 在AEM中指定之使用者的語言設定。

   * 預設會啟用瀏覽器地區設定。 要更改瀏覽器區域設定，
      * 開啟配置管理器。 URL為`http://[server]:[port]/system/console/configMgr`
      * 找到並開啟&#x200B;**[!UICONTROL 適用性表單和互動式通訊Web通道]**&#x200B;設定。
      * 更改配置的&#x200B;**[!UICONTROL 使用瀏覽器區域設定]**&#x200B;選項和&#x200B;**[!UICONTROL 保存]**&#x200B;的狀態。

識別地區設定後，適用性表單會挑選表單特定字典。 如果找不到所請求地區的表單特定字典，則會針對製作最適化表單的語言使用字典。

如果沒有地區設定資訊，則會以表單的原始語言傳送最適化表單。 原始語言是開發最適化表單時使用的語言。

如果所請求區域的客戶端庫不存在，則它檢查客戶端庫中是否存在語言代碼。 例如，如果請求的地區設定為`en_ZA`（南非英語），並且`en_ZA`的客戶端庫不存在，則適用性表單將使用`en`（英語）語言的客戶端庫（如果存在）。 但是，如果沒有任何字典，適用性表單會將字典用於`en`地區設定。

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
1. 按一下可編輯&#x200B;**指南本地化服務**&#x200B;元件。
1. 將要添加的區域設定添加到支援的區域設定清單中。

![指南本地化服務](assets/configservice.png)

### 為地區設定新增XFA用戶端程式庫 {#add-xfa-client-library-for-a-locale-br}

在`etc/<folderHierarchy>`下建立類型`cq:ClientLibraryFolder`（類別`xfaforms.I18N.<locale>`）的節點，並將下列檔案添加到客戶端庫：

* **I18N.** jsdefining `xfalib.locale.Strings`  for  `<locale>` （如中定義） `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`。

* **js.** txt包含下列項目：

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 為區域設定新增最適化表單用戶端程式庫 {#add-adaptive-form-client-library-for-a-locale-br}

在`etc/<folderHierarchy>`下建立類型`cq:ClientLibraryFolder`的節點，類別為`guides.I18N.<locale>`，依賴項為`xfaforms.3rdparty`、`xfaforms.I18N.<locale>`和`guide.common`。 &quot;

將以下檔案添加到客戶端庫：

* **i18n.** jsdefining  `guidelib.i18n`，具有「calendarSymbols」、 `datePatterns`、 `timePatterns`、 `dateTimeSymbols`、 `numberPatterns`、 `numberSymbols`、 `currencySymbols`、 `typefaces` 的模式，根據 `<locale>` 區域設定規範 [](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)中描述的XFA規範。您也可以看到如何為`/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`中的其他支援地區設定定義。
* **LogMessages.js** 定 `guidelib.i18n.strings` 義 `guidelib.i18n.LogMessages` 和，如 `<locale>` 中定義 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`。
* **js.** txt包含下列項目：

```text
i18n.js
LogMessages.js
```

### 為字典添加地區支援 {#add-locale-support-for-the-dictionary-br}

僅當添加的`<locale>`不在`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr`之間時，才執行此步驟。

1. 在`etc`下建立`nt:unstructured`節點`languages`（如果尚未存在）。

1. 將多值字串屬性`languages`添加到節點（如果尚未存在）。
1. 新增`<locale>`預設地區設定值`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr`（如果尚未出現）。

1. 將`<locale>`添加到`/etc/languages`的`languages`屬性的值中。

`<locale>`將顯示在`https://'[server]:[port]'/libs/cq/i18n/translator.html`。

### 重新啟動伺服器 {#restart-the-server}

重新啟動AEM伺服器，讓新增的地區設定生效。

## 新增西班牙文支援的范常式式庫 {#sample-libraries-for-adding-support-for-spanish}

新增西班牙文支援的用戶端程式庫範例

[取得檔案](assets/sample.zip)
