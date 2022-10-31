---
title: 與Adobe Campaign Standard整合
seo-title: Integrating with Adobe Campaign Standard
description: 了解如何整合AEM與Adobe Campaign Standard。
seo-description: Learn how to integrate AEM with Adobe Campaign Standard.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
source-git-commit: a0062ffbdd6477eca494fea4142d271f3015599a
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 0%

---


# 與Adobe Campaign Standard整合 {#integrating-with-adobe-campaign-standard}

將AEM與Adobe Campaign整合後，您就可以直接在AEM中管理電子郵件傳遞、內容和表單。 需要Adobe Campaign Standard和AEM中的設定步驟，才能啟用解決方案之間的雙向通訊。

此整合可讓AEM和Adobe Campaign Standard獨立使用。 行銷人員可在Adobe Campaign中建立行銷活動及使用鎖定目標，而內容建立者可同時在AEM中進行內容設計。 透過整合，Adobe Campaign可定位並傳送在AEM中建立之促銷活動的內容與設計。

## 整合步驟 {#integration-steps}

設定AEM和Adobe Campaign Standard之間的整合需要兩個解決方案中的許多步驟。

1. [設定 ](#aemserver-user)
1. [驗證 ](#resource-type-filter)
1. [在Campaign中建立AEM專屬的電子郵件傳送範本](#aem-email-delivery-template)
1. [在AEM中設定Campaign整合](#campaign-integration)
1. [設定復寫至AEM發佈執行個體](#replication)
1. [設定AEM Externalizer](#externalizer)
1. [設定 ](#campaign-remote-user)
1. [在Campaign中設定AEM外部帳戶](#acc-external-user)

本檔案會詳細引導您完成這些步驟。

## 必備條件 {#prerequisites}

* 管理員存取Adobe Campaign Standard
   * 若您需要有關如何設定和設定Adobe Campaign Standard的其他詳細資訊，請參閱 [Adobe Campaign Standard檔案。](https://experienceleague.adobe.com/docs/campaign-standard/using/campaign-standard-home.html)
* 管理員AEM存取權

## 在Campaign中設定aemserver使用者 {#aemserver-user}

Adobe Campaign Standard預設會隨 `aemserver` AEM用來連線至Adobe Campaign的使用者。 必須為此用戶分配適當的安全組並設定其密碼。

1. 以管理員身分登入Adobe Campaign。

1. 點選或按一下功能表列左上方的Adobe Campaign標誌，以開啟全域導覽，然後選取 **管理** > **使用者與安全性** > **使用者** 的下一頁。

1. 點選或按一下 `aemserver` 使用者。

1. 確保 `aemserver` 至少將用戶分配給具有角色的安全組 `deliveryPrepare` 已指派給它。 依預設，群組 `Standard Users` 有這個角色。

   ![Adobe Campaign的aemserver使用者](assets/acs-aemserver-user.png)

1. 點選或按一下 **儲存** 以儲存變更。

您的 `aemserver` 使用者現在擁有必要的權限，AEM才能使用它與Adobe Campaign通訊。

不過，在AEM可以使用 `aemserver` 用戶，必須設定其密碼。 這無法透過Adobe Campaign完成。 必須由Adobe支援工程師執行。 [請向Adobe客戶服務提出票證](https://experienceleague.adobe.com/?support-tab=home#support) 請求重設 `aemserver` 密碼。 一旦您收到Adobe客戶服務的密碼，請將其保留在安全位置。

## 驗證Campaign中的AEMResourceTypeFilter {#resource-type-filter}

此 `AEMResourceTypeFilter` 是Adobe Campaign中的選項，可用來篩選可在Adobe Campaign中使用的AEM資源。 由於AEM包含許多內容，此選項可作為篩選器，讓Adobe Campaign只能擷取專為在Adobe Campaign中使用而設計的類型的AEM內容。

此選項已預先設定。 不過，如果您已自訂AEM的Campaign元件，則可能需要更新它。 驗證 `AEMResourceTypeFilter` 選項，請依照下列步驟操作。

1. 以管理員身分登入Adobe Campaign。

1. 點選或按一下功能表列左上方的Adobe Campaign標誌，以開啟全域導覽，然後選取 **管理** > **應用程式設定** > **選項** 的下一頁。

1. 點選或按一下 `AEMResourceTypeFilter` 在選項控制台中。

1. 確認 `AEMResourceTypeFilter`. 路徑會以逗號分隔，且依預設會包含：

   * `mcm/campaign/components/newsletter`
   * `mcm/campaign/components/campaign_newsletterpage`
   * `mcm/neolane/components/newsletter`

   ![AEMResourceTypeFilter](assets/acs-aem-resource-type-filter.png)

1. 點選或按一下 **儲存** 以儲存變更。

您的 `AEMResourceTypeFilter` 現在已設定為從AEM擷取正確的內容。

## 在Campaign中建立AEM專屬的電子郵件傳送範本 {#aem-email-delivery-template}

依預設，AEM不會在Adobe Campaign的電子郵件範本中啟用。 您必須設定新的電子郵件傳送範本，以便使用AEM內容建立電子郵件。 若要建立AEM專用的電子郵件傳送範本，請遵循下列步驟。

1. 以管理員身分登入Adobe Campaign。

1. 點選或按一下功能表列左上方的Adobe Campaign標誌，以開啟全域導覽，然後選取 **資源** > **範本** > **傳遞範本** 的下一頁。

1. 在傳送範本主控台中，找出預設的電子郵件範本 **透過電子郵件（郵件）傳送** 將滑鼠移至代表該資訊卡的資訊卡（或折線）上，即可顯示選項。 按一下 **重複元素**.

   ![重複元素](assets/acs-copy-template.png)

1. 在 **確認** 對話框，按一下 **確認** 複製範本。

   ![確認對話方塊](assets/acs-confirmation.png)

1. 範本編輯器隨即開啟，其中會顯示 **透過電子郵件（郵件）傳送** 範本。 按一下 **編輯屬性** 圖示。

   ![範本編輯器](assets/acs-template-editor.png)

1. 在「屬性」窗口中，更改 **標籤** 欄位來描述新AEM範本。

1. 按一下 **內容** 展開並選取 **Adobe Experience Manager** 在 **內容來源** 下拉式清單。

1. 如此可顯示 **Adobe Experience Manager帳戶** 欄位。 使用下拉式清單來選取 **Adobe Experience Manager例項(aemInstance)** 使用者。 這是AEM整合的預設外部使用者。

![配置模板屬性](assets/acs-template-properties.png)

1. 按一下 **確認** 以儲存屬性的變更。

1. 在範本編輯器中，按一下 **儲存** 儲存已修改的電子郵件範本副本以與AEM搭配使用。

您現在有可使用AEM內容的電子郵件範本。

## 在AEM中設定Campaign整合 {#campaign-integration}

AEM使用內建整合與 `aemserver` 您在Adobe Campaign中設定的使用者。 請依照下列步驟來設定此整合。

1. 以管理員身分登入AEM製作執行個體。

1. 在全域導覽側邊欄中，選取 **工具** > **Cloud Services** > **舊版Cloud Services** > **Adobe Campaign**，然後按一下 **立即配置**.

   ![設定Adobe Campaign](assets/configure-campaign-service.png)

1. 在對話方塊中，輸入 **標題** 按一下 **建立**.

   ![設定Campaign對話方塊](assets/configure-campaign-dialog.png)

1. 將開啟新窗口和對話框以編輯配置。 提供必要的資訊。

   * **使用者名稱**  — 這是 [the `aemserver` 在Adobe Campaign中的使用者。](#aemserver-user) 預設為 `aemserver`.
   * **密碼**  — 這是 [the `aemserver` 使用者(在Adobe Campaign中)。](#aemserver-user)
   * **API端點**  — 這是Adobe Campaign執行個體URL。

   ![在AEM中設定Adobe Campaign](assets/configure-campaign.png)

1. 選擇 **連線至Adobe Campaign** 驗證連接，然後按一下 **確定**.

AEM現在可與Adobe Campaign通訊。

>[!NOTE]
>
>請確定您的Adobe Campaign伺服器可透過網際網路存取。 AEM無法存取專用網路。

## 設定復寫至AEM發佈執行個體 {#replication}

促銷活動內容是由內容作者在AEM製作例項上建立。 此例項通常僅供貴組織內部使用。 若要讓行銷活動的收件者存取影像和資產等內容，您需要發佈該內容。

復寫代理負責將您的內容從AEM製作例項發佈至發佈例項，且必須進行設定，整合才能正常運作。 若要將某些製作執行個體設定複製到發佈執行個體，也必須執行此步驟。

若要設定從AEM製作執行個體到發佈執行個體的復寫：

1. 以管理員身分登入AEM製作執行個體。

1. 在全域導覽側邊欄中，選取 **工具** > **部署** > **復寫** > **作者代理**，然後點選或按一下 **預設代理（發佈）**.

   ![配置複製代理](assets/acc-replication-config.png)

1. 點選或按一下 **編輯** 然後選取 **運輸** 標籤。

1. 設定 **URI** 欄位，取代預設值 `localhost` 值與AEM發佈執行個體的IP位址。

   ![傳輸標籤](assets/acc-transport-tab.png)

1. 點選或按一下 **確定** 以保存對代理設定的更改。

您已設定到AEM發佈執行個體的復寫，讓您的行銷活動收件者可以存取您的內容。

>[!NOTE]
>
>如果您不想使用復寫URL，而是使用公開的URL，您可以透過OSGi在下列組態設定中設定公用URL
>
>在全域導覽側邊欄中，選取 **工具** > **操作** > **Web主控台** > **OSGi配置** 和搜索 **AEM Campaign整合 — 設定**. 編輯設定並變更欄位 **公用URL** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`)。

## 設定AEM Externalizer {#externalizer}

[Externalizer](/help/sites-developing/externalizer.md) 是AEM中的OSGi服務，可將資源路徑轉換為外部和絕對URL，這是AEM提供Campaign可使用的內容所必要的。 您必須進行設定，Campaign整合才能運作。

1. 以管理員身分登入AEM製作執行個體。
1. 在全域導覽側邊欄中，選取 **工具** > **操作** > **Web主控台** > **OSGi配置** 和搜索 **Day CQ link Externalizer**.
1. 依預設， **網域** 欄位適用於發佈例項。 將URL從預設值變更為 `http://localhost:4503` 至您公開可用的發佈例項。

   ![配置外部化程式](assets/acc-externalizer-config.png)

1. 點選或按一下 **儲存**.

您已設定Externalizer，而Adobe Campaign現在可以存取您的內容。

>[!NOTE]
必須可從Adobe Campaign伺服器存取發佈執行個體。 如果指向 `localhost:4503` 或Adobe Campaign無法存取的其他伺服器，來自AEM的影像將不會顯示在Adobe Campaign主控台中。

## 在AEM中設定campaign-remote使用者 {#campaign-remote-user}

如同您需要Adobe Campaign中可供AEM用來與Adobe Campaign通訊的使用者，Adobe Campaign也需要AEM中的使用者才能與AEM通訊。 依預設，Campaign整合會建立 `campaign-remote` 使用者。 請依照下列步驟來設定此使用者。

1. 以管理員身分登入AEM。
1. 在主導覽主控台上，按一下 **工具** 在左側邊欄。
1. 然後按一下 **安全性** > **使用者** 以開啟使用者管理控制台。
1. 找出 `campaign-remote` 使用者。
1. 選取 `campaign-remote` 使用者，按一下 **屬性** 來編輯用戶。
1. 在 **編輯使用者設定** 按一下 **更改密碼**.
1. 為用戶提供新密碼，並在安全位置記下密碼，以備將來使用。
1. 按一下 **儲存** 保存密碼更改。
1. 按一下 **儲存並關閉** 儲存 `campaign-remote` 使用者。

## 在Campaign中設定AEM外部帳戶 {#acc-external-user}

當您 [已建立AEM專屬的電子郵件傳送範本，](#aem-email-delivery-template) 您指定範本應使用 `aemInstance` 與AEM通訊的外部帳戶。 若要啟用這兩個解決方案之間的雙向通訊，您必須在Adobe Campaign中設定此帳戶。

1. 以管理員身分登入Adobe Campaign。

1. 點選或按一下功能表列左上方的Adobe Campaign標誌，以開啟全域導覽，然後選取 **管理** > **應用程式設定** > **外部帳戶** 的下一頁。

1. 點選或按一下 **Adobe Experience Manager例項(aemInstance)** 使用者。

1. 確認使用者已 **Adobe Experience Manager** 作為 **類型**.

1. 在 **連線** 區段，定義下列欄位：

   1. 伺服器：這是AEM製作伺服器的URL。 此結尾不應為斜線。
   1. 帳戶：這是 `campaign-remote` 使用者 [先前在AEM中設定。](#campaign-remote-user)
   1. 密碼：這是 `campaign-remote`使用者 [先前在AEM中設定。](#campaign-remote-user)

   ![編輯aemInstance使用者](assets/acs-external-acount-editor.png)

1. 確保 **已啟用** 核取方塊，然後按一下 **儲存** 來儲存變更。

恭喜！您已完成AEM與Adobe Campaign Standard的整合！

## 後續步驟 {#next-steps}

同時設定Adobe Campaign Classic和AEM後，整合現在已完成。

您現在可以繼續使用，了解如何在Adobe Experience Manager中建立電子報 [此文檔。](/help/sites-authoring/campaign.md)
