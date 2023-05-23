---
title: 如何使用JEE Workbench上AEM Forms的執行指令碼服務來生成XML資料？
description: 在JEE Workbench上使用AEM Forms中的執行指令碼服務生成XML資料
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# 在JEE Workbench上使用AEM Forms中的執行指令碼服務生成XML資料 {#using-execute-script-service-forms-jee-workbench}

在JEE流程管理工作流中，AEM Forms涉及大量XML，例如：XML資訊可以在流程中構建，併發送到AEM Forms的FlexJEE Workspace應用程式，用於系統設定，或將資訊傳遞到表單和表單。 有許多實例是JEE上的AEM Forms開發人員需要管理XML，而且很多情況下，這要求XML通過AEM Forms的JEE進程進行管理。

處理簡單XML設定時，可使用 `Set Value` 服務，這是JEE服務的預設AEM Forms。 此服務設定流程資料模型中一個或多個資料項的值。 對於非常簡單的條件邏輯「如果這樣，那麼」情形，此服務可以符合目的。

但是，在更複雜的情況下，「設定值」服務沒有那麼有效。 在這些情況下，需要依靠一組更強健的寫程式命令，例如由Java等寫程式語言提供的那些命令。 使用Java生成複雜XML比在「設定值」服務中從簡單文本生成XML文檔簡單得多，也更清晰。 此外，在Java中包含條件寫程式比在Set Value服務中更容易。

## 在進程中使用執行指令碼服務 {#using-execute-script-service-in-process}

在AEM FormsJEE Workbench上提供的關於JEE服務的標準AEM Forms的集合中， `Execute Script` 服務。 此服務允許您在進程中執行指令碼，並提供 `executeScript` 操作。

### 建立「執行指令碼」服務定義為活動的應用程式和進程 {#create-an-application}

在本教程中，總體應用程式和過程建立超出了範圍，但為了本說明的目的，我們建立了一個名為「DemoApplication02」的應用程式。 假定已建立應用程式，則需要在此應用程式中建立進程以調用executeScript服務。 將進程添加到包括 `Execute Script` 服務：

1. 按一下右鍵應用程式並選擇 [!UICONTROL 新建]。 在 [!UICONTROL 新建] 滑出菜單，選擇 [!UICONTROL 進程]。 相應地命名您的流程，如有必要，添加說明，然後選擇要表示此流程的表徵圖。 在本教程中，我們建立了一個進程，並將其命名為  `executeScriptDemoProcess`。
1. 定義起點，或簡單選擇稍後添加起點。
1. 該進程現在已建立，應在 [!UICONTROL 流程設計] 的子菜單。 在此窗口中，按一下「流程設計」窗口頂部的「活動選取器」表徵圖，並將新活動拖到游泳道上。 此時， [!UICONTROL 定義活動窗口] （請參閱下圖）。
   ![定義活動](assets/define-activity.jpg)
1. 可在以下位置找到executeScript服務： `Foundation` 服務集。 服務名稱將對象列為 `Execute Script – 1.0` 具有操作名稱 `executeScript`。 按一下以選擇此項目。
1. 現在應建立此進程，預設情況下， [!UICONTROL 進程屬性] 窗口。

#### 使用「執行指令碼」服務向進程添加指令碼 {#add-script-to-process-with-execute-script}

在定義了「執行指令碼」服務活動的情況下建立進程後，您就可以向該進程添加指令碼。 向此進程添加指令碼：

1. 導航到 [!UICONTROL 進程屬性] 調色板。 在此調色板中，展開 [!UICONTROL 輸入] ，然後按一下「……」表徵圖。

1. 在出現的文本框中編寫指令碼。 編寫指令碼後，按「OK（確定）」（請參閱下圖）。
   ![執行指令碼](assets/execute-script.jpg)

## 使用執行指令碼服務建立XML {#create-xml-execute-script-service}

建立包含執行指令碼服務的進程後，就可以使用此指令碼建立XML。 您可以使用 `Execute Script` 上面的服務部分。

**關於Execute Script Service的技術**

要瞭解執行指令碼服務的能力和局限性，必須瞭解服務的技術基礎。 AEM FormsJEE使用Apache Xerces文檔對象模型(DOM)分析器在進程內建立和儲存XML變數。 Xerces是W3C文檔對象模型規範的Java實現；定義 [這裡](https://dom.spec.whatwg.org/)。 DOM規範是自1998年以來一直採用的XML操作標準。 Xerces的Java實現Xerces-J支援DOM Level 2 1.0版。

用於儲存XML變數的Java類包括：

* org.apache.xerces.dom.NodeImpl和

* org.apache.xerces.dom.DocumentImpl

DocumentImpl是NodeImpl的子類，因此可以假定任何XML進程變數都是NodeImpl派生。 您可以找到NodeImpl的文檔 [這裡](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html)。

**使用Execute Script服務建立XML示例**

下面是在Execute Script服務中建立XML的示例。 進程具有XML類型的變數節點。 此活動的最終結果將是XML文檔。 該文檔的功能，或它如何應用於整個過程，在本教程中是超出範圍的；最終要歸結到XML在整個應用程式中所需要做的。 如導言中所述，XML可用於AEM FormsJEE表單和進程中的許多用途，這只是有關如何對執行指令碼活動進行代碼以輸出簡單XML文檔的說明。

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
>必須將上述DOM對象導入到指令碼中。

此簡單指令碼的結果是新的XML文檔，其變數節點設定為：

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**使用迭代循環向XML添加節點**

節點也可以添加到進程內的現有XML變數。 變數節點包含我們剛建立的XML對象。

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
