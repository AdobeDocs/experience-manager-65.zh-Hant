---
title: 在摘要URL中取得任務變數
description: 如何重複使用任務的資訊，並產生「摘要URL」來摘要或描述任務。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# 在摘要URL中取得任務變數 {#getting-task-variables-in-summary-url}

摘要頁面會顯示工作相關資訊。 本文說明如何在摘要頁面中重複使用工作相關資訊。

在此協調流程範例中，員工會提交休假申請表。 申請表隨後會前往員工的經理進行核准。

1. 為resourseType **Employees/PtoApplication**&#x200B;建立範例HTML轉譯器(html.esp)。

   轉譯器會假設要在節點上設定下列屬性：

   * 列名
   * empid
   * 原因
   * 期間

   >[!NOTE]
   >
   >此轉譯器是摘要頁面範本。

   此轉譯器的下列範常式式碼包含在：

   `apps/Employees/PtoApplication/html.esp`

   ```html
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. 修改協調流程，從提交的表單資料中擷取四個屬性。 之後，在CRX中建立型別&#x200B;**Employees/PtoApplication**&#x200B;的節點，並填入屬性。

   1. 建立處理序&#x200B;**建立PTO摘要**，並在您的協調流程中進行&#x200B;**指派工作**&#x200B;作業之前，將此作為子處理序使用。
   1. 將&#x200B;**employeeName**、**employeeID**、**ptoReason**、**totalDays**&#x200B;和&#x200B;**nodeName**&#x200B;定義為新處理序中的輸入變數。 這些變數將作為提交的表單資料傳遞。

      同時定義設定摘要URL時使用的輸出變數&#x200B;**ptoNodePath**。

   1. 在&#x200B;**建立PTO摘要**&#x200B;程式中，使用&#x200B;**set value**&#x200B;元件來設定&#x200B;**nodeProperty**(**nodeProps**)對應中的輸入詳細資料。

      此對應中的索引鍵應與上一步驟中HTML轉譯器中定義的索引鍵相同。

      此外，在對應中新增值為&#x200B;**Employees/PtoApplication**&#x200B;的&#x200B;**sling：resourceType**&#x200B;機碼。

   1. 在&#x200B;**建立PTO摘要**&#x200B;處理程式中，使用&#x200B;**ContentRepositoryConnector**&#x200B;服務的子處理程式&#x200B;**storeContent**。 此子程式會建立CRX節點。

      它需要三個輸入變數：

      * **資料夾路徑**：建立新CRX節點的路徑。 將路徑設定為&#x200B;**/content**。
      * **節點名稱**：將輸入變數nodeName指派給此欄位。 這是唯一的節點名稱字串。
      * **節點型別**：定義型別為&#x200B;**nt：unstructured**。 此程式的輸出為nodePath。 nodePath是新建立節點的CRX路徑。 ndoePath將會是&#x200B;**建立PTO**&#x200B;摘要程式的最終輸出。

   1. 將提交的表單資料（**employeeName**、**employeeID**、**ptoReason**&#x200B;及&#x200B;**totalDays**）作為輸入傳入新程式&#x200B;**建立PTO摘要**。 將輸出做為&#x200B;**ptoSummaryNodePath**。

1. 將摘要URL定義為包含伺服器詳細資料以及&#x200B;**ptoSummaryNodePath**&#x200B;的XPath運算式。

   XPath： `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`。

在AEM Forms工作區中，當您開啟任務時，摘要URL會存取CRX節點，而HTML轉譯器會顯示摘要。

無需修改流程即可變更摘要版面。 HTML轉譯器會適當地顯示摘要。
