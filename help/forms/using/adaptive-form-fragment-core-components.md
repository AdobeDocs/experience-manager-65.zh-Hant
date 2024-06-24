---
title: 什麼是最適化表單片段？
description: 最適化Forms提供一種機制，可建立在任何最適化表單中使用的表單區段（例如面板或欄位群組）。 您也可以將現有面板另存為片段。
topic-tags: author
keywords: 新增最適化表單片段， 最適化表單片段， 建立表單片段， 新增片段至最適化表單， 管理片段
feature: Adaptive Forms,Core Components
exl-id: 4a1ba259-8eb5-408f-8ee7-4868f98cca03
solution: Experience Manager, Experience Manager Forms
role: Admin, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1840'
ht-degree: 3%

---

# 在基於核心元件的自適應窗體中建立和使用自適應Forms片段 {#adaptive-form-fragments}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | 本文章 |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/adaptive-form-fragments-core-components.html) |

雖然每個表單都是為特定目的而設計，但大多數表單中都有一些常見的區段，例如提供個人詳細資訊，例如姓名和地址、家庭詳細資訊、收入詳細資訊。 每次建立新表單時，表單開發人員都必須建立這些通用區段。

最適化Forms提供一種便利的機制，讓您只需建立一次表單區段（例如面板或欄位群組），即可在最適化Forms中重複使用。 這些可重複使用的獨立區段稱為「最適化表單片段」。

表單片段可無縫整合至多種表單，精簡建立一致且專業外觀的表單。 表單片段透過「一次變更，處處反映」功能確保可重複性、標準化和品牌一致性。由於在一處進行的更新會自動傳播到使用這些片段的所有表單，因此可體驗更高的可維護性和效率。

您可以將片段多次新增到檔案，並使用其元件的資料繫結屬性將其連結到不同的資料來源或結構描述。 例如，您可以將相同的地址片段用於永久、通訊和帳單地址，並將其連線到資料來源或結構的不同欄位。

>[!NOTE]
>
> 您可以使用輕鬆為使用者自訂片段體驗 [表單片段元件的「設定」對話方塊和「設計」對話方塊](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-fragment.html).


## 建立表單片段 {#create-a-fragment}

您可以從頭開始建立最適化表單片段，或將現有最適化表單中的面板儲存為片段。 若要建立表單片段：

1. 在https://登入您的AEM Forms執行個體&#x200B;[*主機名稱*]：[*連線埠*]/aem/forms.html.
1. 按一下 **建立>自適應表單片段**.
1. 指定片段的標題、名稱、說明和標籤。 請確定您為片段指定唯一的名稱。 如果存在具有相同名稱的其他片段，則無法建立片段。
1. 選取表單範本。 您可以為以核心元件為基礎的Adaptive Forms或基礎元件為基礎的Adaptive Forms建立表單片段。
   * 若要建立核心元件型表單的表單片段，請選取核心元件型範本。
   * 若要為以基礎元件為基礎的表單建立表單片段，請選取基礎元件範本。 例如，/libs/fd/af/templateForFragment/defaultFragmentTemplate。

   當您建立核心元件型表單的表單片段時，請使用選取表單主題選項來選取核心元件型主題。

1. 按一下以開啟 **表單模型** 標籤，並從 **選取自** 下拉式選單，為片段選取以下其中一個模型：

   ![在表單模型標籤中顯示模型型別](assets/create-af-1-1.png)

   * **無**：指定從頭開始建立片段，而不使用任何表單模型。

     >[!NOTE]
     >
     > 在 Adaptive Forms 中，您可以多次使用單一窗體片段 （基於核心元件）。 它支援無型和結構描述型表單片段。

   * **架構**：指定使用上傳至 AEM Forms 的 XML 或 JSON 綱要建立片段。 您可以上傳或從可用的XML或JSON結構描述中選取作為片段的表單模型。 選取XML結構描述時，您也可以從以下專案選取所選結構描述中存在的complexType，以建立最適化表單片段： **[!UICONTROL XML結構描述複雜型別]** 下拉式方塊。 選取JSON結構描述時，您也可以從以下專案選取所選結構描述中存在的結構描述定義，以建立調適型表單片段： **[!UICONTROL json結構描述定義]** 下拉式方塊。
   * **表單資料模型**：指定使用表單資料模型建立片段。 您可以根據表單資料模型中只有一個資料模型物件來建立最適化表單片段。 展開表單資料模型定義下拉式清單。 它會列出指定表單資料模型中的所有資料模型物件。 從清單中選取資料模型物件。

   ![表單資料模型](assets/create-af-3.png)



1. 按兩下&#x200B;**建立**，然後按兩下打開&#x200B;**，**&#x200B;以在編輯模式下使用預設範本打開片段。在編輯模式中，您可以新增任何最適化表單元件至片段。

<!-- For information about Adaptive Form components, see [Introduction to authoring Adaptive Forms](../../forms/using/introduction-forms-authoring.md). --> 此外，如果您選取XML結構描述或XDP表單範本作為片段的表單模型，內容尋找器中會出現一個顯示表單模型階層的新索引標籤。 它可讓您將表單模型元素拖放至片段上。 新增的表單模型元素會轉換為表單元件，同時保留關聯XDP或XSD的原始屬性。

根據結構或表單資料模型建立自適應表單片段後，表單資料模型或結構元素會出現在Adaptive Form編輯器中，內容瀏覽器的「資料來源」標籤中。 您可以將表單模型元素拖放至片段上。 新增的表單模型元素會轉換為表單元件，同時保留關聯結構描述的原始屬性。


## 將片段新增至最適化表單 {#insert-a-fragment-in-an-adaptive-form}

若要將最適化表單片段新增至最適化表單：

1. 在編輯模式中開啟最適化表單。
1. 新增 **最適化表單片段** 元件至表單。
1. 按一下 **資產** 內容瀏覽器側欄。 在資產瀏覽器的路徑下，選取 **最適化表單片段** 選項。 您的表單可用的所有Adaptive Forms片段（視表單的模型而定）都會出現。

   ![選取最適化表單片段選項](assets/adaptive-forms-fragments.png)

1. 將最適化表單片段拖放至 **最適化表單片段** 最適化表單上的元件。

   >[!NOTE]
   >
   >未啟用最適化表單片段來從最適化表單內進行製作。 此外，您無法在JSON型最適化表單中使用XSD型片段，反之亦然。

最適化表單片段是參考最適化表單而新增，並與獨立的最適化表單片段保持同步。 這代表對最適化表單片段所做的任何修改，都會反映在片段併入最適化Forms的所有執行個體中。

### 在最適化表單中嵌入片段 {#embed-a-fragment-in-adaptive-form}

您可以選擇將最適化窗體片段嵌入最適化表單中，方法是按下 ![所添加片段的面板工具列「內嵌](assets/Smock_Import_18_N.svg) 」圖示

嵌入的片段不再與獨立片段連結。 您可以從最適化表單中編輯嵌入片段中的元件。

<!-- 
## Configure fragment appearance {#configure-fragment-appearance}

Any fragment you insert in Adaptive Forms appears as a placeholder image. The placeholder displays titles of up to a maximum of ten child panels in the fragment. You can configure AEM Forms to show the complete fragment instead of the placeholder image.

Perform the following steps to show complete fragments in forms:

1. Go to AEM web console configuration page at https:[*host*]:[*port*]/system/console/configMgr.

1. Search and click **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** to open it in edit mode.
1. Disable **[!UICONTROL Enable Placeholder in place of Fragment]** checkbox to show complete fragments rather than the placeholder image.

-->

### 使用片段中的片段 {#using-fragments-within-fragments}

您可以建立巢狀的Adaptive Form片段，這表示您可以將片段拖放到另一個片段中，而且可以有巢狀片段結構。

### 在最適化表單中多次使用表單片段 {#using-form-fragment-mutiple-times-in-af}

您可以在自適應表單中多次使用基於非基於綱要的表單片段，為每個表單片段欄位唯一地保存數據。 例如，您可以使用地址表單片段在貸款應用程式表單中收集永久、通信和當前居住地址的地址詳細信息。

![在自適應表單中使用多個片段](assets/using-multiple-fragment-af.gif)

## 自動數據綁定的片段映射 {#auto-mapping-of-fragments-for-data-binding}

當您使用 XFA 表單 範本 或 XSD 複雜類型創建自適應表單片段並將該片段拖放到自適應表單時，XFA 片段或 XSD 複合類型將自動替換為相應的自適應表單片段，其片段模型根映射到 XFA 片段或 XSD 複雜類型。

您可以從「編輯元件」對話方塊變更片段資產及其連結。

您也可以從AEM內容尋找器中的最適化表單片段資料庫拖放已繫結的最適化表單片段，並從Adaptive Form片段面板的「編輯」元件對話方塊提供正確的繫結參考。

## 管理片段 {#manage-fragments}

您可以使用AEM Forms UI對最適化表單片段執行數個操作。

1. 前往 `https://[hostname]/aem/forms.html`。

1. 按一下 **選取** 在AEM Forms UI工具列中選取最適化表單片段。 工具列會顯示您對選取的Adaptive Form片段可以執行的下列操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>編輯</p> </td>
   <td><p>在編輯模式中開啟選取的Adaptive Form片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>屬性</p> </td>
   <td><p>開啟屬性面板。 從「屬性」面板中，您可以檢視和編輯屬性、產生預覽，以及上傳所選片段的縮圖影像。 如需詳細資訊，請參閱 <a>管理中繼資料</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>複製</p> </td>
   <td><p>複製所選片段。 「貼上」按鈕會出現在工具列中。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>下載</p> </td>
   <td><p>下載選取的片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>預覽</p> </td>
   <td><p>提供以HTML預覽片段的選項，或透過將XML檔案的資料與片段合併來預覽自訂預覽。 如需詳細資訊，請參閱 <a>預覽表單</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>開始檢閱/管理檢閱</p> </td>
   <td><p>允許啟動和管理所選片段的審查。 如需詳細資訊，請參閱 <a>建立和管理稽核</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>新增字典</p> </td>
   <td><p>產生字典以將選取的片段本地化。 如需詳細資訊，請參閱 <a>將最適化Forms本地化</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>發佈/取消發佈</p> </td>
   <td><p>發佈/取消發佈選取的片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>刪除</p> </td>
   <td><p>刪除選取的片段。<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 使用片段時要記住的關鍵點 {#key-points-to-remember-when-working-with-fragments}

* 確保片段名稱是唯一的。 如果存在具有相同名稱的現有片段，則片段無法建立。
* 在XDP型最適化表單中，如果您將面板儲存為包含其他XDP片段的片段，則產生的片段會自動與子XDP片段繫結。 如果是XSD型最適化表單，產生的片段會與結構描述根繫結。
* 當您建立最適化表單片段時，會建立片段節點，這類似於CRXDE Lite的最適化表單的guideContainer節點。
* 不支援使用不同表單資料模型的最適化表單中的片段。 例如，XSD型最適化表單中不支援XDP型片段，反之亦然。
* 最適化表單片段可透過AEM內容尋找器中的最適化表單片段標籤使用。
* 透過參考插入或嵌入自適應表單時，獨立自適應表單片段中的任何運算式、指令碼或樣式都會保留。
* 您無法從最適化表單中編輯透過參考插入的最適化表單片段。 若要編輯，請編輯獨立的調適型表單片段或將片段嵌入調適型表單中。
* 發佈最適化表單時，您需要發佈在最適化表單中透過參考插入的獨立最適化表單片段。
* 當您重新發佈更新的Adaptive Form片段時，變更會反映在使用片段的Adaptive Form的已發佈例項中。
* 包含Verify元件的調適型表單不支援匿名使用者。 此外，不建議在自適應表單片段中使用驗證元件。
* （**僅限** Mac）為了確保表單片段功能在所有場景中都能完美運行，請將以下內容添加到 /private/etc/hosts 檔中：
  `127.0.0.1 <Host machine>` **主機**：部署AEM Forms的Apple Mac電腦。

## 參考片段 {#reference-fragments}

參考可用來建立表單的自適應表單片段。
<!-- For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md). -->

## 另請參閱 {#see-also}

* [建立以核心元件為基礎的最適化表單](create-an-adaptive-form-core-components.md)
* [使用規則 編輯者將動態行為添加到表單中](rule-editor.md)
* [建立或自定義基於核心元件的主題Forms](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [建立基於核心元件的 Adaptive Forms 的範本](template-editor.md)
* [建立或將自適應窗體新增至AEM Sites 頁面片段或體驗片段](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [範例主題範本和表單資料模型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
