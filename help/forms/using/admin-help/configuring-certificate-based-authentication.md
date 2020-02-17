---
title: 設定憑證式驗證
seo-title: 設定憑證式驗證
description: 將憑證授權機構(CA)憑證匯入信任存放區，並建立憑證對應以進行憑證式驗證。
seo-description: 將憑證授權機構(CA)憑證匯入信任存放區，並建立憑證對應以進行憑證式驗證。
uuid: 9802a969-6d29-4b80-a4ed-06eb6e66e046
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d958ae65-3008-4d68-9e11-4346e149827f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定憑證式驗證 {#configuring-certificate-based-authentication}

使用者管理通常使用使用者名稱和密碼來執行驗證。 使用者管理也支援憑證式驗證，您可使用此驗證來透過Acrobat驗證使用者，或以程式設計方式驗證使用者。 如需以程式設計方式驗證使用者的詳細資訊，請參 [閱「使用AEM表格進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63)」。

若要使用憑證式驗證，請將您信任的憑證授權機構(CA)憑證匯入信任存放區，然後建立憑證對應。

## 導入CA證書 {#import-the-ca-certificate}

匯入憑證時，請選取「信任認證」和「信任身分」選項，以及您需要的任何其他選項。 有關導入證書的詳細資訊，請參 [閱管理證書](/help/forms/using/admin-help/certificates.md#managing-certificates)。

## 配置證書映射 {#configuring-certificate-mapping}

若要為使用者啟用憑證式驗證，請建立憑證對應。 憑證 *對應* ，定義憑證屬性與網域中使用者屬性之間的對應。 您可以將多個憑證對應至相同的網域。

當您測試憑證時，「使用者管理」會上傳憑證檢查，以確保其符合下列要求：

* 憑證有效。
* 您指定的發行者可以驗證憑證。
* 證書包含映射所需的屬性。
* 您指定的對應將憑證對應至AEM表單資料庫中的僅一位使用者。 系統會檢查目前和已過時（已刪除）的使用者，以判斷他們是否符合對應標準。 因此，如果多個用戶（包括過時用戶）具有考慮的屬性值，則證書測試失敗。

>[!NOTE]
>
>您無法編輯現有的憑證對應。

**新增憑證對應**

1. 在管理控制台中，按一下「設定>使用者管理>設定>憑證對應」。
1. 按一下「新建證書映射」，然後在「發行者」清單中，選擇信任儲存管理中配置的證書別名。
1. 將憑證的其中一個屬性對應至使用者的屬性。 例如，您可以將憑證的公用名稱對應至使用者的登入ID。

   如果憑證中屬性的內容與使用者管理資料庫中使用者屬性的內容不同，您可以使用Java規則運算式(regex)來比對這兩個屬性。 例如，如果憑證的公用名稱是 *Alex Pink(Authentication)* 和 *Alex Pink(Signing)，而使用者管理資料庫的公用名稱是* Alex Pink *，則您會使用regex來擷取憑證屬性(在此範例中為*** Alex Pink)的必要部分。您指定的規則運算式必須符合Java regex規範。

   可以通過在「自定義順序」框中指定組的順序來轉換表達式。 自訂順序會與方法一起 `java.util.regex.Matcher.replaceAll()` 使用。 所看到的行為將對應該方法的行為，且必須相應地指定輸入字串（自訂順序）。

   若要測試規則運算式，請在「測試參數」方塊中輸入值，然後按一下「測試」。

   您可以在regex中使用下列字元：

   * . （任何字元）
   * &amp;ast;（0次或多次）
   * ()（以方括弧指定群組）
   * \（用於將regex字元逸出為規則字元）
   * $n（用於指第n個群組）
   規則運算式範例：

   * 從「Alex Pink（驗證）」摘取「Alex Pink」

      **** Regex:。&amp;ast;)\（驗證\）

   * 從「Alex(Authentication)Pink」摘取「Alex Pink」

      **** Regex:。&amp;ast;)\（驗證\）(.&amp;ast;)

   * 從「Alex(Authentication)Pink」摘取「Pink Alex」

      **** Regex:。&amp;ast;)\（驗證\）(.&amp;ast;)

      自訂順序：$2 $1（返回第二組，串連到第一組，由空白字元擷取）

   * 要從「smtp:apink@sampleorg.com」中提取「apink@sampleorg.com」

      **** Regex:smtp:(.&amp;ast;)
   如需使用規則運算式的詳細資訊，請參 [閱有關規則運算式的Java教學課程](https://java.sun.com/docs/books/tutorial/essential/regex/)。

1. 在「網域」清單中，選取使用者的網域。
1. 若要測試此設定，請按一下「瀏覽」以上傳範例使用者憑證，按一下「測試憑證」，如果設定正確，請按一下「確定」。

**編輯現有的憑證對應**

1. 在「管理控制台」中，按一下「設定>使用者管理>設定」。
1. 按一下「憑證對應」。
1. 選擇證書映射以編輯和編輯其配置。 您可以更新規則運算式和自訂順序。
1. 若要測試您的變更，請按一下「瀏覽」以上傳範例憑證，按一下「測試憑證」，然後按一下「確定」。

**刪除證書映射**

1. 在管理控制台中，按一下「設定>使用者管理>設定>憑證對應」。
1. 選擇要刪除的證書映射的複選框，按一下刪除，然後按一下確定。

