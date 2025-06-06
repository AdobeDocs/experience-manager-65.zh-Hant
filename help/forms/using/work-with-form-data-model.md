---
title: 使用表單資料模型
description: 資料整合提供表單資料模型編輯器，可設定和使用表單資料模型。
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 16b76265-9ec4-4993-9ac0-b7aef1b1e5f1
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '4159'
ht-degree: 0%

---

# 使用表單資料模型{#work-with-form-data-model}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/work-with-form-data-model.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

![資料整合](do-not-localize/data-integeration.png)

表單資料模型編輯器提供直覺式使用者介面和工具，用於編輯和設定表單資料模型。 使用編輯器，您可以從表單資料模型中的相關資料來源新增及設定資料模型物件、屬性和服務。 此外，它可讓您在不使用資料來源的情況下建立資料模型物件和屬性，並在稍後將它們與各自的資料模型物件和屬性繫結。 您也可以產生和編輯資料模型物件屬性的範例資料，以便在預覽時用來預先填入最適化表單和互動式通訊。 您可以測試表單資料模型中設定的資料模型物件和服務，以確保其與資料來源正確整合。

如果您是初次使用Forms資料整合，但尚未設定資料來源或建立表單資料模型，請參閱下列主題：

* [AEM Forms資料整合](/help/forms/using/data-integration.md)
* [設定資料來源](/help/forms/using/configure-data-sources.md)
* [建立表單資料模型](/help/forms/using/create-form-data-models.md)

請閱讀下文，瞭解您可以使用表單資料模型編輯器執行的各種任務和設定的詳細資訊。

>[!NOTE]
>
>您必須是&#x200B;**fdm-author**&#x200B;和&#x200B;**forms-user**&#x200B;群組的成員才能建立和使用表單資料模型。 請聯絡您的AEM管理員，以成為群組的成員。

## 新增資料模型物件及服務 {#add-data-model-objects-and-services}

如果您使用資料來源建立表單資料模型，您可以使用表單資料模型編輯器來新增資料模型物件和服務、設定其屬性、建立資料模型物件之間的關聯，以及測試表單資料模型和服務。

您可以從表單資料模型中的可用資料來源新增資料模型物件和服務。 當新增的資料模型物件出現在模型標籤中時，新增的服務出現在服務標籤中。

若要新增資料模型物件與服務：

1. 登入AEM編寫執行個體，導覽至&#x200B;**[!UICONTROL Forms >資料整合]**，然後開啟您要新增資料模型物件的表單資料模型。
1. 在資料來源窗格中，展開資料來源以檢視可用的資料模型物件及服務。
1. 選取您要新增至表單資料模型的資料模型物件和服務，並選取&#x200B;**[!UICONTROL 新增選取的專案]**。

   ![選取的物件](assets/selected-objects.png)

   選取的資料模型物件與服務

   >[!NOTE]
   >
   > 如果您的Forms資料模型包含物件，而該物件是關聯式資料庫的保留關鍵字，則可能會導致資料新增、更新或擷取問題。 因此，請避免在表單資料模型中使用這類物件。

   「模型」標籤會顯示所有資料模型物件及其加入至表單資料模型之屬性的圖形表示。 每個資料模型物件由表單資料模型中的方塊表示。

   ![模型標籤](assets/model-tab.png)

   模型標籤顯示新增的資料模型物件

   >[!NOTE]
   >
   >您可以按住並拖曳資料模型物件方塊，以便在內容區域中加以組織。 所有新增至表單資料模型的資料模型物件在「資料來源」窗格中都會呈現灰色。

   「服務」標籤會列出新增的服務。

   ![services-tab](assets/services-tab.png)

   「服務」標籤顯示資料模型服務

   >[!NOTE]
   >
   >除了資料模型物件和服務之外，OData服務中繼資料檔案還包括定義兩個資料模型物件之間關聯的導覽屬性。 如需詳細資訊，請參閱[使用OData服務的導覽屬性](#work-with-navigation-properties-of-odata-services)。

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存表單模型物件。

   >[!NOTE]
   >
   >您可以使用最適化表單規則，叫用您在表單資料模型的「服務」標籤中設定的服務。 設定的服務可在規則編輯器的Invoke Services動作中使用。如需在調適型表單規則中使用這些服務的詳細資訊，請參閱[規則編輯器](/help/forms/using/rule-editor.md)中的Invoke Services和設定規則值。

## 建立資料模型物件和子屬性 {#create-data-model-objects-and-child-properties}

### 建立資料模型物件 {#create-data-model-objects}

雖然您可以從已設定的資料來源新增資料模型物件，也可以建立沒有資料來源的資料模型物件或實體。 如果您尚未在表單資料模型中設定資料來源，此功能會特別實用。

若要在不使用資料來源的情況下建立資料模型物件：

1. 登入AEM作者執行個體，導覽至&#x200B;**[!UICONTROL Forms >資料整合]**，然後開啟您要建立資料模型物件或實體的表單資料模型。
1. 選取&#x200B;**[!UICONTROL 建立實體]**。
1. 在[建立資料模型]對話方塊中，指定資料模型物件的名稱，並選取&#x200B;**[!UICONTROL 新增]**。 資料模型物件會新增至表單資料模型。 新加入的資料模型物件未繫結至資料來源，且不具有下列影像所示的任何屬性。

   ![new-entity](assets/new-entity.png)

接下來，您可以在未繫結的資料模型物件中新增子屬性。

### 新增子屬性 {#child-properties}

表單資料模型編輯器可讓您在資料模型物件中建立子屬性。 建立時的屬性未繫結至資料來源中的任何屬性。 您稍後可以將子屬性與包含資料模型物件中的另一個屬性繫結。

若要建立子屬性：

1. 在表單資料模型中，選取資料模型物件並選取&#x200B;**[!UICONTROL 建立子屬性]**。
1. 在&#x200B;**[!UICONTROL 建立子屬性]**&#x200B;對話方塊中，分別在&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Type]**&#x200B;欄位中指定屬性的名稱和資料型別。 您可以選擇指定屬性的標題和說明。
1. 如果屬性是計算屬性，則啟用Computed 。 計算屬性的值是根據規則或運算式來評估。 如需詳細資訊，請參閱[編輯屬性](#edit-properties)。
1. 如果資料模型物件繫結至資料來源，則新增的子屬性會自動繫結至具有相同名稱和資料型別的父資料模型物件的屬性。

   若要手動繫結子屬性與資料模型物件屬性，請選取&#x200B;**[!UICONTROL 繫結參考]**&#x200B;欄位旁的瀏覽圖示。 **[!UICONTROL 選取物件]**&#x200B;對話方塊會列出父資料模型物件的所有屬性。 選取要繫結的屬性，然後選取勾號圖示。 請注意，您只能選取與子屬性具有相同資料型別的屬性。

1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存子屬性，並選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存表單資料模型。 子屬性現在已新增至資料模型物件。

建立資料模型物件和屬性後，您可以繼續根據表單資料模型建立最適化表單和互動式通訊。 稍後，當您有可用的資料來源且已設定資料來源時，即可將表單資料模型與資料來源繫結。 繫結將會在相關的自適應表單和互動式通訊中自動更新。 如需使用表單資料模型建立最適化表單和互動式通訊的詳細資訊，請參閱[使用表單資料模型](/help/forms/using/using-form-data-model.md)。

### 繫結資料模型物件和屬性 {#bind-data-model-objects-and-properties}

當您要與表單資料模型整合的資料來源可用時，您可以將其新增至表單資料模型，如[更新資料來源](/help/forms/using/create-form-data-models.md#update)中所述。 然後，執行下列操作以繫結未繫結的資料模型物件和屬性：

1. 在表單資料模型中，選取要與資料來源繫結的未繫結資料來源。
1. 選取&#x200B;**[!UICONTROL 編輯屬性]**。
1. 在&#x200B;**[!UICONTROL 編輯屬性]**&#x200B;窗格中，選取&#x200B;**[!UICONTROL 繫結]**&#x200B;欄位旁的瀏覽圖示。 它會開啟&#x200B;**[!UICONTROL 選取物件]**&#x200B;對話方塊，其中列出新增至表單資料模型中的資料來源。

   ![select-object](assets/select-object.png)

1. 展開資料來源樹狀結構並選取要繫結的資料模型物件，然後選取勾號圖示。
1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存屬性，然後選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存表單資料模型。 資料模型物件現在與資料來源繫結。 請注意，資料模型物件不再標籤為「未繫結」。

   ![繫結模型物件](assets/bound-model-object.png)

## 設定服務 {#configure-services}

若要讀取和寫入資料模型物件的資料，請執行以下動作來設定讀取和寫入服務：

1. 選取資料模型物件頂端的核取方塊以選取它，並選取&#x200B;**[!UICONTROL 編輯屬性]**。

   ![edit-properties](assets/edit-properties.png)

   編輯屬性以設定資料模型物件的讀取和寫入服務

   「編輯屬性」對話方塊開啟。

   ![edit-properties-2](assets/edit-properties-2.png)

   編輯內容對話方塊

   >[!NOTE]
   >
   >除了資料模型物件和服務之外，OData服務中繼資料檔案還包括定義兩個資料模型物件之間關聯的導覽屬性。 當您將OData服務資料來源新增至表單資料模型時，表單資料模型中有一項服務可用於資料模型物件中的所有導覽屬性。 您可以使用此服務來讀取對應資料模型物件的導覽屬性。
   >
   >
   >如需使用服務的詳細資訊，請參閱[使用OData服務的導覽屬性](#work-with-navigation-properties-of-odata-services)。

1. 切換&#x200B;**[!UICONTROL 最上層物件]**&#x200B;以指定資料模型物件是否為最上層模型物件。

   在表單資料模型中設定的資料模型物件可用於根據表單資料模型的最適化表單內容瀏覽器中的資料模型物件索引標籤。 當您在兩個資料模型物件之間新增關聯時，您與之關聯的資料模型物件會巢狀內嵌在從「資料模型物件」標籤中關聯的資料模型物件下。 如果巢狀資料模型是頂層物件，它也會單獨出現在「資料模型物件」標籤中。 因此，您會看到其中的兩個專案，一個在巢狀階層內，另一個在巢狀階層外，這可能會混淆表單作者。 若要讓關聯的資料模型物件只出現在巢狀階層中，請停用「最上層物件」屬性。

1. 為選取的資料模型物件選取讀取和寫入服務。 服務的引數會出現。

   ![讀寫服務](assets/read-write-services.png)

   為員工資料來源設定的讀寫服務

1. 選取![aem_6_3_edit](assets/aem_6_3_edit.png)將讀取服務引數繫結至[將引數繫結至使用者設定檔屬性、要求屬性或常值值](#bindargument)，並指定繫結值。
1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存引數，**[!UICONTROL 完成]**&#x200B;以儲存屬性，然後選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存表單資料模型。

### 繫結讀取服務引數 {#bindargument}

根據繫結值，將讀取服務引數繫結到使用者設定檔屬性、要求屬性或常值值。 值會作為引數傳遞至服務，以從資料來源擷取與指定值相關聯的詳細資料。

#### 常值數值 {#literal-value}

從&#x200B;**[!UICONTROL 繫結至]**&#x200B;下拉式功能表中選取&#x200B;**[!UICONTROL 常值]**，並在&#x200B;**[!UICONTROL 繫結值]**&#x200B;欄位中輸入值。 會從資料來源擷取與該值相關聯的詳細資料。 使用此選項可擷取與靜態值相關聯的詳細資料。

在此範例中，與&#x200B;**4367655678** （作為`mobilenum`引數的值）相關聯的詳細資料是從資料來源擷取。 如果傳遞行動號碼引數的值，關聯的詳細資料可包含客戶名稱、客戶地址和城市等屬性。

![常值值](assets/fdm_binding_literal_new.png)

#### 使用者檔案屬性 {#user-profile-attribute}

從&#x200B;**[!UICONTROL 繫結至]**&#x200B;下拉式功能表中選取&#x200B;**[!UICONTROL 使用者設定檔屬性]**，並在&#x200B;**[!UICONTROL 繫結值]**&#x200B;欄位中輸入屬性名稱。 根據屬性名稱，會從資料來源擷取登入AEM執行處理的使用者詳細資訊。

在&#x200B;**[!UICONTROL 繫結值]**&#x200B;欄位中指定的屬性名稱必須包含完整的繫結路徑，直到使用者的屬性名稱為止。 開啟以下URL以存取CRXDE上的使用者詳細資訊：

`https://[server-name]:[port]/crx/de/index.jsp#/home/users/`

![使用者設定檔](assets/binding_crxde_user_profile_new.png)

在此範例中，請在`grios`使用者的&#x200B;**[!UICONTROL 繫結值]**&#x200B;欄位中指定`profile.empid`。

![編輯引數](assets/edit_argument_user_profile_new.png)

`id`引數接受使用者設定檔的`empid`屬性值，並將其作為引數傳入Read服務。 它會從與登入使用者相關聯之`empid`的員工資料模型物件讀取並傳回關聯屬性的值。

#### 要求屬性 {#request-attribute}

使用請求屬性從資料來源擷取關聯的屬性。

1. 從&#x200B;**[!UICONTROL 繫結至]**&#x200B;下拉式功能表中選取&#x200B;**[!UICONTROL 要求屬性]**，並在&#x200B;**[!UICONTROL 繫結值]**&#x200B;欄位中輸入屬性名稱。

1. 為head.jsp建立[覆蓋](../../../help/sites-developing/overlays.md)。 若要建立覆蓋，請開啟CRX DE並將`https://<server-name>:<port number>/crx/de/index.jsp#/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp`檔案複製到`https://<server-name>:<port number>/crx/de/index.jsp#/apps/fd/af/components/page2/afStaticTemplatePage/head.jsp`

   >[!NOTE]
   >
   >* 如果您使用靜態範本，請將head.jsp覆蓋在：
   >  `/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp`
   >* 如果您使用可編輯的範本，請覆蓋aftemplatedpage.jsp，網址為：
   >  `/libs/fd/af/components/page2/aftemplatedpage/aftemplatedpage.jsp`

1. 設定要求屬性的[!DNL paramMap]。 例如，將下列程式碼加入apps資料夾的.jsp檔案中：

   ```javascript
   <%Map paraMap = new HashMap();
    paraMap.put("<request_attribute>",request.getParameter("<request_attribute>"));
    request.setAttribute("paramMap",paraMap);
   ```

   例如，使用以下程式碼從資料來源擷取petid的值：


   ```javascript
   <%Map paraMap = new HashMap();
   paraMap.put("petId",request.getParameter("petId"));
   request.setAttribute("paramMap",paraMap);%>
   ```

系統會根據要求中指定的屬性名稱，從資料來源擷取詳細資料。

例如，在要求中指定屬性為`petid=100`會從資料來源擷取與屬性值相關的屬性。

## 新增關聯 {#add-associations}

通常，在資料來源中的資料模型物件之間會建立關聯。 關聯可以是一對一或一對多。 例如，可以有多個與員工相關聯的相依項。 它稱為一對多關聯，由`1:n`在連線關聯資料模型物件的線上描述。 但是，如果關聯針對指定的員工ID傳回唯一員工名稱，則稱為一對一關聯。

當您將資料來源中的關聯資料模型物件新增至表單資料模型時，它們的關聯會保留並顯示為以箭頭線連線。 您可以在表單資料模型中跨不同資料來源的資料模型物件之間新增關聯。

>[!NOTE]
>
>JDBC資料來源中的預先定義關聯不會保留在表單資料模型中。 手動建立。

若要新增關聯：

1. 選取資料模型物件頂端的核取方塊以選取它，並選取&#x200B;**[!UICONTROL 新增關聯]**。 「新增關聯」對話方塊開啟。

   ![新增關聯](assets/add-association.png)

   >[!NOTE]
   >
   >除了資料模型物件和服務之外，OData服務中繼資料檔案還包括定義兩個資料模型物件之間關聯的導覽屬性。 在表單資料模型中新增關聯時，您可以使用這些導覽屬性。 如需詳細資訊，請參閱[使用OData服務的導覽屬性](#work-with-navigation-properties-of-odata-services)。

   「新增關聯」對話方塊開啟。

   ![add-association-2](assets/add-association-2.png)

   新增關聯對話方塊

1. 在「新增關聯」窗格中：

   * 指定關聯的標題。
   * 選取關聯型別 — 「一對一」或「一對多」。
   * 選取要關聯的資料模型物件。
   * 選取讀取服務，以從選取的模型物件讀取資料。 讀取服務引數會出現。 編輯以視需要變更引數，並將其繫結至要關聯的資料模型物件的屬性。

   在下列範例中，Dependents資料模型物件之讀取服務的預設引數為`dependentid`。

   ![add-association-example](assets/add-association-example.png)

   相依物件讀取服務的預設引數相依於

   但是，引數必須是關聯資料模型物件之間的共同屬性，在此範例中為`Employeeid`。 因此，`Employeeid`引數必須繫結至Employee資料模型物件的`id`屬性，才能從Dependents資料模型物件擷取關聯的相依專案詳細資料。

   ![add-association-example-2](assets/add-association-example-2.png)

   已更新引數和繫結

   選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存引數。

1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存關聯，然後選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存表單資料模型。
1. 視需要重複這些步驟以建立更多關聯。

>[!NOTE]
>
>新增的關聯會顯示在資料模型物件方塊中，並包含指定的標題和連線相關資料模型物件的直線。
>
>您可以選取關聯的核取方塊並選取&#x200B;**[!UICONTROL 編輯關聯]**&#x200B;來編輯關聯。

![已新增關聯](assets/added-association.png)

## 編輯屬性 {#properties}

您可以編輯資料模型物件的屬性、其屬性，以及在表單資料模型中新增的服務。

若要編輯屬性：

1. 選取表單資料模型中資料模型物件、屬性或服務旁的核取方塊。
1. 選取&#x200B;**[!UICONTROL 編輯屬性]**。 選取的模型物件、屬性或服務的&#x200B;**[!UICONTROL 編輯屬性]**&#x200B;窗格會開啟。

   * **資料模型物件**：指定讀取和寫入服務並編輯引數。
   * **屬性**：指定屬性的型別、子型別和格式。 您也可以指定選取的屬性是否為資料模型物件的主索引鍵。
   * **服務**：指定服務的輸入模型物件、輸出型別和引數。 對於Get服務，您可以指定是否預期它會傳回陣列。

   ![edit-properties-service](assets/edit-properties-service.png)

   Get服務的「編輯內容」對話方塊

1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存屬性，然後選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存表單資料模型。

### 建立計算屬性 {#computed}

計算屬性是根據規則或運算式計算其值的屬性。 您可以使用規則將計算屬性的值設定為常值字串、數字、數學運算式的結果或表單資料模型中其他屬性的值。

例如，您可以建立計算屬性&#x200B;**FullName**，其值是現有&#x200B;**FirstName**&#x200B;和&#x200B;**LastName**&#x200B;屬性串連的結果。 若要這麼做：

1. 建立資料型別為String且名稱為`FullName`的屬性。
1. 啟用&#x200B;**[!UICONTROL Computed]**&#x200B;並選取&#x200B;**[!UICONTROL Done]**&#x200B;以建立屬性。

   ![已計算](assets/computed.png)

   隨即建立FullName運算屬性。 請注意屬性旁的圖示，以描繪運算屬性。

   ![computed-prop](assets/computed-prop.png)

1. 選取FullName屬性並選取&#x200B;**[!UICONTROL 編輯規則]**。 規則編輯器視窗隨即開啟。
1. 在規則編輯器視窗中，選取&#x200B;**[!UICONTROL 建立]**。 **[!UICONTROL 設定值]**&#x200B;規則視窗隨即開啟。

   從「選取選項」下拉式清單中，選取&#x200B;**[!UICONTROL 數學運算式]**。 其他可用選項為&#x200B;**[!UICONTROL 表單資料模型物件]**&#x200B;和&#x200B;**[!UICONTROL 字串]**。

1. 在數學運算式中，分別選取第一個物件和第二個物件中的&#x200B;**[!UICONTROL 名字]**&#x200B;和&#x200B;**[!UICONTROL 姓氏]**。 選取&#x200B;**[!UICONTROL 加]**&#x200B;作為運運算元。

   選取&#x200B;**[!UICONTROL 完成]**，然後選取&#x200B;**[!UICONTROL 關閉]**&#x200B;以關閉規則編輯器視窗。 規則看起來類似下列。

   ![規則](assets/rule.png)

1. 在表單資料模型上，選取&#x200B;**[!UICONTROL 儲存]**。 運算屬性已設定。

## 使用OData服務的導覽屬性 {#work-with-navigation-properties-of-odata-services}

在OData服務中，導覽屬性用來定義兩個資料模型物件之間的關聯。 這些屬性是在圖元型別或複雜型別上定義的。 例如，在從範例[TripPin](https://www.odata.org/blog/trippin-new-odata-v4-sample-service/) OData範例服務的中繼資料檔案的下列擷取中，個人實體包含三個導覽屬性 — Friends、BestFriend和Trips。

如需有關導覽屬性的詳細資訊，請參閱[OData檔案](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752536)。

```xml
<edmx:Edmx xmlns:edmx="https://docs.oasis-open.org/odata/ns/edmx" Version="4.0">
<script/>
<edmx:DataServices>
<Schema xmlns="https://docs.oasis-open.org/odata/ns/edm" Namespace="Microsoft.OData.Service.Sample.TrippinInMemory.Models">
<EntityType Name="Person">
<Key>
<PropertyRef Name="UserName"/>
</Key>
<Property Name="UserName" Type="Edm.String" Nullable="false"/>
<Property Name="FirstName" Type="Edm.String" Nullable="false"/>
<Property Name="LastName" Type="Edm.String"/>
<Property Name="MiddleName" Type="Edm.String"/>
<Property Name="Gender" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.PersonGender" Nullable="false"/>
<Property Name="Age" Type="Edm.Int64"/>
<Property Name="Emails" Type="Collection(Edm.String)"/>
<Property Name="AddressInfo" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location)"/>
<Property Name="HomeAddress" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location"/>
<Property Name="FavoriteFeature" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature" Nullable="false"/>
<Property Name="Features" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature)" Nullable="false"/>
<NavigationProperty Name="Friends" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person)"/>
<NavigationProperty Name="BestFriend" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person"/>
<NavigationProperty Name="Trips" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Trip)"/>
</EntityType>
```

當您在表單資料模型中設定OData服務時，實體容器中的所有導覽屬性都可透過表單資料模型中的服務使用。 在此TripPin OData服務範例中，`Person`實體容器中的三個導覽屬性可以使用表單資料模型中的一個`GET LINK`服務來讀取。

以下特別說明表單資料模型中的`GET LINK of Person /People`服務，這是TripPin OData服務`Person`實體中三個導覽屬性的組合服務。

![nav-prop-service](assets/nav-prop-service.png)

將`GET LINK`服務新增至表單資料模型中的服務標籤後，您可以編輯屬性以選擇要在服務中使用的輸出模型物件與導覽屬性。 例如，下列範例中的下列`GET LINK of Person /People`服務使用Trip作為輸出模型物件，而導覽屬性作為Trips。

![edit-prop-nav-prop](assets/edit-prop-nav-prop.png)

>[!NOTE]
>
>**NavigationPropertyName**&#x200B;引數的&#x200B;**預設值**&#x200B;欄位中可用的值取決於&#x200B;**傳回陣列的狀態？**&#x200B;切換按鈕。 當啟用時，它會顯示集合型別的導覽屬性。

在此範例中，您也可以選擇輸出模型物件作為Person，選擇導覽屬性引數作為Friends或BestFriend （取決於&#x200B;**是否傳回陣列？）**&#x200B;已啟用或已停用)。

![edit-prop-nav-prop2](assets/edit-prop-nav-prop2.png)

同樣地，您可以在表單資料模型中新增關聯時，選擇`GET LINK`服務並設定其導覽屬性。 但是，若要能夠選取導覽屬性，請確定&#x200B;**[!UICONTROL 繫結至欄位]**&#x200B;設定為&#x200B;**常值**。

![add-association-nav-prop](assets/add-association-nav-prop.png)

## 產生和編輯範例資料 {#sample}

表單資料模型編輯器可讓您為表單資料模型中的所有資料模型物件屬性（包括計算屬性）產生範例資料。 這是一組隨機值，符合為每個屬性設定的資料型別。 您也可以編輯並儲存資料，即使您重新產生範例資料，資料仍會保留。

執行下列操作以產生和編輯範例資料：

1. 開啟表單資料模型並選取&#x200B;**[!UICONTROL 編輯範例資料]**。 它會在「編輯範例資料」視窗中產生並顯示範例資料。

   ![產生範例資料](assets/form_data_model_generate_sample_data_new.png)

1. 在&#x200B;**[!UICONTROL 編輯範例資料]**&#x200B;視窗中，視需要編輯資料，並選取&#x200B;**[!UICONTROL 儲存]**。

接下來，您可以使用範例資料，根據表單資料模型預先填寫及測試互動式通訊。 如需詳細資訊，請參閱[使用表單資料模型](/help/forms/using/using-form-data-model.md)。

## 測試資料模型物件與服務 {#test-data-model-objects-and-services}

您的表單資料模型已設定，但在投入使用之前，您可能想要測試已設定的資料模型物件和服務是否如預期般運作。 若要測試資料模型物件與服務：

1. 在表單資料模型中選取資料模型物件或服務，然後分別選取&#x200B;**[!UICONTROL 測試模型物件]**&#x200B;或&#x200B;**[!UICONTROL 測試服務]**。

   「測試表單資料模型」視窗隨即開啟。

   ![test-data-model](assets/test-data-model.png)

1. 在「測試表單資料模型」視窗中，從「輸入」窗格選取要測試的資料模型物件或服務。

1. 在測試程式碼中指定引數值，並選取&#x200B;**[!UICONTROL 測試]**。 成功的測試會傳回「輸出」窗格中的輸出。

   ![測試結果](assets/test_results_form_data_model_new.png)

同樣地，您可以在表單資料模型中測試其他資料模型物件與服務。

## 自動驗證輸入資料 {#automated-validation-of-input-data}

表單資料模型會在叫用DermisBridge API時（根據表單資料模型中提供的驗證條件），驗證作為輸入所收到的資料。 驗證是以用來叫用API的查詢物件中所設定的`ValidationOptions`旗標為基礎。

此旗標可設為下列任一值：

* **FULL**： FDM會根據所有限制執行驗證
* **關閉**：沒有驗證
* **BASIC**： FDM會根據&#39;required&#39;和&#39;nullable&#39;條件約束執行驗證

如果未設定`ValidationOptions`標幟的值，則會對輸入資料執行&#x200B;**BASIC**&#x200B;驗證。

下列是將驗證旗標設定為&#x200B;**FULL**&#x200B;的範例：

```java
operationOptions.setValidationOptions(ValidationOptions.FULL);
```

>[!NOTE]
>
>您在輸入資料中為屬性提供的值必須與在中繼資料檔案中為屬性定義的資料型別相符。\
>如果值不符合為屬性定義的資料型別，DermisBridge API會顯示例外狀況，不論`ValidationOptions`旗標的值為何。 如果記錄層級設定為Debug，則會將錯誤記錄到&#x200B;**error.log**&#x200B;檔案。

表單資料模型會根據資料型別限制清單來驗證輸入資料。 輸入資料的限制清單可能會因資料來源而異。

下表根據資料來源列出輸入資料的限制：

<table>
 <tbody> 
  <tr> 
   <td>限制</td> 
   <td>說明</td> 
   <td>輸入資料來源</td> 
  </tr> 
  <tr> 
   <td>必要</td> 
   <td>如果為true，則引數必須包含在輸入資料中。</td> 
   <td>Swagger、WSDL和資料庫</td> 
  </tr> 
  <tr> 
   <td>可為空</td> 
   <td>若為true，則可將輸入資料中的引數值設為Null。</td> 
   <td>WSDL、Odata和資料庫</td> 
  </tr> 
  <tr> 
   <td>最大</td> 
   <td>指定數值的上限。 指定為上限的最大值也可以指派給輸入資料中的引數。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>最小值</td> 
   <td>指定數值的下限。 指定為下限的最小值也可以指定給輸入資料中的引數。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMax</td> 
   <td>指定數值的上限。 指定為上限的最大值不得指派給輸入資料中的引數。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMinimum</td> 
   <td>指定數值的下限。 不得將指定為下限的最小值指派給輸入資料中的引數。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>minlength</td> 
   <td>指定字串中所含字元數的下限。 指定為下限的最小值也可以指定給輸入資料中的引數。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>maxLength</td> 
   <td>指定字串中所含字元數的上限。 指定為上限的最大值也可以指派給輸入資料中的引數。</td> 
   <td>Swagger、WSDL、Odata和資料庫</td> 
  </tr> 
  <tr> 
   <td>圖樣</td> 
   <td>指定固定的字元順序。 只有在字元符合指定的模式時，才能成功驗證輸入字串。</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>minItems</td> 
   <td>指定陣列中專案的最小數目。 指定為下限的最小值也可以指定給輸入資料中的引數。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>maxItems</td> 
   <td>指定陣列中專案的最大數量。 指定為上限的最大值也可以指派給輸入資料中的引數。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueItems</td> 
   <td>如果為true，則陣列的所有元素在輸入資料中必須是唯一的。</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>列舉（字串）<br /> <br /> </td> 
   <td>將輸入資料中的引數值限製為固定的字串值集。 它必須是至少有一個元素的陣列，其中每個元素都是唯一的。</td> 
   <td>Swagger、WSDL和Odata</td> 
  </tr> 
  <tr> 
   <td>列舉（數字）<br /> <br /> </td> 
   <td>將輸入資料中的引數值限製為固定的數值集。 它必須是至少有一個元素的陣列，其中每個元素都是唯一的。</td> 
   <td>WSDL</td> 
  </tr> 
 </tbody> 
</table>

在此範例中，輸入資料會根據Swagger檔案中定義的最大值、最小值和必要限制進行驗證。 只有在存在訂單ID且其值介於1到10之間時，輸入資料才會符合驗證准則。

```json
   parameters: [
   {
   name: "orderId",
   in: "path",
   description: "ID of pet that needs to be fetched",
   required: true,
   type: "integer",
   maximum: 10,
   minimum: 1,
   format: "int64"
   }
   ]
```

如果輸入資料不符合驗證准則，則會顯示例外。 如果記錄層級設定為&#x200B;**Debug**，則會將錯誤記錄到&#x200B;**error.log**&#x200B;檔案。 例如，

```verilog
21.01.2019 17:26:37.411 *ERROR* com.adobe.aem.dermis.core.validation.JsonSchemaValidator {"errorCode":"AEM-FDM-001-044","errorMessage":"Input validations failed during operation execution.","violations":{"/orderId":["numeric instance is greater than the required maximum (maximum: 10, found: 16)"]}}
```

## 後續步驟 {#next-steps}

您有一個工作表單資料模型，現在可用於調適型表單和互動式通訊工作流程。 如需詳細資訊，請參閱[使用表單資料模型](/help/forms/using/using-form-data-model.md)。
