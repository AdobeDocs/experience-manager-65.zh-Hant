---
title: 啟用功能切換以整合早期採用者和發行前功能
description: 功能切換是AEM中的一項功能，可讓管理員在執行階段環境中啟用新功能。
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
source-git-commit: 794d93d890ba752f9036a85831f7cbc8391fb545
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 2%

---

# Adobe Experience Manager (AEM) 6.5中的功能切換{#enable-feature-toggle-aem-forms-65}

功能切換是AEM中的一項功能，可讓管理員動態啟用或停用特定功能。 此功能特別適合用於管理&#x200B;**早期採用者功能**&#x200B;和&#x200B;**發行前功能**，而不需要主要部署或變更程式碼基底。 它可確保靈活度並控制可在AEM環境中存取的功能。

## 啟用功能切換 {#enable-feature-toggle-65}

早期採用者的功能切換或新功能可以透過&#x200B;**AEM Web Console**&#x200B;設定，請遵循下列步驟：

1. 登入您的AEM Forms執行個體。
2. 導覽至 `http://<author-instance-url>:portnumber/system/console/configMgr`。
3. 在Configuration Manager中搜尋&#x200B;**AdobeGranite動態切換提供者**。
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
3. 在Configuration Manager中搜尋&#x200B;**AdobeGranite動態切換提供者**。
4. 按一下圖示![鉛筆圖示](assets/illustratorcc_penciltool_cur_edit_2_17.png)。
5. 在[!UICONTROL 已停用的切換]區段中，按一下![鉛筆圖示](assets/aem6forms_add.png)。
6. 為要停用的功能新增切換號碼。
   ![移除切換](assets/remove_toggle_feature_forms.png)
7. 按一下「儲存」。

## 技術考量

功能切換是特定於環境的，在執行階段進行管理，因此不需要重新啟動伺服器。 不過，有些功能可能需要重新整理相關頁面或清除快取以反映變更。
您可以透過`http://<author-instance-url>:4502/etc.clientlibs/toggles.json`存取透過功能切換為您的環境啟用的功能清單。