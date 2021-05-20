---
title: 在摘要URL中取得任務變數
seo-title: 在摘要URL中取得任務變數
description: 如何重複使用任務的資訊並生成摘要URL以匯總或描述任務。
seo-description: 如何重複使用任務的資訊並生成摘要URL以匯總或描述任務。
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# 在摘要URL {#getting-task-variables-in-summary-url}中獲取任務變數

摘要頁面會顯示與任務相關的資訊。 本文說明如何在摘要頁面中重複使用與任務相關的資訊。

在此示例業務流程中，員工提交了休假申請表。 然後，申請表將提交員工的經理審批。

1. 為resourceType **Employees/PtoApplication**&#x200B;建立示例HTML轉譯器(html.esp)。

   呈現器假設要在節點上設定以下屬性：

   * 名稱
   * empid
   * 原因
   * 持續時間

   >[!NOTE]
   >
   >此轉譯器是摘要頁面範本。

   此轉譯器的下列范常式式碼包含在中：

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

1. 修改協調，從提交的表單資料中擷取四個屬性。 之後，在CRX中建立一個&#x200B;**Employees/PtoApplication**&#x200B;類型的節點，並填入屬性。

   1. 建立流程&#x200B;**建立PTO匯總**，並將此流程用作業務流程中&#x200B;**分配任務**&#x200B;操作之前的子流程。
   1. 將&#x200B;**employeeName**、**employeeID**、**ptoReason**、**totalDays**&#x200B;和&#x200B;**nodeName**&#x200B;定義為新流程中的輸入變數。 這些變數會以提交的表單資料傳遞。

      另外，定義一個輸出變數&#x200B;**ptoNodePath**，該變數將在設定摘要Url時使用。

   1. 在&#x200B;**建立PTO摘要**&#x200B;過程中，使用&#x200B;**set value**&#x200B;元件在&#x200B;**nodeProperty**(**nodeProps**)映射中設定輸入詳細資訊。

      此地圖中的索引鍵應與上一步驟中HTML轉譯器中定義的索引鍵相同。

      此外，在地圖中新增&#x200B;**sling:resourceType**&#x200B;索引鍵，其值為&#x200B;**Employees/PtoApplication**。

   1. 使用&#x200B;**建立PTO摘要**&#x200B;流程中&#x200B;**ContentRepositoryConnector**&#x200B;服務的子進程&#x200B;**storeContent**。 此子進程將建立CRX節點。

      需要三個輸入變數：

      * **資料夾路徑**:建立新CRX節點的路徑。將路徑設定為&#x200B;**/content**。
      * **節點名稱**:將輸入變數nodeName指派給此欄位。這是唯一的節點名稱字串。
      * **節點類型**:將類型定義為 **nt:unstructured**。此過程的輸出為nodePath。 nodePath是新建立節點的CRX路徑。 ndoePath將是&#x200B;**建立PTO**&#x200B;匯總流程的最終輸出。
   1. 將提交的表單資料（**employeeName**、**employeeID**、**ptoReason**&#x200B;和&#x200B;**totalDays**）作為新流程的輸入&#x200B;**建立PTO匯總**。 將輸出作為&#x200B;**ptoSummaryNodePath**。


1. 將摘要Url定義為包含伺服器詳細資訊以及&#x200B;**ptoSummaryNodePath**&#x200B;的XPath表達式。

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

在AEM Forms工作區中，當您開啟任務時，摘要Url會存取CRX節點，而HTML轉譯器會顯示摘要。

無需修改流程，即可更改摘要佈局。 HTML轉譯器會適當顯示摘要。
