---
title: 使用可重複的區段建立表單
seo-title: Creating forms with repeatable sections
description: 可重複的區段是可動態新增或移除至表單的面板。
seo-description: Repeatable sections are panels that can be dynamically added or removed to a form.
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
feature: Adaptive Forms
exl-id: f2abae0a-f7fd-4a39-bd8c-03492ce06fe9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# 使用可重複的區段建立表單 {#creating-forms-with-repeatable-sections}

可重複的區段是可動態新增或移除至表單的面板。

例如，在申請職務時，求職者提供以前的雇傭詳細資訊，如公司名稱、角色、項目和其他資訊。 所有雇主的資訊需要不同但相似的外觀部分。 在這種情況下，雇傭表提供雇主部分，並提供動態添加更多這樣的部分的選項。 這些動態新增的區段稱為可重複區段。

您可以使用下列其中一種方法來建立可重複的面板：

## 透過指令碼使用Instance Manager  {#using-instance-manager-via-scripts-nbsp}

1. 在編輯模式中，選取面板，然後點選 ![cppr](assets/cmppr.png). 在側欄的「屬性」下，啟用 **讓面板可重複**. 指定 **[!UICONTROL 最大值]** 和 **[!UICONTROL 最低]** 欄位。

   「最大」欄位指定某個面板在頁面上顯示的次數上限。 您可以在「計數上限」欄位中指定–1，讓面板出現無限次。

   「最小值」欄位指定表單上顯示面板的次數下限。 如果您將「最小計數」欄位設為零，之後您就可以在轉譯完成後，透過指令碼移除所有例項。

   >[!NOTE]
   >
   >若要建立非可重複的面板，請將「最大」和「最小」欄位的值設為一。 折疊式功能表配置不支援「最大計數」欄位中的–1。 您可以指定高數字來提供無限值的概念。

1. 要重複的面板父級應包含新增和刪除按鈕，以管理可重複面板的例項。 執行下列步驟以將按鈕插入父級並啟用按鈕上的指令碼：

   1. 從側欄，將按鈕元件拖放至面板的上層。 選取元件並點選 ![編輯規則](assets/edit-rules.png). 按鈕的規則會在規則編輯器中開啟。
   1. 在規則編輯器視窗中，按一下 **建立**.

      選擇 **可視化編輯器** （在「表單對象和函式」行中）。

      1. 在規則區域的「WHEN」下，選擇「state」 **已點按**.
      1. 在THEN下：

         * 要建立添加面板按鈕，請選擇 **新增例項**，並使用 ![切換側面板](assets/toggle-side-panel.png) 或使用 **放置對象或選擇此處。**
         * 若要建立刪除面板按鈕，請選取 **刪除實例**，並使用 ![切換側面板](assets/toggle-side-panel.png) 或使用 **放置對象或選擇此處。**

      選擇 **代碼編輯器** （在「表單對象和函式」行中）。 按一下 **編輯規則** 在代碼區：

      * 要建立添加面板按鈕，請指定 `this.panel.instanceManager.addInstance()`
      * 若要建立刪除面板按鈕，請指定 `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      按一下 **完成**.

      >[!NOTE]
      >
      >如果欄位屬於可重複面板，則無法在指令碼中使用其名稱直接存取它。 若要存取欄位，請使用 `instances` API `InstanceManager`. 使用 `instances` API `InstanceManager` 為：
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >例如，您可以使用具有文字方塊的可重複面板來建立最適化表單。 使用三個可重複的文字方塊預先填入表單時，您需要下列xml:
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
      >如需詳細資訊，請參閱：類別：InstanceManager#instances(在 [AEM Forms Java API參考](https://adobe.com/go/learn_aemforms_documentation_63).

      >[!NOTE]
      >
      >從最適化表單中移除面板的所有例項時，若要新增已移除面板的例項，請使用_panelName語法來擷取面板的例項管理員，並使用例項管理員的addInstance API來新增已刪除的例項。 例如_panelName.addInstance()。 它會新增移除面板的例項。



## 使用父面板的折疊式功能表配置   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

面板有各種版面選項。 可重複面板的「配置用於折疊式設計」選項現成可用。 使用「配置以進行折疊式設計」選項對可重複面板執行以下步驟：

1. 在要重複的面板的上層，點選 ![cppr](assets/cmppr.png). 您可以在側欄中看到屬性。 在 **版面** 下拉式清單，選取 **折疊式功能表**.
1. 在要重複的面板上，點選 ![cppr](assets/cmppr.png). 您可以在側邊欄中看到面板屬性。 啟用 **讓面板可重複** ，並指定 **最大值** 和 **最低** 欄位。

   現在，您可以使用加號(+)和刪除( ![delete-panel](assets/delete-panel.png))按鈕來新增和移除面板。

## 使用表單範本中的重複子表單(XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

可重複的子表單類似於適用性Forms中可重複的面板。 在AEM Forms Designer中，執行下列步驟以建立重複的子表單：

1. 在階層浮動視窗中，選取您要重複之子表單的父子表單。
1. 在「對象」調色板中，按一下子表單頁簽，然後在「內容」清單中，選擇「流」。
1. 選取要重複的子表單。
1. 在「對象」調色板中，按一下「子表單」頁簽，然後在「內容」清單中，選擇「定位」或「流」。
1. 按一下「綁定」頁簽，然後為每個資料項選擇「重複子表單」。
1. 要指定最小重複次數，請選擇「最小計數」，然後在關聯框中鍵入一個數字。 如果此選項設定為0，並且在資料合併時沒有為子表單中的對象提供資料，則在呈現表單時不會放置子表單。
1. 要指定子表單重複次數的最大數，請選擇「最大」，然後在相關框中鍵入一個數字。 如果您未在「最大值」方塊中指定值，子表單重複次數將無限制。
1. 要指定一組子表單重複次數，而不考慮資料數量，請選擇「初始計數」，並在相關框中鍵入數字。 如果您選取此選項，且沒有可用資料或資料項少於指定的「初始計數」值，表單上仍會放置子表單的空例項。
1. 在父子表單中添加兩個按鈕 — 一個用於添加實例，另一個用於刪除可重複子表單的實例。 如需詳細步驟，請參閱 [建立動作](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. 現在，將「表單範本」連結至最適化表單。 如需詳細步驟，請參閱 [根據範本建立最適化表單](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. 使用在步驟9中建立的按鈕來添加和刪除子表單。

附加的.zip檔案包含可重複的子表單範例。

[取得檔案](assets/samplerepeatablesubform.zip)

## 使用XML架構(XSD)的重複設定 {#using-repeat-settings-of-an-xml-schema-xsd-br}

您可以從XML結構，以及任何複雜類型元素的minOccours &amp; maxOccurs屬性建立可重複的面板。 有關XML架構的詳細資訊，請參見 [使用XML結構作為表單模型建立最適化表單](/help/forms/using/adaptive-form-xml-schema-form-model.md).

在下列程式碼中， `SampleType`面板使用minOccours &amp; maxOccurs屬性。

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
>對於非折疊式版面，請使用最適化表單按鈕元件來新增和移除例項。
