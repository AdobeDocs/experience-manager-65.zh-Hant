---
title: 建立具有可重複節的表單
seo-title: Creating forms with repeatable sections
description: 可重複的部分是可動態添加或移除到表單的面板。
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

# 建立具有可重複節的表單 {#creating-forms-with-repeatable-sections}

可重複部分是可動態添加到表單或將其刪除的面板。

例如，在申請工作時，求職者會提供以前的雇傭詳細資訊，如公司名稱、職責、項目和其他資訊。 所有雇主的資訊都需要不同但相似的部分。 在這種情況下，雇傭表格提供了雇主部分，還提供了動態添加更多此類部分的選項。 這些動態添加的節稱為可重複節。

可以使用以下方法之一建立可重複面板：

## 通過指令碼使用實例管理器  {#using-instance-manager-via-scripts-nbsp}

1. 在編輯模式下，選擇一個面板，然後點擊 ![招商](assets/cmppr.png)。 在提要欄中的「屬性」下，啟用 **使面板可重複**。 指定 **[!UICONTROL 最大]** 和 **[!UICONTROL 最小]** 的子菜單。

   「最大」欄位指定面板在頁面上顯示的最大次數。 可以在「最大計數」欄位中指定–1，以允許面板出現無限次。

   「最小」欄位指定面板在窗體上顯示的最小次數。 如果將「最小計數」欄位設定為零，則以後可以在格式副本完成後通過指令碼刪除所有實例。

   >[!NOTE]
   >
   >要建立非可重複面板，請將「最大」和「最小」欄位的值設定為1。 在「最大計數」欄位中，折疊佈局不支援–1。 可以指定一個高數以給出無限值的概念。

1. 要重複的面板的父級應包含「添加」和「刪除」按鈕以管理可重複面板的實例。 執行以下步驟將按鈕插入父級並啟用按鈕上的指令碼：

   1. 從提要欄，將按鈕元件拖放到面板的父級。 選擇元件並點擊 ![編輯規則](assets/edit-rules.png)。 在規則編輯器中開啟按鈕的規則。
   1. 在「規則編輯器」窗口中，按一下 **建立**。

      選擇 **可視編輯器** 的子菜單。

      1. 在規則區域中，在WHEN下，選擇狀態 **按一下**。
      1. 在THEN下：

         * 要建立添加面板按鈕，請選擇 **添加實例**，然後使用 ![切換側面板](assets/toggle-side-panel.png) 或 **刪除對象或選擇此處。**
         * 要建立刪除面板按鈕，請選擇 **刪除實例**，然後使用 ![切換側面板](assets/toggle-side-panel.png) 或 **刪除對象或選擇此處。**

      選擇 **代碼編輯器** 的子菜單。 按一下 **編輯規則** 在代碼區域：

      * 要建立添加面板按鈕，請指定 `this.panel.instanceManager.addInstance()`
      * 要建立刪除面板按鈕，請指定 `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      按一下 **完成**。

      >[!NOTE]
      >
      >如果欄位屬於可重複面板，則不能在指令碼中使用其名稱直接訪問它。 要訪問欄位，請使用 `instances` API在 `InstanceManager`。 使用 `instances` API在 `InstanceManager` 為：
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >例如，可建立具有文本框的可重複面板的自適應表單。 預填入三個可重複的文本框時，需要下面的xml:
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
      >有關詳細資訊，請參閱：類：InstanceManager#實例 [AEM FormsJava API參考](https://adobe.com/go/learn_aemforms_documentation_63)。

      >[!NOTE]
      >
      >從自適應表單中刪除面板的所有實例後，要添加已刪除面板的實例，請使用_panelName語法捕獲面板的實例管理器，並使用實例管理器的addInstance API添加已刪除的實例。 例如，_panelName.addInstance()。 它會添加刪除面板的實例。



## 使用父面板的折疊佈局   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

面板具有各種佈局選項。 「按風格設計的佈局」選項為可重複面板提供了現成的支援。 使用「Layout for accordian design（按照設計的佈局）」選項對可重複面板執行以下步驟：

1. 在要重複的面板的父級上，點擊 ![招商](assets/cmppr.png)。 您可以在邊欄中看到屬性。 在 **佈局** 下拉，選擇 **手風琴**。
1. 在要重複的面板上，點擊 ![招商](assets/cmppr.png)。 您可以在邊欄中看到面板屬性。 啟用 **使面板可重複** ，並指定值 **最大** 和 **最小** 的子菜單。

   現在，可以使用加號(+)和刪除( ![刪除面板](assets/delete-panel.png))按鈕以添加和刪除面板。

## 使用表單模板中的重複子表單(XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

可重複子格式類似於自適應Forms中的可重複面板。 在AEM Forms設計器中，執行以下步驟建立重複子窗體：

1. 在「層次」元件面板中，選擇要重複的子表單的父子表單。
1. 在「對象」調色板中，按一下「子表單」頁籤，然後在「內容」清單中選擇「流」。
1. 選擇要重複的子窗體。
1. 在「對象」調色板中，按一下「子表單」頁籤，然後在「內容」清單中選擇「定位」或「流」。
1. 按一下「綁定」頁籤，然後為每個資料項選擇「重複子表單」。
1. 要指定最小重複次數，請選擇「最小計數」，然後在關聯框中鍵入一個數字。 如果此選項設定為0，並且在資料合併時未為子表單中的對象提供資料，則在呈現表單時不會放置子表單。
1. 要指定子表單重複的最大數量，請選擇「最大」，然後在關聯框中鍵入一個數字。 如果未在「最大」(Max)框中指定值，則子表單重複次數是無限的。
1. 要指定子表單重複的集數，而不管資料數量如何，請選擇「初始計數」，然後在關聯框中鍵入一個數字。 如果選擇此選項，並且沒有可用資料或存在的資料條目少於指定的「初始計數」值，則子窗體的空實例仍會放置在窗體上。
1. 在父子窗體中添加兩個按鈕 — 一個用於添加實例，另一個用於刪除可重複子窗體的實例。 有關詳細步驟，請參見 [生成操作](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2)。
1. 現在，將表單模板連結到自適應表單。 有關詳細步驟，請參見 [基於模板建立自適應表單](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template)。
1. 使用在步驟9中建立的按鈕添加和刪除子表單。

附加的.zip檔案包含可重複的子表單示例。

[取得檔案](assets/samplerepeatablesubform.zip)

## 使用XML架構(XSD)的重複設定 {#using-repeat-settings-of-an-xml-schema-xsd-br}

可以從XML架構和任何複雜類型元素的minOccours &amp; maxOccurs屬性建立可重複面板。 有關XML架構的詳細資訊，請參見 [使用XML架構作為表單模型建立自適應表單](/help/forms/using/adaptive-form-xml-schema-form-model.md)。

在以下代碼中， `SampleType`面板使用minOccours &amp; maxOccurs屬性。

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
>對於非按序佈局，使用自適應表單按鈕元件來添加和刪除實例。
