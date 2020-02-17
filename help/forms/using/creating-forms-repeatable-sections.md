---
title: 使用可重複的區段建立表單
seo-title: 使用可重複的區段建立表單
description: 可重複的區段是可動態新增或移除至表單的面板。
seo-description: 可重複的區段是可動態新增或移除至表單的面板。
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30

---


# 使用可重複的區段建立表單 {#creating-forms-with-repeatable-sections}

可重複的區段是可動態新增或移除至表單的面板。

例如，在申請職務時，求職者會提供先前的雇傭詳細資料，例如公司名稱、職責、專案和其他資訊。 所有雇主的資訊需要不同但相似的部分。 在這種情況下，雇用表提供雇主部分，並提供動態添加更多此類部分的選項。 這些動態添加的節稱為「可重複」節。

您可以使用下列其中一種方法來建立可重複的面板：

## 通過指令碼使用實例管理器 {#using-instance-manager-via-scripts-nbsp}

1. 在編輯模式中，選取面板，然後點選 ![cmppr](assets/cmppr.png)。 在側欄的「屬性」下方，啟用「 **讓面板可重複**」。 指定「最大」和「 **[!UICONTROL 最小]** 」 **[!UICONTROL 欄位的值]** 。

   「最大值」欄位會指定面板在頁面上出現的最大次數。 您可以在「最大計數」欄位中指定-1，讓面板出現無限次數。

   「最小值」欄位會指定面板在表單上出現的次數下限。 如果您將「最小計數」欄位設為零，稍後您就可以在轉譯完成後，透過指令碼移除所有例項。

   >[!NOTE]
   >
   >若要建立非可重複的面板，請將「最大值」和「最小值」欄位的值設為1。 accordion版面不支援「最大計數」欄位中的-1。 您可以指定一個高數來表示無限值的概念。

1. 要重複的面板的父級應包含添加和刪除按鈕，以管理可重複面板的實例。 執行以下步驟，將按鈕插入父項並啟用按鈕上的指令碼：

   1. 從側欄，將按鈕元件拖放至面板的父項。 選取元件並點選 ![編輯規則](assets/edit-rules.png)。 按鈕的規則在規則編輯器中開啟。
   1. 在「規則編輯器」視窗中，按一下「 **建立**」。

      在「表 **單對象和函式** 」行中選擇「可視編輯器」。

      1. 在規則區域的「WHEN」下方，會按一下選取 **狀態**。
      1. 在THEN下：

         * 若要建立新增面板按鈕，請選取「 **新增例項**」，然後使用切換側面板拖放面板 ![，或使用「拖放」物件選取面板](assets/toggle-side-panel.png)**，或在此處選取。**
         * 若要建立刪除面板按鈕，請選取「 **移除例項**」，然後使用切換側面板拖放面板 ![](assets/toggle-side-panel.png)**，或使用「拖放」物件選取面板，或在此處選取。**
      在「表 **單對象和函式** 」行中選擇代碼編輯器。 按一 **下「編輯規則** 」，並在程式碼區域中：

      * 若要建立新增面板按鈕，請指定 `this.panel.instanceManager.addInstance()`
      * 若要建立刪除面板按鈕，請指定 `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`
      按一 **下完成**。

      >[!NOTE]
      >
      >如果欄位屬於可重複面板，則不能在指令碼中使用其名稱直接訪問該面板。 若要存取欄位，請使用中的 `instances` API指定欄位所屬的可重複例項 `InstanceManager`。 在中使用 `instances` API的語 `InstanceManager` 法為：
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >例如，您可建立具有文字方塊的可重複面板的最適化表單。 當您使用三個可重複的文字方塊預先填入表格時，需要下列xml:
      >
      >
      >`<panel1><textbox1>AA1</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA2</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA3</panel1></textbox1>`
      >
      >
      >要讀取AA1資料，請指定：
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >要讀取AA2資料，請指定：
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >如需詳細資訊，請參閱：類別：AEM Forms Java API參考中 [的InstanceManager#instances](https://adobe.com/go/learn_aemforms_documentation_63)。

      >[!NOTE]
      >
      >從最適化表單移除面板的所有例項後，若要新增已移除面板的例項，請使用_panelName語法來擷取面板的例項管理員，並使用例項管理員的addInstance API來新增已刪除的例項。 例如，_panelName.addInstance()。 它會新增移除面板的例項。















## 使用父面板的accordion版面 {#using-the-accordion-layout-for-the-parent-panel-nbsp}

面板有各種版面選項。 針對accordian設計的「版面」選項可立即支援可重複的面板。 使用Layout for accordian設計選項對可重複面板執行以下步驟：

1. 在要重複的面板的父項上，點選 ![cmppr](assets/cmppr.png)。 您可以在側欄中看到屬性。 在「版 **面** 」下拉式清單中，選 **取「Accordion」**。
1. 在要重複的面板上，點選 ![cmppr](assets/cmppr.png)。 您可在側欄中看到面板屬性。 啟用「 **Make Panel Repeatable** 」(使面板重複 **)頁籤，並為「Maximum** 」（最大值）和「Minimum **」（最小值）欄位** 指定值。

   現在，您可以使用加號(+)和刪除( ![delete-panel](assets/delete-panel.png))按鈕來新增和移除面板。

## 從表單範本使用重複子表單(XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

可重複的子表單類似於Adaptive Forms中可重複的面板。 在AEM Forms Designer中，執行下列步驟以建立重複的子表單：

1. 在「階層」浮動視窗中，選取您要重複的子表單的父子表單。
1. 在「物件」浮動視窗中，按一下「子表單」標籤，然後在「內容」清單中選取「溢流」。
1. 選擇要重複的子表單。
1. 在「物件」浮動視窗中，按一下「子表單」標籤，然後在「內容」清單中選取「定位」或「溢位」。
1. 按一下「系結」標籤，並選取「針對每個資料項目重複子表單」。
1. 若要指定最小重複次數，請選取「最小計數」並在相關方塊中輸入數字。 如果此選項設定為0，並且在資料合併時沒有為子表單中的對象提供資料，則在呈現表單時不會放置子表單。
1. 若要指定子表單重複次數的最大數目，請選取「最大」，然後在相關方塊中輸入數字。 如果您未在「最大」方塊中指定值，子表單重複的次數將不限。
1. 若要指定一組子表單重複次數，而不論資料的數量為何，請選取「初始計數」，然後在相關方塊中輸入數字。 如果您選取此選項，且沒有可用的資料或比指定的「初始計數」值少的資料項目，表單上仍會放置子表單的空例項。
1. 在父子表單中添加兩個按鈕——一個用於添加實例，另一個用於刪除可重複子表單的實例。 如需詳細步驟，請參 [閱建立動作](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2)。
1. 現在，將表單範本連結至最適化表單。 如需詳細步驟，請 [參閱「建立以範本為基礎的最適化表單」](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template)。
1. 使用步驟9中建立的按鈕來新增和移除子表單。

附加的。zip檔案包含範例可重複的子表單。

[取得檔案](assets/samplerepeatablesubform.zip)

## 使用XML架構(XSD)的重複設定 {#using-repeat-settings-of-an-xml-schema-xsd-br}

您可以從XML架構和任何複雜類型元素的minOccours &amp; maxOccurs屬性建立可重複的面板。 有關XML架構的詳細資訊，請參 [閱使用XML架構作為表單模型建立自適應表單](/help/forms/using/adaptive-form-xml-schema-form-model.md)。

在下列程式碼中，面 `SampleType`板會使用minOccours &amp; maxOccurs屬性。

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>對於非收合式版面，請使用最適化表單按鈕元件來新增和移除例項。
