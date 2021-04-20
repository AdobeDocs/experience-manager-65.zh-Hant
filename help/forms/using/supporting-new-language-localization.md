---
title: 支援最適化表單本地化的新地區
seo-title: 支援最適化表單本地化的新地區
description: AEM Forms允許您為本地化適應性表單添加新的地區。 依預設，支援的地區設定是英文、法文、德文和日文。
seo-description: AEM Forms允許您為本地化適應性表單添加新的地區。 依預設，支援的地區設定是英文、法文、德文和日文。
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
feature: Adaptive Forms
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---


# 支援最適化表單本地化的新地區設定{#supporting-new-locales-for-adaptive-forms-localization}

## 關於地區字典{#about-locale-dictionaries}

最適化表單的本地化需要兩種語言環境字典：

**表單特定字典** 包含最適化表單中使用的字串。例如，標籤、欄位名稱、錯誤訊息、說明說明等。 它作為一組XLIFF檔案來管理，用於每個區域設定，您可以在`https://<host>:<port>/libs/cq/i18n/translator.html`訪問它。

**全域** 字典在用戶端資料庫中有兩個全域字典，以JSON物AEM件管理。這些字典包含預設錯誤訊息、月名、貨幣符號、日期和時間模式等。 您可以在CRXDe Lite中找到這些字典，網址為/libs/fd/xfaforms/clientlibs/I18N。 這些位置包含每個地區設定的個別資料夾。 由於全域字典通常不會經常更新，因此在每個地區設定中保留個別的JavaScript檔案可讓瀏覽器快取這些字典，並減少在同一伺服器上存取不同最適化表單時的網路頻寬使用。

### 自適應表單的本地化如何運作{#how-localization-of-adaptive-form-works}

有兩種方法可識別最適化表單的地區。 在呈現最適化表單時，它會依下列項目識別所要求的地區設定：

* 查看最適化表單URL中的`[local]`選擇器。 URL的格式為`http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`。 使用`[local]`選擇器可快取最適化表單。

* 按指定順序查看以下參數：

   * 請求參數`afAcceptLang`
若要覆寫使用者的瀏覽器地區設定，您可以將 
`afAcceptLang` 請求參數來強制地區設定。例如，下列URL將強制在日文地區中轉換表單：
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * 為用戶設定的瀏覽器區域設定，該設定在使用`Accept-Language`標題的請求中指定。

   * 中指定的用戶的語言設定AEM。

   * 預設會啟用瀏覽器地區設定。 若要變更瀏覽器地區設定，
      * 開啟配置管理器。 URL為`http://[server]:[port]/system/console/configMgr`
      * 找到並開啟&#x200B;**[!UICONTROL 自適應表單和互動式通信Web通道]**&#x200B;配置。
      * 更改&#x200B;**[!UICONTROL 使用瀏覽器區域設定]**&#x200B;選項和&#x200B;**[!UICONTROL 保存]**&#x200B;配置的狀態。

一旦識別了地區設定，最適化表單就會挑選特定表單的字典。 如果找不到所請求地區的表單特定字典，則會使用該字典編寫最適化表單的語言。

如果沒有地區設定資訊，則會以表單的原始語言傳送最適化表單。 原始語言是開發適應性表單時使用的語言。

如果所請求地區的用戶端程式庫不存在，則會檢查地區中是否存在語言程式碼的用戶端程式庫。 例如，如果請求的語言環境為`en_ZA`（南非英文），而`en_ZA`的用戶端程式庫不存在，則最適化表單會使用`en`（英文）語言的用戶端程式庫（如果存在）。 但是，如果這些表單都不存在，則最適化表單會使用`en`地區設定的字典。

## 新增不支援地區設定的本地化支援{#add-localization-support-for-non-supported-locales}

AEM Forms目前支援以英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文——巴西(pt-BR)、中文(zh-CN)、中文——台灣(zh-TW)和韓文(ko-KR)地區語言，將調適性表單內容本地化。

若要在最適化表單執行時期新增語言環境支援：

1. [將地區設定新增至GuideLocalizationService服務](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [為地區設定新增XFA用戶端程式庫](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [為地區設定新增最適化表單用戶端程式庫](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [新增字典的地區設定支援](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [重新啟動伺服器](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 將語言環境添加到指南本地化服務{#add-a-locale-to-the-guide-localization-service-br}

1. 前往 `https://'[server]:[port]'/system/console/configMgr`.
1. 按一下以編輯&#x200B;**Guide Localization Service**&#x200B;元件。
1. 將要添加的區域設定添加到支援的區域設定清單中。

![指南本地化服務](assets/configservice.png)

### 為區域設定{#add-xfa-client-library-for-a-locale-br}添加XFA客戶端庫

在`etc/<folderHierarchy>`下建立類型`cq:ClientLibraryFolder`的節點（類別為`xfaforms.I18N.<locale>`），並將以下檔案添加到客戶端庫：

* **I18N.** js定義 `xfalib.locale.Strings` 的 `<locale>` 定義，如中所定 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`義。

* **js.** txt包含下列項目：

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 為區域設定{#add-adaptive-form-client-library-for-a-locale-br}添加自適應表單客戶端庫

在`etc/<folderHierarchy>`下建立類型`cq:ClientLibraryFolder`的節點，類別為`guides.I18N.<locale>` ，從屬關係為`xfaforms.3rdparty`、`xfaforms.I18N.<locale>`和`guide.common`。&quot;

將下列檔案新增至用戶端程式庫：

* **i18n.** jsdefing `guidelib.i18n`，具有&quot;CalendarSet&quot;的模式， `datePatterns`, `timePatterns`, `dateTimeSymbols` `numberPatterns`，對XFA符號進行了說明，在XSet Specification Set Specification Specification Set Specification Set Specification中對 `numberSymbols` `currencySymbols` `typefaces`  `<locale>`  [](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)CaS的說明。您也可以查看如何為`/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`中的其他受支援地區設定定義。
* **LogMessages.** jsdefing  `guidelib.i18n.strings` and  `guidelib.i18n.LogMessages` for the  `<locale>` as defined in `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.** txt包含下列項目：

```text
i18n.js
LogMessages.js
```

### 新增字典{#add-locale-support-for-the-dictionary-br}的地區支援

僅當要添加的`<locale>`不在`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`和`ko-kr`之間時，才執行此步驟。

1. 在`etc`下建立`nt:unstructured`節點`languages`（如果尚未存在）。

1. 將多值字串屬性`languages`新增至節點（如果尚未出現）。
1. 新增`<locale>`預設地區設定值`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr`（如果尚未出現）。

1. 將`<locale>`添加到`/etc/languages`的`languages`屬性的值中。

`<locale>`將顯示在`https://'[server]:[port]'/libs/cq/i18n/translator.html`。

### 重新啟動伺服器{#restart-the-server}

重新啟AEM動伺服器，使添加的語言環境生效。

## 新增西班牙文{#sample-libraries-for-adding-support-for-spanish}支援的范常式式庫

新增西班牙文支援的範例用戶端程式庫

[取得檔案](assets/sample.zip)
