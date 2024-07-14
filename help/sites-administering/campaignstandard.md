---
title: 將AEM 6.5與Adobe Campaign Standard整合
description: 瞭解如何將AEM 6.5與Adobe Campaign Standard整合。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 0%

---


# 將AEM 6.5與Adobe Campaign Standard整合 {#integrating-with-adobe-campaign-standard}

將AEM 6.5與Adobe Campaign Standard (ACS)整合後，您可以直接在AEM中管理電子郵件傳送、內容和表單。 需要同時執行Adobe Campaign Standard和AEM的設定步驟，才能在解決方案之間啟用雙向通訊。

此整合可讓AEM和Adobe Campaign Standard獨立使用。 行銷人員可以在Adobe Campaign中建立行銷活動並使用目標定位，而內容建立人員則可以同時在AEM中設計內容。 透過整合，Adobe Campaign可針對在AEM中建立的行銷活動內容和設計進行目標定位和傳遞。

>[!INFO]
>
>本檔案詳細說明如何將Adobe Campaign Standard與AEM 6.5整合。如需其他Campaign整合，請參閱檔案[將AEM 6.5與Adobe Campaign整合。](campaign.md)

## 整合步驟 {#integration-steps}

設定AEM與Adobe Campaign Standard之間的整合需要在這兩個解決方案中執行數個步驟。

1. [設定 ](#aemserver-user)
1. [驗證 ](#resource-type-filter)
1. [在Campaign中建立AEM專屬電子郵件傳遞範本](#aem-email-delivery-template)
1. [在AEM中設定Campaign整合](#campaign-integration)
1. [設定復寫至AEM Publish執行個體的設定](#replication)
1. [設定AEM Externalizer](#externalizer)
1. [設定 ](#campaign-remote-user)
1. [在Campaign中設定AEM外部帳戶](#acc-external-user)

本檔案將詳細介紹每一個步驟。

## 先決條件 {#prerequisites}

* Adobe Campaign Standard的管理員存取權
   * 如果您需要更多有關如何設定和設定Adobe Campaign Standard的詳細資訊，請參閱[Adobe Campaign Standard檔案。](https://experienceleague.adobe.com/docs/campaign-standard/using/campaign-standard-home.html)
* AEM的管理員存取權

## 在Campaign中設定aemserver使用者 {#aemserver-user}

依預設，Adobe Campaign Standard會隨附AEM用來連線至Adobe Campaign的`aemserver`使用者。 為此使用者指派適當的安全性群組並設定其密碼。

1. 以管理員身分登入Adobe Campaign。

1. 按一下功能表列左上方的Adobe Campaign標誌以開啟全域導覽，然後從導覽功能表中選取&#x200B;**管理** > **使用者與安全性** > **使用者**。

1. 按一下使用者主控台中的`aemserver`使用者。

1. 確保至少將`aemserver`使用者指派給已指派角色`deliveryPrepare`的安全性群組。 依預設，群組`Standard Users`具有此角色。

   Adobe Campaign中的![aemserver使用者](assets/acs-aemserver-user.png)

1. 按一下[儲存]儲存變更。****

您的`aemserver`使用者現在擁有必要許可權，讓AEM能夠使用它與Adobe Campaign通訊。

不過，必須先設定密碼，AEM才能使用`aemserver`使用者。 這不能透過Adobe Campaign完成。 必須由Adobe支援工程師執行。 [向Adobe客戶服務](https://experienceleague.adobe.com/?support-tab=home#support)提交票證，以要求重設`aemserver`密碼。 取得Adobe客戶服務的密碼後，請妥善儲存在安全位置。

## 驗證Campaign中的AEMResourceTypeFilter {#resource-type-filter}

`AEMResourceTypeFilter`是Adobe Campaign中的選項，用來篩選可以在Adobe Campaign中使用的AEM資源。 由於AEM包含許多內容，此選項可作為篩選器，允許Adobe Campaign僅擷取特別設計用於Adobe Campaign之型別的AEM內容。

此選項已預先設定。 不過，如果您已自訂AEM的Campaign元件，則可能需要更新。 若要確認已設定`AEMResourceTypeFilter`選項，請遵循下列步驟。

1. 以管理員身分登入Adobe Campaign。

1. 按一下功能表列左上方的Adobe Campaign標誌以開啟全域導覽，然後從導覽功能表中選取&#x200B;**管理** > **應用程式設定** > **選項**。

1. 按一下選項主控台中的`AEMResourceTypeFilter`。

1. 確認`AEMResourceTypeFilter`的設定。 路徑會以逗號分隔，預設包含：

   * `mcm/campaign/components/newsletter`
   * `mcm/campaign/components/campaign_newsletterpage`
   * `mcm/neolane/components/newsletter`

   ![AEMResourceTypeFilter](assets/acs-aem-resource-type-filter.png)

1. 按一下[儲存]儲存變更。****

您的`AEMResourceTypeFilter`現在已設定為從AEM擷取正確的內容。

## 在Campaign中建立AEM專屬電子郵件傳遞範本 {#aem-email-delivery-template}

預設不會在Adobe Campaign的電子郵件範本中啟用AEM。 設定新的電子郵件傳遞範本，以使用AEM內容建立電子郵件。 若要建立AEM專屬電子郵件傳遞範本，請按照下列步驟操作。

1. 以管理員身分登入Adobe Campaign。

1. 按一下功能表列左上方的Adobe Campaign標誌以開啟全域導覽，然後從導覽功能表中選取&#x200B;**資源** > **範本** > **傳遞範本**。

1. 在傳遞範本主控台中，找到預設的電子郵件範本&#x200B;**透過電子郵件（郵件）**，並將滑鼠停留在代表該範本的卡片（或行）上，以顯示選項。 按一下&#x200B;**重複專案**。

   ![重複的元素](assets/acs-copy-template.png)

1. 在&#x200B;**確認**&#x200B;對話方塊中，按一下&#x200B;**確認**&#x200B;以複製範本。

   ![確認對話方塊](assets/acs-confirmation.png)

1. 範本編輯器隨即開啟，其中包含&#x200B;**透過電子郵件（郵件）**&#x200B;範本的復本。 按一下視窗右上角的&#x200B;**編輯屬性**&#x200B;圖示。

   ![範本編輯器](assets/acs-template-editor.png)

1. 在屬性視窗中，將&#x200B;**標籤**&#x200B;欄位變更為新AEM範本的描述性。

1. 按一下「**內容**」標題將其展開，並在「**內容來源**」下拉式清單中選取「**Adobe Experience Manager**」。

1. 這會顯示&#x200B;**Adobe Experience Manager帳戶**&#x200B;欄位。 使用下拉式清單來選取&#x200B;**Adobe Experience Manager執行個體(aemInstance)**&#x200B;使用者。 這是AEM整合的預設外部使用者。

![設定範本屬性](assets/acs-template-properties.png)

1. 按一下&#x200B;**確認**&#x200B;儲存屬性的變更。

1. 在範本編輯器中，按一下&#x200B;**儲存**，儲存您修改過的電子郵件範本復本，以與AEM搭配使用。

您現在已擁有可以使用AEM內容的電子郵件範本。

## 在AEM中設定Campaign整合 {#campaign-integration}

AEM會使用內建整合與您在Adobe Campaign中設定的`aemserver`使用者來與Adobe Campaign通訊。 請依照下列步驟設定這項整合。

1. 以管理員身分登入您的AEM編寫執行個體。

1. 從全域導覽側邊欄中，選取&#x200B;**工具** > **Cloud Service** > **舊版Cloud Service** > **Adobe Campaign**，然後按一下&#x200B;**立即設定**。

   ![設定Adobe Campaign](assets/configure-campaign-service.png)

1. 在對話方塊中，輸入&#x200B;**標題**&#x200B;並按一下&#x200B;**建立**&#x200B;以建立Campaign服務設定。

   ![設定行銷活動對話方塊](assets/configure-campaign-dialog.png)

1. 新視窗和對話方塊會開啟以編輯配置。 提供必要資訊。

   * **使用者名稱** — 這是[您在上一步設定的Adobe Campaign `aemserver`位使用者。](#aemserver-user)預設為`aemserver`。
   * **密碼** — 這是您在上一步中向Adobe客戶服務請求的[Adobe Campaign中`aemserver`使用者的密碼。](#aemserver-user)
   * **API端點** — 這是Adobe Campaign執行個體URL。

   ![在AEM中設定Adobe Campaign](assets/configure-campaign.png)

1. 選取&#x200B;**連線至Adobe Campaign**&#x200B;以驗證連線，然後按一下&#x200B;**確定**。

AEM現在可以與Adobe Campaign通訊。

>[!NOTE]
>
>請確定您的Adobe Campaign伺服器可透過網際網路連線。 AEM無法存取私人網路。

## 設定復寫至AEM Publish執行個體的設定 {#replication}

Campaign內容是由內容作者在AEM編寫執行個體上建立。 此例項通常僅供貴組織內部使用。 為了讓行銷活動的收件者可存取影像和資產等內容，您需要發佈該內容。

復寫代理程式負責將您的內容從AEM製作執行個體發佈至發佈執行個體，且必須設定為讓整合正常運作。 此步驟也是將某些編寫執行個體設定復寫至發佈執行個體所必需的。

若要設定從您的AEM編寫執行個體到發佈執行個體的復寫：

1. 以管理員身分登入您的AEM編寫執行個體。

1. 從全域導覽側邊欄中，選取&#x200B;**工具** > **部署** > **復寫** > **作者上的代理程式**，然後按一下&#x200B;**預設代理程式（發佈）**。

   ![設定復寫代理程式](assets/acc-replication-config.png)

1. 按一下&#x200B;**編輯**，然後選取&#x200B;**傳輸**&#x200B;標籤。

1. 將預設`localhost`值取代為AEM發佈執行個體的IP位址，以設定&#x200B;**URI**&#x200B;欄位。

   ![傳輸標籤](assets/acc-transport-tab.png)

1. 按一下&#x200B;**確定**&#x200B;儲存代理程式設定的變更。

您已設定復寫至AEM發佈執行個體，以便行銷活動收件者可以存取您的內容。

>[!NOTE]
>
>如果您不想使用復寫URL，而是使用公開顯示的URL，您可以透過OSGi在下列組態設定中設定公開URL
>
>從全域導覽側邊欄中，選取&#x200B;**工具** > **作業** > **網頁主控台** > **OSGi設定**，並搜尋&#x200B;**AEM Campaign整合 — 設定**。 編輯設定並變更欄位&#x200B;**公用URL** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`)。

## 設定AEM Externalizer {#externalizer}

[Externalizer](/help/sites-developing/externalizer.md)是AEM中的OSGi服務，可將資源路徑轉換為外部和絕對URL，這是AEM提供Campaign可使用的內容所必需的。 進行設定，讓Campaign整合正常運作。

1. 以管理員身分登入AEM編寫執行個體。
1. 從全域導覽側邊欄中，選取&#x200B;**工具** > **作業** > **網頁主控台** > **OSGi組態**，並搜尋&#x200B;**Day CQ連結外部化器**。
1. 根據預設，**網域**&#x200B;欄位中的最後一個專案是針對發佈執行個體。 將URL從預設`http://localhost:4503`變更為您公開可用的發佈執行個體。

   ![設定外部化程式](assets/acc-externalizer-config.png)

1. 按一下「**儲存**」。

您已設定Externalizer，且Adobe Campaign現在可以存取您的內容。

>[!NOTE]
>
發佈執行個體必須可以從Adobe Campaign伺服器存取。 如果影像指向`localhost:4503`或Adobe Campaign無法連線的其他伺服器，則來自AEM的影像不會出現在Adobe Campaign主控台中。

## 在AEM中設定行銷活動遠端使用者 {#campaign-remote-user}

如同AEM在Adobe Campaign中需要可用來與Adobe Campaign通訊的使用者，Adobe Campaign也需要AEM中的使用者才能與AEM通訊。 根據預設，Campaign整合會在AEM中建立`campaign-remote`使用者。 請依照下列步驟設定此使用者。

1. 以管理員身分登入AEM。
1. 在主導覽主控台上，按一下左側邊欄中的&#x200B;**工具**。
1. 然後按一下[安全性]**** > [使用者]****&#x200B;以開啟使用者管理主控台。
1. 找到`campaign-remote`使用者。
1. 選取`campaign-remote`使用者，然後按一下&#x200B;**屬性**&#x200B;以編輯使用者。
1. 在&#x200B;**編輯使用者設定**&#x200B;視窗中，按一下&#x200B;**變更密碼**。
1. 為使用者提供新密碼，並將密碼記在安全位置以備將來使用。
1. 按一下&#x200B;**儲存**&#x200B;以儲存密碼變更。
1. 按一下&#x200B;**儲存並關閉**&#x200B;以儲存對`campaign-remote`使用者的變更。

## 在Campaign中設定AEM外部帳戶 {#acc-external-user}

當您[建立AEM專屬的電子郵件傳遞範本時，](#aem-email-delivery-template)您指定範本應使用`aemInstance`外部帳戶與AEM通訊。 若要啟用兩個解決方案之間的雙向通訊，您需要在Adobe Campaign中設定此帳戶。

1. 以管理員身分登入Adobe Campaign。

1. 按一下功能表列左上方的Adobe Campaign標誌以開啟全域導覽，然後從導覽功能表中選取&#x200B;**管理** > **應用程式設定** > **外部帳戶**。

1. 按一下使用者主控台中的&#x200B;**Adobe Experience Manager執行個體(aemInstance)**&#x200B;使用者。

1. 確定使用者擁有&#x200B;**Adobe Experience Manager**&#x200B;做為&#x200B;**型別**。

1. 在&#x200B;**連線**&#x200B;區段中，定義下列欄位：

   1. 伺服器：這是您AEM編寫伺服器的URL。 此不應以斜線結尾。
   1. 帳戶：這是您[先前在AEM中設定的`campaign-remote`使用者。](#campaign-remote-user)
   1. 密碼：這是您[先前在AEM中設定之`campaign-remote`使用者的密碼。](#campaign-remote-user)

   ![正在編輯aemInstance使用者](assets/acs-external-acount-editor.png)

1. 確定已選取&#x200B;**已啟用**&#x200B;核取方塊，然後按一下[儲存&#x200B;**]儲存您的變更。**

恭喜！您已完成AEM與Adobe Campaign Standard之間的整合！

## 後續步驟 {#next-steps}

在設定Adobe Campaign Classic和AEM後，整合現已完成。

您現在可以繼續閱讀[此檔案，瞭解如何在Adobe Experience Manager中建立電子報。](/help/sites-authoring/campaign.md)
