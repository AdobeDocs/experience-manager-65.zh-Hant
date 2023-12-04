---
title: 如何連線最適化表單資料並將其傳送到Microsoft&reg； Power Automate？
description: 連線最適化表單資料並將其傳送到Microsoft&reg； Power Automate的逐步指南。
keywords: 最適化Forms Microsoft Power Automate，將最適化Forms資料提交至Microsoft Power Automate
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 13%

---


# 連線最適化表單資料並將其提交到Microsoft® Power Automate {#connect-adaptive-form-with-power-automate}

您可以設定最適化表單，在提交時執行 Microsoft® Power Automate Cloud Flow。設定的最適化表單會將擷取的資料、附件和記錄文件傳送到 Power Automate Cloud Flow 進行處理。那有助於建置自訂資料擷取體驗，同時利用 Microsoft® Power Automate 的強大功能，根據擷取的資料建置商業邏輯，並將客戶工作流程自動化。以下是整合最適化表單與 Microsoft® Power Automate 後，可以執行的部分操作範例：

* 在 Power Automate 業務流程中使用最適化表單資料
* 使用 Power Automate 將擷取的資料傳送到 500 多個資料來源或任何公開可用的 API
* 對擷取的資料執行複雜的計算
* 按預定義的排程將最適化表單資料儲存到儲存系統

最適化Forms編輯器提供 **叫用Microsoft®Power Automate流程** 傳送最適化表單資料、附件和記錄檔案的提交動作會傳送到Power Automate雲端流程。 若要使用提交動作將擷取的資料傳送至Microsoft®Power Automate， [將您的AEM Forms編寫執行個體與Microsoft® Power Automate連線](#connect-your-aem-forms-instance-with-microsoft&reg;-power-automate)

## 先決條件

以下為連線最適化表單與Microsoft® Power Automate的必要條件：

* Microsoft® Power Automate Premium授權
* Microsoft® [Power Automate流程](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) 使用 `When an HTTP request is received` 觸發以接受最適化表單提交資料
* 具有的Experience Manager使用者 [Forms Author](/help/forms/using/forms-groups-privileges-tasks.md) 和 [Forms管理員](/help/forms/using/forms-groups-privileges-tasks.md) 許可權
* 用來連線至Microsoft的帳戶®Power Automate是已設定為可從調適型表單接收資料的Power Automate流程的所有者


## 連線您的AEM Forms執行個體與Microsoft® Power Automate {#connect-forms-server-with-power-automate}

執行以下動作，將您的AEM Forms編寫執行個體與Microsoft® Power Automate連線：

1. [建立Microsoft](#ms-power-automate-application)
1. [建立Microsoft](#microsoft-power-automate-dataverse-cloud-configuration)
1. [建立Microsoft](#create-microsoft-power-automate-flow-cloud-configuration)
1. [發佈Microsoft](#publish-microsoft-power-automate-dataverse-cloud-configuration)

### 建立Microsoft® Azure Active Directory應用程式 {#ms-power-automate-application}

1. 登入 [Azure入口網站](https://portal.azure.com/).
1. 選取 [!UICONTROL Azure Active Directory] 從左側導覽。
1. 在「預設目錄」頁面上，選取 [!UICONTROL 應用程式註冊] 從左側面板。
1. 在「應用程式註冊」頁面上，按一下「新註冊」 。
1. 在頁面上指定名稱、支援的帳戶型別和重新導向URI。 在「重新導向URI」中，指定下列專案，然後按一下「儲存」。
   * `https://[AEM Forms Author instance]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[AEM Forms Author instance]/libs/fd/powerautomate/content/flowservice/config.html`

   ![註冊Azure Active Directory應用程式](assets/power-automate-application.png)

   >[!NOTE]
   >如有需要，您也可以從「驗證」頁面指定其他重新導向URI。
   > 對於支援的帳戶型別，請根據您的使用案例選取單一租使用者、多個租使用者或個人Microsoft®帳戶


1. 在「驗證」頁面上，啟用下列選項，然後按一下「儲存」。


   * 存取權杖（用於隱含流程）
   * ID權杖（用於隱含和混合流量）

1. 在API許可權頁面上按一下「新增許可權」 。
1. 在Microsoft® API底下選取流量服務，然後選取以下許可權。
   * Flows.Manage.All
   * Flows.Read.All

   按一下「新增許可權」以儲存許可權。
1. 在API許可權頁面上按一下「新增許可權」 。 選取我的組織使用的API並搜尋 `DataVerse`.
1. 啟用user_impersonation ，然後按一下新增許可權。
1. （選擇性）在「憑證和密碼」頁面上，按一下「新增使用者端密碼」。 在「新增使用者端密碼」畫面上，提供密碼到期的說明和時段，然後按一下「新增」。 產生秘密字串。
1. 記下特定於您的組織的資訊 [動態環境URL](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests).

### 建立Microsoft® Power Automate Dataverse雲端設定 {#microsoft-power-automate-dataverse-cloud-configuration}

1. 在AEM Forms作者例項上，導覽至 **[!UICONTROL 工具]** ![錘子](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**.
1. 在 **[!UICONTROL 設定瀏覽器]** 頁面，選取 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立設定]** 對話方塊，指定 **[!UICONTROL 標題]** 對於設定，啟用 **[!UICONTROL 雲端設定]**，並選取 **[!UICONTROL 建立]**. 這樣便會建立儲存 Cloud Services 的設定容器。請確保資料夾名稱未含任何空格。
1. 瀏覽至 **[!UICONTROL 工具]** ![錘子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate Dataverse]** 然後開啟您在上一步中建立的設定容器。

   >[!NOTE]
   >
   建立最適化表單時，請在 **[!UICONTROL 設定容器]** 欄位。

1. 在設定頁面上，選取 **[!UICONTROL 建立]** 以建立 [!DNL Microsoft®® Power Automate Flow Service] AEM Forms中的設定。
1. 在 **[!UICONTROL 設定Microsoft®® Power Automate的Dataverse服務]** 頁面，指定 **[!UICONTROL 使用者端ID]** （也稱為應用程式ID）、 **[!UICONTROL 使用者端密碼]**， **[!UICONTROL OAuth URL]** 和 **[!UICONTROL 動態環境URL]**. 使用的使用者端ID、使用者端密碼、OAuth URL及動態環境URL [Microsoft® Azure Active Directory應用程式](#ms-power-automate-application) 您在上一節中建立。 在Microsoft® Azure Active Directory應用程式UI中使用端點選項來尋找OAuth URL

   ![使用Microsoft Power Automate應用程式UI中的「端點」選項來尋找OAuth URL](assets/endpoints.png)

1. 選取 **[!UICONTROL 連線]** . 如有要求，請登入您的Microsoft® Azure帳戶。 選取&#x200B;**[!UICONTROL 儲存]**。

### 建立Microsoft® Power Automate流程服務雲端設定 {#create-microsoft-power-automate-flow-cloud-configuration}

1. 瀏覽至 **[!UICONTROL 工具]** ![錘子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate流程服務]** 並開啟您在上一節中建立的設定容器。

   >[!NOTE]
   >
   建立最適化表單時，請在 **[!UICONTROL 設定容器]** 欄位。
1. 在設定頁面上，選取 **[!UICONTROL 建立]** 以建立 [!DNL Microsoft®® Power Automate Flow Service] AEM Forms中的設定。
1. 在 **[!UICONTROL 設定Microsoft®® Power Automate的Dataverse]** 頁面，指定 **[!UICONTROL 使用者端ID]** （也稱為應用程式ID）、 **[!UICONTROL 使用者端密碼]**， **[!UICONTROL OAuth URL]** 和 **[!UICONTROL 動態環境URL]**. 使用使用者端ID、使用者端密碼、OAuth URL和Dynamics環境ID。 在Microsoft® Azure Active Directory應用程式UI中使用端點選項來尋找OAuth URL。 開啟 [我的流程](https://us.flow.microsoft.com) 連結並選取「我的流程」，使用URL中列出的ID作為「動態環境ID」。
1. 選取 **[!UICONTROL 連線]**. 如有要求，請登入您的Microsoft® Azure帳戶。 選取&#x200B;**[!UICONTROL 儲存]**。

### 發佈Microsoft® Power Automate Dataverse和Microsoft® Power Automate流程服務雲端設定 {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. 瀏覽至 **[!UICONTROL 工具]** ![錘子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate Dataverse]** 並開啟您之前建立的設定容器 [建立Microsoft® Power Automate Dataverse雲端設定](#microsoft-power-automate-dataverse-cloud-configuration) 區段。
1. 選取 `dataverse` 設定並選取 **[!UICONTROL 發佈]**.
1. 在發佈頁面上，選取 **[!UICONTROL 所有設定]** 並選取 **[!UICONTROL 發佈]**. 發佈Power Automate Dataverse和Power Automate流程服務雲端設定。

您的AEM Forms作者執行個體現在已與Microsoft® Power Automate連線。 您現在可以將最適化Forms資料傳送到Power Automate流程。

## 使用叫用Microsoft® Power Automate流程提交動作將資料傳送至Power Automate流程 {#use-the-invoke-microsoft-power-automate-flow-submit-action}

在您之後 [將您的AEM Forms編寫執行個體與Microsoft® Power Automate連線](#connect-forms-server-with-power-automate)，執行下列動作來設定您的最適化表單，以在表單提交時傳送擷取的資料至Microsoft®流程。

1. 登入您的Author例項，選取您的Adaptive Form並按一下 **[!UICONTROL 屬性]**.
1. 在設定容器中，瀏覽並選取在區段中建立的容器 [建立Microsoft® Power Automate Dataverse雲端設定](#microsoft-power-automate-dataverse-cloud-configuration)，並選取 **[!UICONTROL 儲存並關閉]**.
1. 開啟最適化表單進行編輯並導覽至 **[!UICONTROL 提交]** 最適化表單容器屬性的區段。
1. 在屬性容器中，針對 **[!UICONTROL 提交動作]** 選取 **[!UICONTROL 叫用Power Automate流程]** 選項。 可用的Power Automate流程清單可在 **[!UICONTROL Power Automate流程]** 選項。 選取所需的流程，並在提交時提交最適化Forms資料。

   ![設定提交動作](assets/submission.png)

>[!NOTE]
>
提交最適化表單前，請確定 `When an HTTP Request is received` 已將具有以下JSON結構描述的觸發程式新增至您的Power Automate流程。

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

## 另請參閱

* [建立最適化表單](create-an-adaptive-form-core-components.md)
* [設定提交動作](configuring-submit-actions.md)
* [Microsoft® Power Automate的Adobe Experience Manager Connector](https://learn.microsoft.com/en-us/connectors/adobeexperiencemanag/)

