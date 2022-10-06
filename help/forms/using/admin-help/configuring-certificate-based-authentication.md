---
title: 配置基於證書的身份驗證
seo-title: Configuring certificate-based authentication
description: 將證書頒發機構(CA)證書導入信任儲存，並為基於證書的身份驗證建立證書映射。
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

User Management通常使用用戶名和密碼來執行身份驗證。 使用者管理也支援憑證式驗證，您可使用憑證來透過Acrobat驗證使用者，或以程式設計方式驗證使用者。 如需以程式設計方式驗證使用者的詳細資訊，請參閱 [使用AEM表單進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63).

若要使用憑證式驗證，請將您信任的憑證授權單位(CA)憑證匯入信任存放區，然後建立憑證對應。

## 導入CA證書 {#import-the-ca-certificate}

匯入憑證時，請選取「信任憑證驗證」和「信任身分」選項，以及您需要的任何其他選項。 如需匯入憑證的詳細資訊，請參閱 [管理憑證](/help/forms/using/admin-help/certificates.md#managing-certificates).

## 配置證書映射 {#configuring-certificate-mapping}

若要為使用者啟用憑證式驗證，請建立憑證對應。 A *憑證對應* 定義證書屬性和域中用戶屬性之間的映射。 您可以將多個憑證對應至相同的網域。

當您測試憑證時，「使用者管理」會上傳憑證檢查，以確保符合下列要求：

* 證書有效。
* 您指定的頒發者可以驗證憑證。
* 憑證包含對應所需的屬性。
* 您指定的對應將憑證對應至AEM表單資料庫中的僅一名使用者。 系統會檢查目前和淘汰（已刪除）的使用者，以判斷他們是否符合對應條件。 因此，如果多個使用者（包括過時的使用者）具有要考慮的屬性值，則憑證測試會失敗。

>[!NOTE]
>
>無法編輯現有證書映射。

**新增憑證對應**

1. 在管理控制台中，按一下「設定>使用者管理>設定>憑證對應」 。
1. 按一下「新建證書映射」 ，然後在「用於頒發者」清單中，選擇信任儲存管理中配置的證書別名。
1. 將憑證的其中一個屬性對應至使用者的屬性。 例如，您可以將憑證的一般名稱對應至使用者的登入ID。

   如果憑證中屬性的內容與使用者管理資料庫中使用者屬性的內容不同，您可以使用Java規則運算式(regex)來比對這兩個屬性。 例如，如果憑證的一般名稱為 *Alex Pink（驗證）* 和 *Alex Pink（簽名）* 而用戶管理資料庫中的通用名稱是 *亞歷克斯·平克*，您可使用規則運算式來擷取憑證屬性的必要部分(在此範例中， *亞歷克斯·平克*.) 您指定的規則運算式必須符合Java規則運算式規範。

   您可以在「自訂順序」方塊中指定群組的順序，以轉換運算式。 自訂順序會與 `java.util.regex.Matcher.replaceAll()` 方法。 所看到的行為將與該方法的行為相對應，且必須據以指定輸入字串（自訂順序）。

   若要測試規則運算式，請在「測試參數」方塊中輸入值，然後按一下「測試」。

   您可以在規則運算式中使用下列字元：

   * .（任何字元）
   * &amp;ast;（0次或更多次）
   * ()（以方括弧指定組）
   * \（用於將規則運算式字元逸出為規則字元）
   * $n（用來指第n個群組）

   規則運算式的範例：

   * 從「Alex Pink（驗證）」中提取「Alex Pink」

      **Regex:** (.&amp;ast;)\（驗證\）

   * 從「Alex(Authentication)Pink」中提取「Alex Pink」

      **Regex:** (.&amp;ast;)\（驗證\）(.&amp;ast;)

   * 從「Alex(Authentication)Pink」中提取「Pink Alex」

      **Regex:** (.&amp;ast;)\（驗證\）(.&amp;ast;)

      自訂順序：$2 $1（傳回第二個群組，串連至第一個群組，由空白字元擷取）

   * 從&quot;smtp:apink@sampleorg.com&quot;中擷取&quot;apink@sampleorg.com&quot;

      **Regex:** smtp:(.&amp;ast;)
   如需使用規則運算式的詳細資訊，請參閱 [關於規則運算式的Java教學課程](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. 在「適用於域」清單中，選擇用戶的域。
1. 要測試此配置，請按一下「瀏覽」以上載示例用戶證書，按一下「測試證書」，如果配置正確，請按一下「確定」。

**編輯現有的憑證對應**

1. 在管理控制台中，按一下「設定>使用者管理>設定」 。
1. 按一下「憑證對應」 。
1. 選取憑證對應以編輯和編輯其設定。 您可以更新規則運算式和自訂順序。
1. 若要測試您的變更，請按一下「瀏覽」以上傳範例憑證，按一下「測試憑證」，然後按一下「確定」。

**刪除證書映射**

1. 在管理控制台中，按一下「設定>使用者管理>設定>憑證對應」 。
1. 選中要刪除的證書映射的複選框，按一下刪除，然後按一下確定。
