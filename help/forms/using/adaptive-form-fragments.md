---
title: 最適化表單片段
seo-title: Adaptive form fragments
description: 適用性表單提供建立表單區段（例如面板或欄位群組）的機制，供任何適用性表單使用。 您也可以將現有面板儲存為片段。
seo-description: Adaptive forms provides a mechanism to create a form segment, such as a panel or a group of fields, as use it in any adaptive form. You can also save an existing panel as fragment.
uuid: bb4830b5-82a0-4026-9dae-542daed10e6f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
feature: Adaptive Forms
exl-id: 2f276e9d-b3c1-48f7-a94a-bdf7eb15a031
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 0%

---

# 最適化表單片段{#adaptive-form-fragments}

雖然每個表單都是為特定目的而設計，但大部分表單中都有一些常見的區段，例如提供個人詳細資訊，例如姓名和地址、家庭詳細資訊、收入詳細資訊等。 每次建立新表單時，表單開發人員都需要建立這些通用區段。

最適化表單提供一種便利的機制，讓您只需建立一次表單區段（例如面板或欄位群組），即可在最適化表單中重複使用。 這些可重複使用的獨立區段稱為最適化表單片段。

## 建立片段 {#create-a-fragment}

您可以從草稿建立最適化表單片段，或將現有最適化表單中的面板儲存為片段。

### 從頭建立片段 {#create-fragment-from-scratch}

1. 前往https://登入AEM Forms作者例項&#x200B;[*主機名*]:[*埠*]/aem/forms.html。
1. 按一下 **建立>最適化表單片段**.
1. 指定片段的標題、名稱、說明和標籤。

   >[!NOTE]
   >
   >請確定您指定片段的唯一名稱。 如果已存在另一個同名片段，則無法建立片段。

1. 按一下以開啟 **表單模型** 標籤，並從 **從** 下拉式選單中，為片段選取下列其中一個模型：

   * **無**:指定從頭建立片段，而不使用任何表單模型。
   * **表單範本**:指定使用上傳至AEM Forms的XDP範本來建立片段。 選取適當的XDP範本，作為片段的表單模型。

   ![使用表單範本作為模型建立最適化表單](assets/form-template-model.png)

   也會顯示所選表單範本中標示為片段的子表單。 您可以從下拉式清單中選取最適化表單片段的子表單。

   ![從指定的表單模板中選擇子表單](assets/fragment-subform.png)

   此外，您還可以使用未在表單範本中標示為片段的子表單建立最適化表單片段，方法是在下拉式方塊中指定子表單的SOM運算式。

   * **XML架構**:指定使用上傳至AEM Forms的XML架構來建立片段。 您可以上傳或從可用的XML結構中選取，作為片段的表單模型。

   ![根據XML架構建立最適化表單片段作為模型](assets/xml-schema-model.png)

   您也可以從下拉式方塊中選取出現在選取架構中的complexType，以建立最適化表單片段。

   ![從指定的XML架構模型中選擇複雜類型](assets/complex-type.png)

1. 按一下 **建立** 然後按一下 **開啟** 以編輯模式開啟片段（使用預設範本）。

在編輯模式中，您可以將任何最適化表單元件從AEM sidekick拖放至片段上。 如需最適化表單元件的相關資訊，請參閱 [製作最適化表單簡介](../../forms/using/introduction-forms-authoring.md).

此外，如果選擇XML架構或XDP表單模板作為片段的表單模型，則內容查找器中將顯示一個顯示表單模型層次結構的新頁簽。 它可讓您將表單模型元素拖放至片段上。 新增的表單模型元素會轉換為表單元件，同時保留相關XDP或XSD的原始屬性。

### 將面板儲存為片段 {#save-panel-as-a-fragment}

1. 開啟一個最適化表單，其中包含您要儲存為最適化表單片段的面板。
1. 在面板工具列中，按一下 **[!UICONTROL 另存為片段]**. 「另存為片段」對話方塊隨即開啟。

   >[!NOTE]
   >
   >如果您要儲存為片段的面板包含子面板，則產生的片段將包含這些面板。

1. 在「片段建立」對話方塊中，指定下列資訊：

   * **名稱**:片段的名稱。 預設值是面板的元素名稱。 這是必填欄位。
      >[!NOTE]
      >
      >請確定您指定片段的唯一名稱。 如果已存在另一個同名片段，則無法建立片段。

   * **標題**:片段的標題。 預設值為面板的標題。

   * **說明**:片段說明。

   * **標籤**:片段的標籤中繼資料。

   * **目標路徑**:儲存片段的存放庫路徑。 如果您未指定路徑，則會在包含最適化表單的節點旁建立與片段名稱相同的節點。 片段會儲存在此節點中。

   * **表單模型**:根據最適化表單的表單模型，此欄位會顯示 **XML架構**, **表單範本**，或 **無**. 這是不可編輯的欄位。

   * **片段模型根**:僅顯示在XSD型適用性表單中。 它指定片段模型的根。 您可以選擇 **/** 或下拉式清單中的XSD複雜類型。 請注意，只有選取複雜類型作為片段模型根時，才可以在另一個最適化表單中重複使用片段。
如果您選擇 **/** 作為片段模型根，根中的完整XSD樹狀結構會顯示在適用性表單資料模型索引標籤中。 對於複雜類型片段模型根，在最適化表單資料模型索引標籤中只會顯示所選複雜類型的子系。

   * **XSD參考**:僅顯示在XSD型適用性表單中。 它顯示XML架構的位置。

   * **XDP參考**:僅顯示在XDP型最適化表單中。 它會顯示XDP表單範本的位置。

   ![儲存片段](assets/save-fragment.png)

   另存為片段對話方塊

1. 按一下&#x200B;**「確定」**。

   面板會儲存在儲存庫的指定或預設位置。 在最適化表單中，面板會由片段的快照取代。 如下所示，「一般資訊」面板及其子面板「個人資訊」和「地址」會儲存為片段。

   若要編輯片段，請按一下 **[!UICONTROL 編輯資產]** 中。 片段會在新索引標籤或視窗中以編輯模式開啟。

   ![編輯片段](assets/edit-fragment.png)

## 使用片段 {#working-with-fragments}

### 設定片段外觀 {#configure-fragment-appearance}

您在適用性表單中插入的任何片段會顯示為預留位置影像。 預留位置在片段中最多顯示10個子面板的標題。 您可以設定AEM Forms以顯示完整片段，而非預留位置影像。

執行下列步驟以在表單中顯示完整片段：

1. 前往AEM Web主控台設定頁面（網址為https）:[*主機*]:[*埠*]/system/console/configMgr。

1. 搜尋並按一下 **[!UICONTROL 最適化表單與互動式通訊Web通道設定]** 以在編輯模式中開啟它。
1. 停用 **[!UICONTROL 啟用預留位置來取代片段]** 顯示完整片段而非預留位置影像的核取方塊。

### 在最適化表單中插入片段 {#insert-a-fragment-in-an-adaptive-form}

您建立的最適化表單片段會顯示在AEM內容尋找器的「最適化表單片段」標籤中。 若要在最適化表單中插入最適化表單片段：

1. 在編輯模式中開啟您要插入最適化表單片段的最適化表單。
1. 按一下 **資產** ![assets-browser](assets/assets-browser.png) 欄。 在資產瀏覽器中，選取 **最適化表單片段** 從下拉式清單中。

   您也可以選擇根據表單模型（表單範本、XML結構或基本）顯示所有最適化表單片段或篩選。

1. 將最適化表單片段拖放至最適化表單。

   >[!NOTE]
   >
   >適用性表單片段無法從適用性表單內進行製作。 此外，您無法以JSON型適用性表單使用XSD型片段，方式相反。

最適化表單片段是透過參考插入適用性表單中，並與獨立適用性表單片段同步。 這表示更新最適化表單片段時，變更會反映在使用片段的所有最適化表單中。

### 在最適化表單中內嵌片段 {#embed-a-fragment-in-adaptive-form}

您可以按一下「 」，選擇將最適化表單片段內嵌在最適化表單中 **內嵌資產：&lt;*fragmentName*>** 按鈕（如以下範例影像所示）。

![在最適化表單中內嵌表單片段](assets/embed-fragment.png)

>[!NOTE]
>
>內嵌片段不再與獨立片段連結。 您可以從最適化表單內編輯內嵌片段中的元件。

### 在片段內使用片段 {#using-fragments-within-fragments}

您可以建立巢狀最適化表單片段，這表示您可以拖放片段至另一個片段，且可以有巢狀片段結構。

### 變更片段 {#change-fragments}

您可以使用 **選取片段資產** 屬性（在「編輯元件」對話方塊中）。

## 用於資料綁定的片段自動映射 {#auto-mapping-of-fragments-for-data-binding}

當您使用XFA表單範本或XSD複雜類型建立適用性表單片段，並將片段拖放至適用性表單時，XFA片段或XSD複雜類型會自動取代為對應的適用性表單片段，其片段模型根對應至XFA片段或XSD複雜類型。

您可以從「編輯元件」對話框更改片段資產及其綁定。

>[!NOTE]
>
>您也可以在AEM內容尋找器中，從適用性表單片段程式庫拖放系結的適用性表單片段，並從適用性表單片段面板的「編輯」元件對話方塊提供正確的系結參考。

## 管理片段 {#manage-fragments}

您可以使用AEM Forms UI對最適化表單片段執行數個操作。

1. 前往 `https://[hostname]:'port'/aem/forms.html`.

1. 按一下 **選擇** 在AEM Forms UI工具列中，選取最適化表單片段。 工具列會顯示您可以對選取的最適化表單片段執行的下列操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>作業</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>開啟</p> </td>
   <td><p>在編輯模式中開啟選取的最適化表單片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>檢視屬性</p> </td>
   <td><p>開啟「屬性」面板。 從「屬性」面板，您可以檢視和編輯屬性、產生預覽，以及上傳所選片段的縮圖影像。 如需詳細資訊，請參閱 <a href="../../forms/using/manage-form-metadata.md" target="_blank">管理中繼資料</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>複製</p> </td>
   <td><p>複製所選片段。 「貼上」(Paste)按鈕出現在工具欄中。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>下載</p> </td>
   <td><p>下載所選片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>預覽</p> </td>
   <td><p>提供從XML檔案合併資料至片段，以HTML形式預覽片段或自訂預覽的選項。 如需詳細資訊，請參閱 <a href="/help/forms/using/previewing-forms.md" target="_blank">預覽表單</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>開始審閱/管理審閱</p> </td>
   <td><p>允許啟動和管理所選片段的審核。 如需詳細資訊，請參閱 <a href="../../forms/using/create-reviews-forms.md" target="_blank">建立和管理審核</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>建立字典</p> </td>
   <td><p>產生字典以將選取的片段當地語系化。 如需詳細資訊，請參閱 <a href="/help/forms/using/lazy-loading-adaptive-forms.md" target="_blank">將最適化表單當地語系化</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>發佈/取消發佈</p> </td>
   <td><p>發佈/取消發佈所選片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>刪除</p> </td>
   <td><p>刪除所選片段。<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 將包含片段的最適化表單當地語系化 {#localizing-adaptive-form-containing-fragments}

若要將包含最適化表單片段的最適化表單當地化，您需要將片段和表單分別當地化。 其構想是將片段本地化一次，然後在多個最適化表單中重複使用。

>[!NOTE]
>
>片段中的本地化索引鍵不會出現在最適化表單的XLIFF檔案中。

## 使用片段時應記住的關鍵點 {#key-points-to-remember-when-working-with-fragments}

* 請確定片段名稱是唯一的。 如果現有片段具有相同名稱，則無法建立片段。
* 在XDP型最適化表單中，如果您將面板儲存為包含其他XDP片段的片段，則產生的片段會自動系結至子XDP片段。 若是XSD型適用性表單，產生的片段將系結至結構根。
* 當您建立最適化表單片段時，會建立片段節點，這類似於CRXDe Lite中適用性表單的guideContainer節點。
* 不支援使用不同表單資料模型的適用性表單中的片段。 例如，XSD型適用性表單不支援XDP型片段，反之亦然。
* 可透過AEM內容尋找器中的「最適化表單片段」索引標籤，使用最適化表單片段。
* 當參考插入或內嵌於最適化表單片段時，會保留獨立適用性表單片段中的任何運算式、指令碼或樣式。
* 您無法從適用性表單內編輯由參考插入的適用性表單片段。 若要編輯，您可以編輯獨立的最適化表單片段，或將片段內嵌在最適化表單中。
* 發佈最適化表單時，您需要發佈參考所插入的獨立最適化表單片段。
* 重新發佈更新的最適化表單片段時，變更會反映在使用片段的最適化表單的已發佈例項中。
* 包含驗證元件的適用性表單不支援匿名使用者。 此外，不建議在最適化表單片段中使用驗證元件。
* (**僅限Mac**)若要確保表單片段功能在所有案例中均正常運作，請將下列項目新增至/private/etc/hosts檔案：
   `127.0.0.1 <Host machine>` **主機**:部署AEM Forms的Apple Mac電腦。

## 參考片段 {#reference-fragments}

可供參考可用來建立表單的最適化表單片段。 如需詳細資訊，請參閱 [參考片段](../../forms/using/reference-adaptive-form-fragments.md).
