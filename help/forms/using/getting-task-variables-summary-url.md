---
title: 獲取摘要URL中的任務變數
seo-title: Getting Task Variables in Summary URL
description: 如何重用有關任務的資訊並生成摘要URL以匯總或描述任務。
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

# 獲取摘要URL中的任務變數 {#getting-task-variables-in-summary-url}

摘要頁面顯示與任務相關的資訊。 本文介紹如何在摘要頁面中重用與任務相關的資訊。

在此業務流程示例中，員工提交休假申請表。 然後，申請表將交給員工的經理審批。

1. 為resourceType建立示例HTML呈現器(html.esp) **員工/PtoApplication**。

   呈現器假定要在節點上設定以下屬性：

   * 名稱
   * 無
   * 原因
   * 持續時間

   >[!NOTE]
   >
   >此呈現器是摘要頁面模板。

   此呈現器的以下示例代碼包含在中：

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

1. 修改業務流程以從提交的表單資料中提取四個屬性。 之後，在CRX中建立類型為 **員工/PtoApplication**，並填充屬性。

   1. 建立進程 **建立PTO匯總** 並將此作為子流程 **分配任務** 業務流程中的操作。
   1. 定義 **employeeName**。 **僱員ID**。 **ptoReason**。 **總天數**, **節點名稱** 作為新進程中的輸入變數。 這些變數將作為已提交的表單資料傳遞。

      還定義輸出變數 **ptoNodePath** 在設定摘要Url時使用。

   1. 在 **建立PTO匯總** 流程，使用 **設定值** 元件以在 **nodeProperty**(**nodeProps**)映射。

      此映射中的鍵應與上一步中HTML呈現器中定義的鍵相同。

      另外，添加 **sling:resourceType** 鍵值 **員工/PtoApplication** 的下界。

   1. 使用子進程 **儲存內容** 從 **內容儲存庫連接器** 服務 **建立PTO匯總** 處理。 此子進程建立CRX節點。

      它需要三個輸入變數：

      * **資料夾路徑**:建立新CRX節點的路徑。 將路徑設定為 **/內容**。
      * **節點名稱**:將輸入變數nodeName分配給此欄位。 這是唯一的節點名稱字串。
      * **節點類型**:將類型定義為 **nt：非結構化**。 此進程的輸出為nodePath。 nodePath是新建立的節點的CRX路徑。 ndoePath將是 **建立PTO** 摘要流程。
   1. 傳遞提交的表單資料(**employeeName**。 **僱員ID**。 **ptoReason**, **總天數**)作為新進程的輸入 **建立PTO匯總**。 將輸出作為 **ptoSummaryNodePath**。


1. 將摘要Url定義為包含伺服器詳細資訊的XPath表達式 **ptoSummaryNodePath**。

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

在AEM Forms工作區中，開啟任務時，摘要Url將訪問CRX節點，HTML呈現器將顯示摘要。

可以更改摘要佈局而不修改流程。 HTML呈現器將相應顯示摘要。
