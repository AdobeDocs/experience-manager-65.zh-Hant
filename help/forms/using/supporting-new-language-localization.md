---
title: 支援最適化表單本地化的全新地區設定
description: AEM Forms可讓您新增本地化最適化表單的地區設定。 支援的地區設定預設為英文、法文、德文和日文。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
feature: Adaptive Forms,Foundation Components
role: Admin,User
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 2%

---

# 支援最適化表單本地化的全新地區設定{#supporting-new-locales-for-adaptive-forms-localization}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization.html) |
| AEM 6.5 | 本文章 |

## 關於地區字典 {#about-locale-dictionaries}

最適化表單本地化依賴兩種型別的地區詞典：

**表單特定字典**&#x200B;包含最適化表單中使用的字串。 例如，標籤、欄位名稱、錯誤訊息、說明說明說明等。 它被管理為每個地區設定的一組XLIFF檔案，您可以在`https://<host>:<port>/libs/cq/i18n/translator.html`存取它。

**全域字典**&#x200B;在AEM使用者端資料庫中有兩個全域字典，管理為JSON物件。 這些字典包含預設錯誤訊息、月份名稱、貨幣符號、日期和時間模式等。 您可以在CRXDe Lite的/libs/fd/xfaforms/clientlibs/I18N找到這些字典。 這些位置包含每個地區設定的個別資料夾。 由於全域字典通常不會經常更新，因此針對每個地區設定保留個別的JavaScript檔案可讓瀏覽器在存取相同伺服器上的不同最適化表單時，快取檔案並降低網路頻寬使用量。

### 最適化表單的本地化運作方式 {#how-localization-of-adaptive-form-works}

有兩種方法可識別最適化表單的地區設定。 轉譯適用性表單時，會透過識別要求的地區設定：

* 正在檢視最適化表單URL中的`[local]`選取器。 URL 的格式是：`http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`。使用`[local]`選擇器可允許快取最適化表單。

* 依指定順序檢視下列引數：

   * 要求引數`afAcceptLang`
若要覆寫使用者的瀏覽器地區設定，您可以傳遞`afAcceptLang`要求引數以強制地區設定。 例如，以下URL被強制以日文地區設定呈現表單：
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * 使用`Accept-Language`標頭在請求中指定之使用者的瀏覽器地區設定。

   * AEM中指定的使用者的語言設定。

   * 瀏覽器地區設定預設為啟用。 若要變更瀏覽器地區設定，
      * 開啟組態管理員。 URL是`http://[server]:[port]/system/console/configMgr`
      * 找到並開啟&#x200B;**[!UICONTROL 最適化表單和互動式通訊Web Channel]**&#x200B;設定。
      * 變更&#x200B;**[!UICONTROL 使用瀏覽器地區設定]**&#x200B;選項和&#x200B;**[!UICONTROL 儲存]**&#x200B;組態的狀態。

地區設定一經識別，最適化表單就會挑選表單專屬的字典。 如果找不到所要求地區設定的表單特定字典，則會使用最適化表單所編寫語言的字典。

如果沒有地區設定資訊出現，最適化表單會以表單的原始語言傳送。 原始語言是開發最適化表單時使用的語言。

如果要求的地區設定的使用者端程式庫不存在，它會檢查地區設定中存在的語言代碼的使用者端程式庫。 例如，如果要求的地區設定為`en_ZA` （南非英文），且`en_ZA`的使用者端資料庫不存在，則最適化表單會使用`en` （英文）語言的使用者端資料庫（如果存在）。 但是，如果兩者都不存在，則最適化表單會針對`en`地區設定使用字典。

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
1. 按一下以編輯&#x200B;**Guide Localization Service**&#x200B;元件。
1. 將您想要新增的區域設定新增至支援的區域設定清單。

![GuideLocalizationService](assets/configservice.png)

### 為地區設定新增XFA使用者端資料庫 {#add-xfa-client-library-for-a-locale-br}

在`etc/<folderHierarchy>`底下使用類別`xfaforms.I18N.<locale>`建立型別`cq:ClientLibraryFolder`的節點，並將下列檔案新增到使用者端程式庫：

* **I18N.js**&#x200B;定義了`/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`中定義的`<locale>`的`xfalib.locale.Strings`。

* **js.txt**&#x200B;包含下列專案：

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 為地區設定新增最適化表單使用者端資料庫 {#add-adaptive-form-client-library-for-a-locale-br}

在`etc/<folderHierarchy>`下建立型別`cq:ClientLibraryFolder`的節點，類別為`guides.I18N.<locale>`，相依性為`xfaforms.3rdparty`、`xfaforms.I18N.<locale>`和`guide.common`。 」

將下列檔案新增至使用者端資源庫：

* **i18n.js**&#x200B;定義了`guidelib.i18n`，並根據[地區設定集規格](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)中描述的XFA規格，為`<locale>`具有「calendarSymbols」、`datePatterns`、`timePatterns`、`dateTimeSymbols`、`numberPatterns`、`numberSymbols`、`currencySymbols`、`typefaces`的模式。 您也可以在`/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`中檢視其他支援地區設定的定義方式。
* **LogMessages.js**&#x200B;定義了`/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`中定義的`<locale>`的`guidelib.i18n.strings`和`guidelib.i18n.LogMessages`。
* **js.txt**&#x200B;包含下列專案：

```text
i18n.js
LogMessages.js
```

### 新增字典的地區設定支援 {#add-locale-support-for-the-dictionary-br}

只有在您新增的`<locale>`不屬於`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr`時，才執行此步驟。

1. 在`etc`下建立`nt:unstructured`節點`languages` （如果尚未存在）。

1. 將多值字串屬性`languages`新增至節點（如果尚未存在）。
1. 新增`<locale>`預設地區設定值`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` （如果尚未存在）。

1. 將`<locale>`新增至`/etc/languages`的`languages`屬性值。

`<locale>`將顯示在`https://'[server]:[port]'/libs/cq/i18n/translator.html`。

### 重新啟動伺服器 {#restart-the-server}

重新啟動AEM伺服器，讓新增的地區設定生效。

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

## 新增西班牙文支援的範常式式庫 {#sample-libraries-for-adding-support-for-spanish}

新增西班牙文支援的使用者端資料庫範例

[取得檔案](assets/sample.zip)
