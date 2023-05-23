---
title: 配置基於證書的身份驗證
seo-title: Configuring certificate-based authentication
description: 將證書頒發機構(CA)證書導入到信任儲存中，並為基於證書的身份驗證建立證書映射。
seo-description: Import a Certificate Authority (CA) certificate into the Trust Store and create a certificate mapping for certificate-based authentication.
uuid: 9802a969-6d29-4b80-a4ed-06eb6e66e046
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d958ae65-3008-4d68-9e11-4346e149827f
exl-id: 9cbea8c8-4d42-446b-b98d-c090709624d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# 配置基於證書的身份驗證 {#configuring-certificate-based-authentication}

用戶管理通常使用用戶名和密碼執行身份驗證。 用戶管理還支援基於證書的身份驗證，您可以使用它通過Acrobat驗證用戶或以寫程式方式驗證用戶。 有關以寫程式方式驗證用戶的詳細資訊，請參見 [用表格編AEM程](https://www.adobe.com/go/learn_aemforms_programming_63)。

要使用基於證書的身份驗證，請將信任的證書頒發機構(CA)證書導入信任儲存，然後建立證書映射。

## 導入CA證書 {#import-the-ca-certificate}

導入證書時，選擇「信任證書驗證」和「信任身份」選項，以及您需要的任何其他選項。 有關導入證書的詳細資訊，請參閱 [管理證書](/help/forms/using/admin-help/certificates.md#managing-certificates)。

## 配置證書映射 {#configuring-certificate-mapping}

要為用戶啟用基於證書的身份驗證，請建立證書映射。 A *證書映射* 定義證書屬性與域中用戶屬性之間的映射。 可以將多個證書映射到同一域。

test證書時，用戶管理會上載證書檢查以確保它滿足以下要求：

* 證書有效。
* 您指定的頒發者可以驗證證書。
* 證書包含映射所需的屬性。
* 您指定的映射將證書映射到表單資料庫中的AEM一個用戶。 檢查當前用戶和過時（已刪除）用戶以確定它們是否與映射條件匹配。 因此，如果多個用戶（包括過時用戶）考慮屬性值，則證書test將失敗。

>[!NOTE]
>
>無法編輯現有證書映射。

**添加證書映射**

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「證書映射」。
1. 按一下新建證書映射，然後在「針對頒發者」清單中選擇在信任儲存管理中配置的證書別名。
1. 將證書的屬性之一映射到用戶的屬性。 例如，可以將證書的公用名稱映射到用戶的登錄ID。

   如果證書中屬性的內容與用戶管理資料庫中用戶屬性中的內容不同，則可以使用Java規則運算式(regex)來匹配這兩個屬性。 例如，如果證書的公用名稱是 *Alex Pink（驗證）* 和 *Alex Pink（簽名）* 並且用戶管理資料庫中的公用名稱是 *亞歷克斯·平克*，使用regex提取證書屬性的必需部分(在本例中， *亞歷克斯·平克*。) 指定的規則運算式必須符合Javaregex規範。

   通過在「自定義順序」框中指定組的順序，可以轉換表達式。 自定義訂單與 `java.util.regex.Matcher.replaceAll()` 的雙曲餘切值。 所看到的行為將與該方法的行為相對應，並且必須相應地指定輸入字串（自定義順序）。

   要test規則運算式，請在「Test參數」框中輸入一個值，然後按一下Test。

   可以在regex中使用以下字元：

   * 。（任何字元）
   * &amp;ast;（0次或多次）
   * ()（用括弧指定組）
   * \（用於將規則運算式字元轉義為正則字元）
   * $n（用於指第n組）

   規則運算式示例：

   * 從「Alex Pink（驗證）」中提取「Alex Pink」

      **規則運算式：** 。&amp;ast;)\（身份驗證\）

   * 從「Alex(Authentication)Pink」中提取「Alex Pink」

      **規則運算式：** 。&amp;ast;)\（驗證\）(.&amp;ast;)

   * 從「Alex(Authentication)Pink」中提取「Pink Alex」

      **規則運算式：** 。&amp;ast;)\（驗證\）(.&amp;ast;)

      自定義訂單：$2 $1（返回第二個組，連接到第一個組，由空格字元捕獲）

   * 從&quot;smtp:apink@sampleorg.com&quot;中解壓&quot;apink@sampleorg.com&quot;

      **規則運算式：** smtp:(...&amp;ast;)
   有關使用規則運算式的詳細資訊，請參見 [關於規則運算式的Java教程](https://java.sun.com/docs/books/tutorial/essential/regex/)。

1. 在「用於域」清單中，選擇用戶的域。
1. 要test此配置，請按一下「瀏覽」以上載示例用戶證書，按一下「Test證書」，如果配置正確，則按一下「確定」。

**編輯現有證書映射**

1. 在管理控制台中，按一下設定>用戶管理>配置。
1. 按一下「證書映射」。
1. 選擇要編輯和編輯其配置的證書映射。 您可以更新規則運算式和自定義順序。
1. 要test更改，請按一下「瀏覽」以上載示例證書，按一下「Test證書」，然後按一下「確定」。

**刪除證書映射**

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「證書映射」。
1. 選中要刪除的證書映射的複選框，按一下刪除，然後按一下確定。
