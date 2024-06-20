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

1. 為resourseType建立範例HTML轉譯器(html.esp) **員工/PtoApplication**.

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

1. 修改協調流程，從提交的表單資料中擷取四個屬性。 之後，在CRX中建立型別為的節點 **員工/PtoApplication**，並填入屬性。

   1. 建立流程 **建立PTO摘要** 並將此作為之前 **指派任務** 協調流程中的作業。
   1. 定義 **employeeName**， **employeeid**， **ptoReason**， **totalDays**、和 **nodeName** 作為新程式中的輸入變數。 這些變數將作為提交的表單資料傳遞。

      同時定義輸出變數 **Ptonodepath** ，在設定摘要URL時使用。

   1. 在 **建立PTO摘要** 程式，使用 **設定值** 用來設定輸入詳細資料的元件 **節點屬性**(**nodeProps**)對應。

      此對應中的索引鍵應與上一步驟中HTML轉譯器中定義的索引鍵相同。

      此外，新增 **sling：resourceType** 有值的索引鍵 **員工/PtoApplication** 在地圖中。

   1. 使用子程式 **storeContent** 從 **contentrepositorconnector** 中的服務 **建立PTO摘要** 程式。 此子程式會建立CRX節點。

      它需要三個輸入變數：

      * **資料夾路徑**：建立新CRX節點的路徑。 將路徑設為 **/content**.
      * **節點名稱**：將輸入變數nodeName指派給此欄位。 這是唯一的節點名稱字串。
      * **節點型別**：將型別定義為 **nt：unstructured**. 此程式的輸出為nodePath。 nodePath是新建立節點的CRX路徑。 ndoePath會是 **建立PTO** 摘要程式。

   1. 傳遞提交的表單資料(**employeeName**， **employeeid**， **ptoReason**、和 **totalDays**)作為新程式的輸入 **建立PTO摘要**. 將輸出視為 **Ptosummarynodepath**.

1. 將摘要URL定義為包含伺服器詳細資訊的XPath運算式，以及 **Ptosummarynodepath**.

   XPath： `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

在AEM Forms工作區中，當您開啟任務時，摘要URL會存取CRX節點，而HTML轉譯器會顯示摘要。

無需修改流程即可變更摘要版面。 HTML轉譯器會適當地顯示摘要。
