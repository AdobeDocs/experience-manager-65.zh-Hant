---
title: AEM 6.5中的AI助理
description: 使用 AI 助理協助您尋找答案，並針對 Adobe Experience Manager 中提供的解決方案進行疑難排解。
solution: Experience Manager, Experience Manager 6.5
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
source-git-commit: c98a66a4b4be23145334b339a793ded1716e9889
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 4%

---

# AEM 6.5中的AI助理 {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>未使用Cloud Manager/Experience Hub的AEM 6.5和AEM 6.5 LTS客戶必須聯絡其Adobe客戶成功工程師以要求存取AI助理。

AEM 6.5/AEM 6.5 LTS中的AI Assistant提供對話式介面，旨在簡化為Adobe Experience Manager相關查詢尋找答案的程式。 它可協助您即時取得與AEM產品相關問題的解答（*可供所有使用者使用*），並自動建立支援票證（*可供支援管理員使用*）。

AI助理支援AEM as a Cloud Service，包括下列解決方案：

* Experience Hub概觀頁面
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


AI 助理會直接嵌入 AEM，並且可透過 AEM Experience Hub、Cloud Manager 和 Author UI 存取。

以下3分鐘39秒的影片逐步解說AEM中的AI Assistant。

>[!VIDEO](https://video.tv.adobe.com/v/3470354?learn=on)

## 在AEM中存取AI助理{#get-access}

若要授與使用者對AEM中AI助理的存取權，您的Adobe管理員必須為需要在&#x200B;**Adobe Admin Console**&#x200B;中存取的設定檔設定下列自訂許可權：

* **AI助理存取** — 在AEM中使用AI助理以取得產品知識的許可權，可讓使用者在AI助理聊天中詢問產品相關問題。 必須啟用此許可權。
* **支援存取** — 使用者也必須具有開啟支援票證的許可權，這需要&#x200B;**支援管理員**&#x200B;角色。

AEM中的AI助理要求會透過Adobe Identity Management Services (IMS)驗證。 如需詳細資訊，請參閱[Adobe Identity Management服務總覽](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf)。

**若要存取AEM中的AI小幫手：**

1. 客戶必須有其他合約才能存取Adobe Experience Manager中大部分的AI支援和代理程式功能。 如需詳細資訊，請聯絡您的Adobe代表。

<!-- OLD STEP 1 [Customers must sign the Gen AI rider with Adobe](https://fieldreadiness-adobe.highspot.com/items/665f831c9f831b011aeda057#1). 

    The GenAI Rider is a legal agreement between a customer and Adobe, required to use most AI and agentic capabilities. Contact Adobe Customer Care to learn more. -->

1. AEM管理員會設定AI助理以供組織使用。 請參閱[在AEM中設定AI小幫手](/help/ai-assistant-in-aem-admin.md)。

<!--
>[!IMPORTANT]
>Be sure you have reviewed and submitted the user agreement so Adobe can enable the AI Assistant feature for you to test out and participate in the private beta program.
>
>For any questions, send an email to [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) from your email address associated with your Adobe ID. -->

## 範圍 {#scope}

AEM中AI助理目前的範圍著重於解決AEMr as a Cloud Service的產品知識問題。 此範圍包含主要領域的完整支援。<!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **介面**：適用於AEM Experience Hub、作者UI、Cloud Manager。
* **功能**：產品知識以及疑難排解和指引的第一站、自動建立支援票證和查詢。
* **Value**：節省時間、加速學習及創造價值的時間、減少手動建立支援票證的需求，並提高建立支援票證的效率。

## 隱私權、安全性和治理{#privacy-security-governance}

AEM中的AI助理在設計上特別強調隱私權、安全性和治理。

本文概述您可以從AEM的AI助理身上期待的以信任為中心的功能：

* AEM中的AI助理不會使用任何個人資料，包括訓練用資料。
* AEM中的AI助理無法存取消費者資料。
* 需要明確許可權，才能與AEM中的AI助理互動。
* 使用者提供的提示（問題、查詢等）不會與其他客戶共用。

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## 瞭解AEM中的AI助理，以取得產品知識和自動化支援票證建立 {#ai-prod-insights}

產品知識包含從Adobe Experience League檔案衍生的概念和主題。 這些問題可以歸類為以下子群組：


| 產品知識 | 可供所有使用者使用<br>範例 |
| :--- | :--- |
| 點式學習 | <ul><li>什麼是通用編輯器？</li><li>如何在Cloud Manager中建立程式？</li></ul> |
| 開啟探索 | <ul><li>如何使用通用編輯器？</li><li>是否有辦法將內容從一個環境複製到另一個環境？</li></ul> |
| 疑難排解 | <ul><li>為何無法存取通用編輯器？</li><li>我的管道為什麼會失敗？</li></ul> |
| **支援票證建立** | **僅支援管理員&#x200B;**<br>**範例** |
| 自動建立支援票證，擷取AI助理聊天記錄與內容 | <ul><li>為我建立支援票證。</li></ul> |
| 擷取支援票證的狀態 | <ul><li>顯示我已開啟的所有支援票證。</li><li>顯示票證「E-----------」的狀態</li></ul> |

{style="table-layout:auto"}


## 如何製作有效的問題 {#ai-craft-questions}

為了從AEM中的AI助理獲得最準確的回應，請務必以清楚和具體的語境表述您的問題。 使用下列提示來確保您的查詢清晰且結構良好：

* 以簡潔明瞭的方式清楚說明您的任務或問題。
* 請避免含糊不清的措辭或過於複雜的語法，以增進瞭解。
* 加入您任務或問題的相關內容，因為此方法有助於AEM中的AI助理提供更精確且相關的答案。
例如，在您的提示中，為您目前使用的AEM解決方案命名 — Sites、Assets、Dynamic Media、Edge Delivery Services、Cloud Manager或Forms會有所幫助。

### 不支援的問題範例 {#ai-unsupported-questions}

| 區域 | 範例 |
| --- | --- |
| 營運分析 | <ul><li>我的租使用者中有多少開發環境？</li><li>誰啟動了最後一個生產管道？</li></ul> |
| 疑難排解 | <ul><li>為什麼我的生產管道失敗？</li></ul> |
| 工作與自動化 | <ul><li>為我從開發分支設定程式碼品質管道。</li></ul> |


## 在AEM中使用AI助理 {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use the AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in the AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### 在AEM對話中啟動AI助理

您可以在AEM中重設AI助理，並在想要變更主題時開始新對話。 在疑難排解失敗的查詢或提供不正確的資訊時，此功能特別實用。

**若要在AEM交談中啟動AI小幫手：**

1. 在AEM使用者介面(從Cloud Manager頁面或AEM環境的作者執行個體)的右上角附近，按一下&#x200B;**AI助理**&#x200B;圖示。

   工具列上的![AI助理圖示](/help/assets/assets-ai/ai-assistant-icon.png)

1. 在底部附近的&#x200B;**AI小幫手**&#x200B;面板文字方塊中，輸入您的問題或提示，然後按`Enter`或按一下![傳送圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)。

   >[!NOTE]
   >
   >您輸入的內容不應包含個人資料，因為使用此工具並不需要此資料。

   ![文字方塊位於AI助理面板底部](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. 若要開始新交談（新主題或主題中的變更），請按一下![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **開始新交談**。

   ![從省略符號圖示在AI助理中開始新交談](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### 依類別探索提示

AEM中的AI助理包含可發現性功能，可協助您探索支援的主題和類別。

**若要依類別探索提示：**

1. 在AI助理面板中，按一下![學習圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)以開啟提示探索面板。

   ![可讓您在AI助理中依類別探索提示的面板](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   顯示AI助理中提示類別的&#x200B;*面板。*

1. 選取類別以檢視相關提示清單。
1. 選取提示以檢視AI助理可以回答的問題型別範例。

1. 若要隱藏提示探索面板，請再按一下![學習圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)。

### 在AEM中的AI助理上分享您的意見回饋

您的輸入可協助Adobe改善AI Assistant，以獲得更出色的效能和準確性。

透過下列選項，分享您對AEM中AI助理體驗的意見反應：

![豎起大拇指、豎下大拇指和旗標圖示](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| 按一下 | 說明 |
| --- | --- |
| ![向上縮圖圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | 指出哪些專案進展順利，並分享正面回饋。 |
| ![向下縮圖圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 提供改善的建議。 新增有關您體驗的特定註解，這些註解每天都會稽核。 |
| ![標幟圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | 回報關於您與AEM中AI助理互動的疑慮或提供詳細意見回饋。 |

## 關於AEM中AI助理的常見問題 {#ai-faq}

以下是AI助理部分常見問題的解答：

* **AEM中的AI助理是否即時提供資訊？**\
  不行。AI助理從Adobe Experience League檔案取得其內容。 內容的更新可能需要一些時間才能反映在回應中。
* **AEM中的AI助理支援哪些Adobe應用程式？**\
  目前，AI Assistant支援AEM as a Cloud Service中的產品知識查詢，包括Sites、Assets、Dynamic Media、Cloud Manager和Forms。
* **AEM中的AI助理有哪些功能？**\
  AEM中的AI Assistant可回答與Adobe產品知識相關的查詢。
* **AEM中的AI助理是否將個人資訊用於訓練資料？**\
  不行。AEM中的AI助理不會將個人資訊用於訓練目的。 避免與AEM中的AI助理分享您或其他人的個人資訊，包括姓名或聯絡詳細資訊。

<!-- IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

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
