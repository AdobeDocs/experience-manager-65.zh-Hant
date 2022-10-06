---
title: 在摘要URL中取得任務變數
seo-title: Getting Task Variables in Summary URL
description: 如何重複使用任務的資訊並生成摘要URL以匯總或描述任務。
seo-description: How-to reuse the information about a task and generate a Summary URL to summarize or describe a task.
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# 在摘要URL中取得任務變數 {#getting-task-variables-in-summary-url}

摘要頁面會顯示與任務相關的資訊。 本文說明如何在摘要頁面中重複使用與任務相關的資訊。

在此示例業務流程中，員工提交了休假申請表。 然後，申請表將提交員工的經理審批。

1. 為resourceType建立範例HTML轉譯器(html.esp) **員工/PtoApplication**.

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

1. 修改協調，從提交的表單資料中擷取四個屬性。 之後，在CRX中建立類型的節點 **員工/PtoApplication**，並填入屬性。

   1. 建立程式 **建立PTO匯總** 並在之前使用此子程式 **分配任務** 在協調中運作。
   1. 定義 **employeeName**, **employeeID**, **ptoReason**, **totalDays**，和 **nodeName** 作為新程式的輸入變數。 這些變數會以提交的表單資料傳遞。

      也定義輸出變數 **ptoNodePath** 設定摘要Url時將使用此URL。

   1. 在 **建立PTO匯總** 過程，使用 **設定值** 元件，以在 **nodeProperty**(**nodeProps**)地圖。

      此地圖中的索引鍵應與上一步驟中HTML轉譯器中定義的索引鍵相同。

      此外，新增 **sling:resourceType** 鍵值 **員工/PtoApplication** 在地圖中。

   1. 使用子程式 **storeContent** 從 **ContentRepositoryConnector** 服務 **建立PTO匯總** 程式。 此子進程將建立CRX節點。

      需要三個輸入變數：

      * **資料夾路徑**:建立新CRX節點的路徑。 將路徑設定為 **/content**.
      * **節點名稱**:將輸入變數nodeName指派給此欄位。 這是唯一的節點名稱字串。
      * **節點類型**:將類型定義為 **nt：非結構化**. 此過程的輸出為nodePath。 nodePath是新建立節點的CRX路徑。 ndoePath將是 **建立PTO** 摘要過程。
   1. 傳遞提交的表單資料(**employeeName**, **employeeID**, **ptoReason**，和 **totalDays**)作為新進程的輸入 **建立PTO匯總**. 將輸出作為 **ptoSummaryNodePath**.


1. 將摘要Url定義為包含伺服器詳細資訊的XPath運算式，以及 **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

在AEM Forms工作區中，當您開啟任務時，摘要Url會存取CRX節點，而HTML轉譯器會顯示摘要。

無需修改流程，即可更改摘要佈局。 HTML轉譯器會適當顯示摘要。
