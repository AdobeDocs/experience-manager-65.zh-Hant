---
title: AEM 6.5中的AI助理
description: 使用 AI 助理協助您尋找答案，並針對 Adobe Experience Manager 中提供的解決方案進行疑難排解。
solution: Experience Manager, Experience Manager 6.5
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
autotag-review: '2026-05-18T18:36:07.915Z'
TQID: 'https://experienceleague.adobe.com/dlFmrtn05S20z96wtAfkpGliITeVJhVkofqPix6QMxk'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2:
  - id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1379
ht-degree: 93%

---

# AEM 6.5中的AI助理 {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>未使用 Cloud Manager/Experience Hub 的 AEM 6.5 和 AEM 6.5 LTS 客戶必須聯絡其 Adobe 客戶成功工程師以要求存取 AI 助理。

AEM 6.5/AEM 6.5 LTS中的AI Assistant提供對話式介面，旨在簡化為Adobe Experience Manager相關查詢尋找答案的程式。 其可以幫助您立即獲得與 AEM 產品相關問題之答案 (*適用於所有使用者*)，並自動支援票證建立 (*適用於支援管理員*)。

AI 助理支援 AEM as a Cloud Service，包括下列解決方案：

* Experience Hub 概觀頁面
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


AI 助理會直接嵌入 AEM，並且可透過 AEM Experience Hub、Cloud Manager 和 Author UI 存取。

以下 3 分鐘 25 秒的影片逐步示範操作 AEM 中的 AI 助理。

>[!VIDEO](https://video.tv.adobe.com/v/3475357/?learn=on&enablevpops)

## 在 AEM 中存取 AI 助理{#get-access}

若要在 AEM 存取 AI 助理，客戶必須具備下列條件：

* 在 AEM 中使用 AI 助理以取得產品知識的權限。 此權限可讓您在 AI 助理聊天中詢問產品相關問題。 此權限必須啟用。
* 開啟支援票證的權限，此權限需要&#x200B;**支援管理員**&#x200B;角色。

>[!NOTE]
>
>AEM 中的 AI 助理要求會透過 Adobe Identity Management Services (IMS) 驗證。 如需詳細資訊，請參閱 [Adobe Identity Management 服務概觀](https://www.adobe.com/tw/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf)。

**在 AEM 中存取 AI 助理：**

1. 客戶必須有其他協議就緒才能存取 Adobe Experience Manager 中大部分的 AI 驅動功能和代理式功能。 如需詳細資訊，請聯絡您的 Adobe 代表。

1. 若要在 AEM 中使用 AI 助理，必須擁有透過 AI 助理存取產品知識的權限。 此權限預設為「開啟」。

   如果您想要控制誰可以存取產品知識，請從與您的 Adobe ID 關聯之電子郵件地址寄送電子郵件到 [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com)。 Adobe 可啟用使用者層級存取控制。 啟用後，您的管理員可以按照[在 AEM 中設定 AI 助理](/help/ai-assistant-in-aem-admin.md)中的步驟來授與使用者層級的存取權。


## 範圍 {#scope}

AEM中AI助理的目前範圍著重於解決AEMr as a Cloud Service的產品知識問題。 此範圍包含主要領域的完整支援。<!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **表面**：適用於 AEM Experience Hub、Author UI 和 Cloud Manager。
* **功能**：產品知識以及疑難排解和指引的首站、自動建立支援票證和查詢。
* **價值**：節省時間、加速學習及實現價值、減少手動建立支援票證的需求，並提高建立支援票證的效率。

## 隱私權、安全性和治理{#privacy-security-governance}

AEM 中的 AI 助理之設計特別強調隱私權、安全性和治理。

本文概述 AEM 中的 AI 助理可提供的以信任為中心之功能：

* AEM 中的 AI 助理不會使用任何個人資料，包括培訓用資料。
* AEM 中的 AI 助理無法存取消費者資料。
* 需要明確權限，才能與 AEM 中的 AI 助理互動。
* 使用者提供的提示 (問題、查詢等) 不會與其他客戶共用。

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## 了解 AEM 中的 AI 助理，以取得產品知識和自動化支援票證建立 {#ai-prod-insights}

產品知識包含從 Adobe Experience League 文件衍生的概念和主題。 這些問題可以歸類為以下子群組：


| 產品知識 | 適用於所有使用者<br>範例 |
| :--- | :--- |
| 針對性的學習 | <ul><li>什麼是通用編輯器？</li><li>如何在 Cloud Manager 中建立方案？</li></ul> |
| 開放式探索 | <ul><li>如何使用通用編輯器？</li><li>是否有辦法將內容從一個環境複製到另一個？</li></ul> |
| 疑難排解 | <ul><li>為何無法存取通用編輯器？</li><li>為何我的管道會失敗？</li></ul> |
| **支援票證建立** | **僅適用於支援管理員&#x200B;**<br>**範例** |
| 自動建立支援票證，擷取 AI 助理聊天歷史記錄與內容 | <ul><li>為我建立支援票證。</li></ul> |
| 擷取支援票證的狀態 | <ul><li>顯示我已開啟的所有支援票證。</li><li>顯示票證「E-----------」的狀態</li></ul> |

{style="table-layout:auto"}


## 如何提出有效的問題 {#ai-craft-questions}

若要從 AEM 中的 AI 助理收到最準確的回應，請務必以清楚明瞭的內容表述您的問題。 請使用下列提示來確保您的查詢清楚且結構良好：

* 以簡潔明瞭的方式清楚說明您的任務或問題。
* 為增進理解度，請避免含糊不清的措辭或過於複雜的語法。
* 加入您任務或問題的相關內容，因為此方法有助 AEM 中的 AI 助理提供更精確及相關的答案。
例如，在您的提示中，為您目前使用的 AEM 解決方案命名為 Sites、Assets、Dynamic Media、Edge Delivery Services、Cloud Manager 或 Forms 會有所幫助。

### 不支援的問題範例 {#ai-unsupported-questions}

| 區域 | 範例 |
| --- | --- |
| 運作洞察 | <ul><li>我的租用戶中有多少開發環境？</li><li>誰啟動了最後一個生產管道？</li></ul> |
| 疑難排解 | <ul><li>為何我的生產管道會失敗？</li></ul> |
| 任務與自動化 | <ul><li>為我從開發分支設定程式碼品質管道。</li></ul> |


## 使用 AEM 中的 AI 助理 {#ai-use}

<!--
UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md).
-->


### 在 AEM 對話中開始使用 AI 助理

您可以在 AEM 中重設 AI 助理，並在想要變更主題時開始新對話。 在為失敗的查詢進行疑難排解或提供不正確的資訊時，此功能特別實用。

**在 AEM 對話中開始使用 AI 助理：**

1. 在 AEM 使用者介面 (從 Cloud Manager 頁面或 AEM 環境的作者執行個體) 的右上角附近，按一下&#x200B;**「AI 助理」**&#x200B;圖示。

   ![工具列上的「AI 助理圖示」](/help/assets/assets-ai/ai-assistant-icon.png)

1. 在接近底部的&#x200B;**「AI 助理」**&#x200B;面板文字方塊中，輸入您的問題或提示，然後按 `Enter` 或按一下![「傳送圖示」](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)。

   >[!NOTE]
   >
   >您輸入的內容不應包含個人資料，因為使用此工具並不需要此資料。

   ![位於 AI 助理面板底部的文字方塊](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. 若要開始新交談 (新主題或主題中的變更)，按一下![「更多圖示」](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **「開始新交談」**。

   ![從省略符號圖示在 AI 助理中開始新交談](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### 依類別探索提示

AEM 中的 AI 助理包含可搜尋性功能，能協助您探索支援的主題和類別。

**依類別探索提示：**

1. 在 AI 助理面板中，按一下![「學習圖示」](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)以開啟提示探索面板。

   ![可讓您在 AI 助理中依類別探索提示的面板](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   *顯示 AI 助理提示類別的面板。*

1. 選取類別以檢視相關提示清單。
1. 選取提示以檢視 AI 助理可以回答的問題類型範例。

1. 若要隱藏提示探索面板，請再按一下![「學習圖示」](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)。

### 在 AEM 中分享 AI 助理的意見回饋

您的意見可協助 Adobe 改善 AI 助理，以追求更佳效能和準確性。

透過下列選項，分享您對 AEM 中的 AI 助理體驗之意見回饋：

![按讚、不滿意和檢舉圖示](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| 按一下 | 說明 |
| --- | --- |
| ![按讚線條圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | 指出哪些地方進展順利，並分享正面回饋。 |
| ![不滿意線條圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 提供改進建議。 新增有關您體驗的特定註解，這些註解每天都會審閱。 |
| ![檢舉圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | 報告關於您與 AEM 中的 AI 助理互動的疑慮或提供詳細意見回饋。 |

## 關於 AEM 中的 AI 助理之常見問題 {#ai-faq}

以下是有關 AI 助理的部分常見問題之回答：

* **AEM 中的 AI 助理是否即時提供資訊？**\
  不行。 AI 助理的內容來自於 Adobe Experience League 的文件。 內容的更新可能需要一些時間才能反映在回應中。
* **AEM 中的 AI 助理支援哪些 Adobe 應用程式？**\
  目前，AI助理支援AEM as a Cloud Service中的產品知識查詢，包括Sites、Assets、Dynamic Media、Cloud Manager和Forms。
* **AEM 中的 AI 助理有哪些功能？**\
  AEM中的AI助理可回答與Adobe產品知識相關的查詢。
* **AEM 中的 AI 助理是否將個人資訊用作培訓資料？**\
  不行。 AEM 中的 AI 助理不會將個人資訊用於培訓目的。 避免與 AEM 中的 AI 助理分享您或其他人的個人資訊，包括姓名或聯絡詳細資訊。

<!--
IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

## AEM Forms AI Assistant (Forms Experience Builder) {#ai-forms-builder}

In addition to the general AI Assistant in AEM for product knowledge, AEM offers a specialized **[AEM Forms AI Assistant (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. This enhanced assistant can actively help you create and configure forms through natural language prompts and answer questions specific to forms.

### Key capabilities

The AEM Forms AI Assistant provides:

* **Form Creation**: Create new forms from scratch using natural language descriptions.
* **Design Import**: Convert existing designs (PDF, Figma, images) into functional AEM Forms. 
* **Form Configuration**: Add fields, panels, validation rules, and conditional logic.
* **Layout Management**: Organize form structure and optimize for different devices.
* **Integration Setup**: Configure form submissions and data handling.
* **Product Knowledge**: Answer questions about AEM Forms features and best practices.

### Where to access

The AEM Forms AI Assistant is available in the following:

* **Universal Editor**: For Edge Delivery Services forms with visual editing capabilities.
* **Adaptive Forms Editor**: For detailed form configuration and advanced features.
* **Forms Management UI**: For high-level form creation and management tasks.

### Getting started

>[!NOTE]
>
> The AEM Forms AI Assistant (Forms Experience Builder) is available under the private beta program. Send an email from your work address to [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) to request access.

To learn more about using the AEM Forms AI Assistant , see the [AEM Forms AI Assistant](/help/edge/docs/forms/forms-ai-assistant.md) documentation.

### Example Use Cases

* **"Create a customer feedback form with name, email, rating, and comments fields"**
* **"Convert this uploaded PDF application form into a digital adaptive form"**  
* **"Add conditional logic to show spouse information only when marital status is 'Married'"**
* **"Configure this form to submit data to the Customer Relationship Management system"**

This specialized AEM Forms AI Assistant represents the next evolution in form building, combining the power of AI with AEM's robust forms capabilities to streamline your form creation workflow.
-->
