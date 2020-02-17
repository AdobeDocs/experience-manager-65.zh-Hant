---
title: 在摘要URL中獲取任務變數
seo-title: 在摘要URL中獲取任務變數
description: 如何重複使用有關任務的資訊並生成摘要URL以匯總或描述任務。
seo-description: 如何重複使用有關任務的資訊並生成摘要URL以匯總或描述任務。
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在摘要URL中獲取任務變數 {#getting-task-variables-in-summary-url}

摘要頁面會顯示與任務相關的資訊。 本文說明如何在摘要頁面中重複使用與任務相關的資訊。

在此範例協調中，員工會提交請假申請表。 然後申請表會送至員工的經理進行核准。

1. 為resourcesType Employees/PtoApplication建立示例HTML轉 **換器(html.esp)**。

   渲染器假定要在節點上設定以下屬性：

   * ename
   * empid
   * 原因
   * 持續時間
   **注意**:此轉譯器是摘要頁面範本。

   此轉譯器的下列范常式式碼包含於：

   `apps/Employees/PtoApplication/html.esp`

   ```
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

1. 修改協調，從提交的表單資料中擷取四個屬性。 之後，在CRX中建立 **Employees/PtoApplication類型的節點**，並填充屬性。

   1. 建立流程 **建立PTO匯總** ，並在協調中的「分配任務 **** 」操作之前將其用作子流程。
   1. 在新流 **程中定義employeeName**、employeeID **、** ptoReason **、** Days Name和NodeNameTotalName為輸入變數的employeeName ******** 、employeeID、ptoReason。 這些變數會以提交的表單資料傳遞。

      此外，還定義輸出變數**ptoNodePath **，它將用於設定摘要Url。

   1. 在創 **建PTO匯總流程中** ，使用 **set value** component來設定**nodeProperty **(**nodeProps**)映射中的輸入詳細資訊。

      此地圖中的索引鍵應與前一步驟中HTML轉譯器中定義的索引鍵相同。

      此外，在地圖 **中新增具有值** Employees/PtoApplication **** 的sling:resourceType索引鍵。

   1. 在建立PTO **摘要流程中，使用** ContentRepositoryConnector服務中的子流 **程storeContent****** 。 此子進程將建立CRX節點。

      它需要三個輸入變數：

      * **資料夾路徑**:建立新CRX節點的路徑。 將路徑設為 **/content**。
      * **節點名稱**:將輸入變數nodeName指派給此欄位。 這是唯一的節點名稱字串。
      * **節點類型**:將類型定義為 **nt:unstructured**。 此進程的輸出是nodePath。 nodePath是新建立的節點的CRX路徑。 ndoePath將是建立PTO匯總流程的 **最終輸出** 。
   1. 將提交的表單資料(**employee** Name、 **employee** ID **、** TotalDays Reason和TotalDays ********)作為輸入傳遞至新流程Oracle Process Create PTO SummaryPo。 將輸出作為 **ptoSummaryNodePath**。


1. 將摘要Url定義為包含伺服器詳細資訊以及 **ptoSummaryNodePath的XPath表達式**。

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

在AEM Forms工作區中，當您開啟工作時，摘要Url會存取CRX節點，而HTML轉譯器會顯示摘要。

您可以變更摘要版面，而不需修改程式。 HTML轉譯器會適當顯示摘要。

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
