---
title: 如何使用JEE Workbench上AEM Forms中的執行指令碼服務來建立XML資料？
description: 在JEE Workbench上使用AEM Forms中的執行指令碼服務來建立XML資料
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# 在JEE Workbench上使用AEM Forms中的執行指令碼服務來建立XML資料 {#using-execute-script-service-forms-jee-workbench}

在JEE流程管理工作流程中，AEM Forms涉及許多XML，例如：XML資訊可以在程式中建置，並傳送至JEE工作區上AEM Forms的Flex應用程式，用於系統設定，或傳遞資訊至表單或從表單傳遞。 在許多情況下，JEE上的AEM Forms開發人員都需要管理XML，而許多時候這都需要透過JEE上的AEM Forms程式來管理XML。

處理簡單XML設定時，可使用 `Set Value` 服務，此為JEE服務上的預設AEM Forms。 此服務設定流程資料模型中一個或多個資料項的值。 對於非常簡單的條件式邏輯「如果這樣，那麼就是那樣」的情況，此服務可以符合其目的。

但是，在更複雜的情況下，「設定值」服務並不有效。 在這些情況下，人們需要依賴一組更強健的寫程式命令，例如由Java等寫程式語言提供的命令。 使用Java構建複雜的XML比在「設定值」服務中從簡單文本構建XML文檔更簡單、更清晰。 此外，在Java中加入條件式程式設計比在設定值服務中更容易。

## 在進程中使用執行指令碼服務 {#using-execute-script-service-in-process}

在AEM Forms on JEE Workbench中提供的標準AEM Forms on JEE服務中， `Execute Script` 服務。 此服務可讓您在程式中執行指令碼，並提供 `executeScript` 操作。

### 使用定義為活動的「執行指令碼」服務建立應用程式和進程 {#create-an-application}

本教程不允許建立總體應用程式和進程，但為了本說明，我們已建立了一個名為「DemoApplication02」的應用程式。 假設已建立應用程式，我們需要在此應用程式中建立一個進程，以調用executeScript服務。 將進程添加到包括 `Execute Script` 服務：

1. 以滑鼠右鍵按一下您的應用程式，然後選取 [!UICONTROL 新增]. 在 [!UICONTROL 新增] 滑出菜單，選擇 [!UICONTROL 程式]. 請據以命名您的程式，視需要新增說明，並選取您要代表此程式的圖示。 為了完成本教學課程，我們已建立程式，並將其命名為  `executeScriptDemoProcess`.
1. 定義您的起始點，或簡單選擇稍後新增您的起始點。
1. 程式現在已建立，且應會在 [!UICONTROL 流程設計] 窗口。 在此窗口中，按一下「流程設計」窗口頂部的「活動選擇器」表徵圖，然後將新活動拖動到游泳道上。 此時， [!UICONTROL 定義活動窗口] （請參閱下圖）。
   ![定義活動](assets/define-activity.jpg)
1. 可在 `Foundation` 服務集。 服務名稱將對象列為 `Execute Script – 1.0` 具有操作名稱 `executeScript`. 按一下以選取此項目。
1. 現在應建立此程式，並依預設 [!UICONTROL 進程屬性] 窗口應出現在左側的窗格中。

#### 使用「執行指令碼」服務向進程添加指令碼 {#add-script-to-process-with-execute-script}

在定義了「執行指令碼」服務活動後，您就可以向此進程添加指令碼。 要向此過程添加指令碼，請執行以下操作：

1. 導覽至 [!UICONTROL 進程屬性] 浮動視窗。 在此浮動視窗中，展開 [!UICONTROL 輸入] 區段，然後按一下「……」圖示。

1. 在顯示的文字方塊中，寫入您的指令碼。 已寫入指令碼時，按「OK（確定）」（請參見下圖）。
   ![執行指令碼](assets/execute-script.jpg)

## 使用執行指令碼服務建立XML {#create-xml-execute-script-service}

在建立了包含執行指令碼服務的進程後，就可以使用此指令碼建立XML。 您可以使用 `Execute Script` 服務區段。

**關於執行指令碼服務的技術**

為了了解執行指令碼服務的功能和限制，您必須了解服務的技術基礎。 AEM Forms on JEE使用Apache Xerces檔案物件模型(DOM)剖析器，在處理中建立和儲存XML變數。 Xerces是W3C文檔對象模型規範的Java實現；定義 [此處](https://dom.spec.whatwg.org/). DOM規格是自1998年以來一直採用的XML處理標準方式。 Xerces、Xerces-J的Java實現支援DOM Level 2 1.0版。

用於儲存XML變數的Java類包括：

* org.apache.xerces.dom.NodeImpl和

* org.apache.xerces.dom.DocumentImpl

DocumentImpl是NodeImpl的子類，因此可以假定任何XML進程變數都是NodeImpl派生。 您可以找到NodeImpl的文檔 [此處](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html).

**使用Execute Script服務建立XML的示例**

以下是在Execute Script服務中建立XML的示例。 該進程具有XML類型的變數節點。 此活動的最終結果將是XML文檔。 本教學課程不涵蓋該檔案的功用，或其如何套用至整體程式；最終，這取決於XML在整個應用程式中需要做什麼。 如本簡介所述，XML可在AEM Forms的JEE表單和程式中用於許多用途，這只是如何編寫執行指令碼活動的程式碼以輸出簡單XML檔案的說明。

輸出XML的簡單Java指令碼如下所示：

```xml
import org.apache.xerces.dom.DocumentImpl;

import org.w3c.dom.Document;

import org.w3c.dom.Element;



Document document = new DocumentImpl();

Element topLevelResources = document.createElement("resources");

Element resource = document.createElement("resource");

resource.setAttribute("id", "first item id");

resource.setAttribute("value", "first item value");

topLevelResources.appendChild(resource);

document.appendChild(topLevelResources);

patExecContext.setProcessDataValue("/process_data/node", document);
```

>[!NOTE]
>
>上述DOM物件必須匯入至指令碼中。

此簡單指令碼的結果是新的XML文檔，其變數節點設定為：

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**使用迭代循環向XML添加節點**

節點也可以添加到進程內的現有XML變數中。 變數節點包含我們剛建立的XML對象。

```xml
Document document = patExecContext.getProcessDataValue("/process_data/node");

NodeList childNodes = document.getChildNodes();

int numChildren = childNodes.getLength();

for (int i = 0; i < numChildren; i++)

{

Node currentChild = childNodes.item(i);

if (currentChild.getNodeType() == Node.ELEMENT_NODE)

{

// found the top level node

Element newResource = document.createElement("resource");

newResource.setAttribute("id", "second item id");

newResource.setAttribute("value", "second item value");

currentChild.appendChild(newResource);

break;

}

}

patExecContext.setProcessDataValue("/process_data/node", document);
The variable node in the XML is now set to:

<resources> 

<resource id="first item id" value="first item value"/> 

<resource id="second item id" value="second item value"/> 

</resources>
```
