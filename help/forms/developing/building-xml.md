---
title: 如何在AEM Forms on JEE Workbench中使用執行指令碼服務來建置XML資料？
description: 使用AEM Forms on JEE Workbench中的執行指令碼服務來建置XML資料
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 0%

---

# 使用AEM Forms on JEE Workbench中的執行指令碼服務來建置XML資料 {#using-execute-script-service-forms-jee-workbench}

JEE流程管理工作流程中的AEM Forms涉及許多XML，例如：XML資訊可在流程中建置並傳送至JEE Workspace上的AEM Forms中的Flex應用程式，用於系統設定，或傳遞資訊至表單或從表單傳送。 在許多情況下，JEE上的AEM Forms開發人員需要管理XML，而且在許多情況下，這要求透過JEE上的AEM Forms管理XML。

處理簡單XML設定時，可以使用`Set Value`服務，這是JEE服務的預設AEM Forms。 此服務會設定流程資料模型中一或多個資料專案的值。 對於簡單的條件邏輯「如果是，則是」情況，此服務可符合其目的。

但是，在更複雜的情況下，「設定值」服務不會那麼有效。 在這些情況下，您必須依賴一組更強大的程式設計指令，例如Java™等程式設計語言所提供的指令。 使用Java™來建置複雜的XML，比使用Set Value服務內的簡單文字建置XML檔案簡單明瞭。 此外，在Java™中納入條件式程式設計比在Set Value服務中更容易。

## 在程式中使用執行指令碼服務 {#using-execute-script-service-in-process}

在AEM Forms on JEE Workbench提供的標準AEM Forms on JEE服務組中，是`Execute Script`服務。 此服務可讓您在執行程式中執行指令碼，並提供要執行此動作的`executeScript`作業。

### 使用定義為活動的「執行指令碼」服務建立應用程式和程式 {#create-an-application}

在本教學課程中，整體應用程式和流程建立不在範圍之內，但就本指示而言，已建立名為「DemoApplication02」的應用程式。 假設應用程式已經建立，您需要在此應用程式中建立程式以呼叫executeScript服務。 若要將處理程式新增至包含`Execute Script`服務的應用程式：

1. 用滑鼠右鍵按一下您的應用程式並選取&#x200B;**[!UICONTROL 新增]**。 在&#x200B;**[!UICONTROL 新增]**&#x200B;滑出功能表中，選取&#x200B;**[!UICONTROL 處理序]**。 為流程命名，視需要新增說明，然後選取要代表此流程的圖示。 出於本教學課程的目的，我們已建立處理序，並將其命名為`executeScriptDemoProcess`。
1. 定義您的起點，或稍後新增起點的簡單選擇。
1. 處理序現在已建立，應該會在[!UICONTROL 處理序設計]視窗中自動開啟。 在此視窗中，按一下「流程設計」視窗頂端的「活動選擇器」圖示，並將新活動拖曳到泳道上。 此時，[!UICONTROL 定義活動視窗]應該會出現（請參閱下圖）。
   ![定義活動](assets/define-activity.jpg)
1. 在`Foundation`組服務下可以找到executeScript服務。 服務名稱將物件列為`Execute Script – 1.0`，作業名稱為`executeScript`。 按一下以選取此專案。
1. 現在應該建立此程式，而且依預設，[!UICONTROL 程式屬性]視窗應該會出現在左邊的窗格中。

#### 使用「執行指令碼」服務將指令碼新增至處理序 {#add-script-to-process-with-execute-script}

使用定義的「執行指令碼」服務活動建立處理序後，就可以將指令碼新增至此處理序。 若要將指令碼新增至此程式：

1. 導覽至[!UICONTROL 處理程式屬性]浮動視窗。 在此調色盤中，展開[!UICONTROL 輸入]區段並按一下「……」圖示。

1. 在出現的文字方塊中寫入您的指令碼。 編寫指令碼後，請按[確定] （請參閱下圖）。
   ![執行指令碼](assets/execute-script.jpg)

## 使用Execute Script Service建立XML {#create-xml-execute-script-service}

一旦建立包含Execute Script服務的處理序後，就可以使用此指令碼來建立XML。 您可以在上述「使用`Execute Script`服務新增指令碼至處理序」一節中所述的文字方塊中撰寫以下所述的指令碼。

**關於執行指令碼服務的技術**

若要瞭解Execute Script服務的功能和限制，必須瞭解服務的技術基礎。 JEE上的AEM Forms使用Apache Xerces檔案物件模型(DOM)剖析器，在程式中建立和儲存XML變數。 Xerces是W3C的[檔案物件模型規格](https://dom.spec.whatwg.org/)的Java™實作。 DOM規格是操作XML的標準方法，自1998年以來就已存在。 Xerces的Java™實作Xerces-J支援DOM Level 2 1.0版。

用來儲存XML變數的Java™類別為：

* org.apache.xerces.dom.NodeImpl和

* org.apache.xerces.dom.DocumentImpl

DocumentImpl是NodeImpl的子類別，因此可以假設任何XML處理變數都是NodeImpl衍生。 如需詳細資訊，請參閱[NodeImpl](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html)的檔案。

**使用執行指令碼服務建立範例XML**

以下是在Execute Script服務中建立XML的範例。 處理序具有型別為XML的變數節點。 此活動的結果為XML檔案。 此檔案有何作用，或如何套用至整個程式，已超出本教學課程的範圍；最終將取決於在整個應用程式中需要XML做什麼。 如簡介中所述，XML可用於AEM Forms中JEE表單和程式的許多用途，這僅是說明如何編寫執行指令碼活動代碼以輸出簡單的XML檔案。

要輸出XML的簡單JavaScript看起來像這樣：

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
>先前提到的DOM物件必須匯入指令碼中。

此簡單指令碼的結果是新XML檔案，其中變數節點設為：

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**使用反複回圈將節點新增到XML**

節點也可以加入至流程中的現有XML變數。 變數（節點）包含已建立的XML物件。

```xml
Document document = patExecContext.getProcessDataValue("/process_data/node");

NodeList childNodes = document.getChildNodes();

int numChildren = childNodes.getLength();

for (int i = 0; i < numChildren; i++)

{

Node currentChild = childNodes.item(i);

if (currentChild.getNodeType() == Node.ELEMENT_NODE)

{

// found the top-level node

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
