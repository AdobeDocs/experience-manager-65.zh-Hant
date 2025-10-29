---
title: 啟用功能切換以整合早期採用者和發行前功能
description: 功能切換是AEM中的一項功能，可讓管理員在執行階段環境中啟用新功能。
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
exl-id: 08815c2b-23b3-4545-a3ab-ba47ba1c3c55
source-git-commit: e3901bbcb82b3c05d95b0d2bb8addab049dc3a4e
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---

# Adobe Experience Manager (AEM) 6.5中的功能切換{#enable-feature-toggle-aem-forms-65}

功能切換是AEM中的一項功能，可讓管理員動態啟用或停用特定功能。 此功能特別適合用於管理&#x200B;**早期採用者功能**&#x200B;和&#x200B;**發行前功能**，而不需要主要部署或變更程式碼基底。 它可確保靈活度並控制可在AEM環境中存取的功能。

## 為何要在AEM 6.5設定中使用功能切換？

在AEM 6.5設定中工作時，功能可切換以下協助：

* 安全地測試實驗功能。

* 分階段推出新元件。

* 跨多個環境維護單一程式碼基底。

* 減少部署和升級期間的風險。

## 考量事項

從AEM 6.5 SP23開始，您不需要安裝套件組合[com.adobe.granite.toggle.impl.dev](http://com.adobe.granite.toggle.impl.dev/)，因為它已與Forms附加元件AEM Service Pack一起安裝。

## 先決條件

在AEM 6.5設定中啟用功能切換之前，請確定以下事項：

* 使用者是`forms-users`群組的成員。

* 導覽至`http://<author-instance-url>:portnumber/system/console/bundles`，並檢查&#x200B;**(com.adobe.granite.toggle.impl.dev-1.1.8.jar)**&#x200B;套件組合是否存在。 若不存在，請[從連結](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fcom.adobe.granite.toggle.impl.dev-1.1.8.jar)下載套件。

![功能切換](/help/forms/using/assets/feature-toggle-1.1.8.png)

## 啟用功能切換 {#enable-feature-toggle-65}

早期採用者的功能切換或新功能可透過&#x200B;**AEM Web Console**&#x200B;設定，請遵循下列步驟：

1. 登入您的AEM Forms執行個體。
2. 導覽至 `http://<author-instance-url>:portnumber/system/console/configMgr`。
3. 在Configuration Manager中搜尋&#x200B;**Adobe Granite動態切換提供者**。
4. 按一下圖示![鉛筆圖示](assets/illustratorcc_penciltool_cur_edit_2_17.png)。
5. 在[!UICONTROL 已啟用的切換]區段中，按一下![鉛筆圖示](assets/aem6forms_add.png)。
6. 新增功能的功能切換ID，如下圖所示。
   ![新增切換](assets/add_toggle_number_forms.png)

   >[!NOTE]
   >
   >您可在檔案中找到早期採用者功能的特定功能切換ID。

7. 按一下「儲存」。

## 停用功能切換 {#disable-feature-toggle-65}

若要針對已啟用切換功能的功能停用功能切換，請遵循下列步驟：

1. 登入您的AEM Forms執行個體。
2. 導覽至 `http://<author-instance-url>:portnumber/system/console/configMgr`。
3. 在Configuration Manager中搜尋&#x200B;**Adobe Granite動態切換提供者**。
4. 按一下圖示![鉛筆圖示](assets/illustratorcc_penciltool_cur_edit_2_17.png)。
5. 在[!UICONTROL 已停用的切換]區段中，按一下![鉛筆圖示](assets/aem6forms_add.png)。
6. 為要停用的功能新增切換號碼。
   ![移除切換](assets/remove_toggle_feature_forms.png)
7. 按一下「儲存」。

## 技術考量

功能切換是特定於環境的，在執行階段進行管理，因此不需要重新啟動伺服器。 不過，有些功能可能需要重新整理相關頁面或清除快取以反映變更。
您可以透過`http://<author-instance-url>:4502/etc.clientlibs/toggles.json`存取透過功能切換為您的環境啟用的功能清單。
