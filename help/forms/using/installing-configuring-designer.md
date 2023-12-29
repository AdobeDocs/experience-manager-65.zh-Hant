---
title: 安裝和設定Designer
description: Designer可作為獨立安裝程式提供，且與Workbench搭配。 瞭解如何安裝獨立設計工具。
uuid: c5b779d1-cb6a-48f4-87d6-48464753e516
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
feature: Forms Designer
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: 77615c5b2fe91f7f1b1017e8d40b744facba4158
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 安裝和設定Designer{#installing-and-configuring-designer}

## 先決條件 {#pre-requisites}

+++ 適用於64位元AEM Forms Designer （建議使用）

* 安裝64位元版本的  [Visual C++ 2019可轉散發套件(x64)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). 在開始安裝之前，請確定已安裝前述的可轉散發執行階段套件。
* 具有安裝或解除安裝AEM Forms Designer管理員許可權的使用者。

+++

+++ 適用於32位元AEM Forms Designer

* 安裝32位元版本的  [Visual C++ 2019可轉散發套件(x64)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). 在開始安裝之前，請確定已安裝前述的可轉散發執行階段套件。
* 具有安裝或解除安裝AEM Forms Designer管理員許可權的使用者。

+++


## 安裝AEM Forms Designer {#install-designer}

Designer是獨立安裝程式，也與WorkBench搭配。 如果您使用AEM Forms Designer的獨立安裝程式，請執行以下步驟：

1. 解除安裝舊版AEM Forms Designer （如果已經安裝）。
1. 根據您的需求，下載64位元AEM Forms Designer （建議）或32位元AEM Forms Designer。

   >[!NOTE]
   > 
   >* 32位元Forms Designer預定在AEM 6.5 Forms Service Pack 20 (6.5.20.0)版本中淘汰。 Adobe建議升級至64位元Forms designer。
   >* 64位元Forms Designer僅適用於AEM 6.5 Forms Service Pack 19 (6.5.19.0)或更新版本。
   >* Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0)之後的Forms Designer版本也包含Service Pack版本。 例如，Service Pack 15的版本編號為6.5.15.20221112.1.0。在此範例中，6.5.15是Service Pack版本。

1. 按兩下setup.exe以啟動AEM Forms Designer安裝程式。
1. 繼續並在「個人化」畫面上提供您的詳細資料和序號。

   >[!NOTE]
   >
   >* 從取得您的Forms Designer授權金鑰 [Adobe授權網站](https://licensing.adobe.com/).

1. 如果您接受授權合約，請按[下一步]繼續。
1. （選擇性）如果您要在您選擇的位置安裝Designer，請變更預設安裝路徑。 按一下「下一步」。
1. 按一下「上一步」以變更任何偏好設定。 若要安裝Designer，請按一下[安裝]。
1. 安裝完成時，按一下「完成」。

或者，您也可以使用被動或無訊息模式，透過命令列安裝AEM Forms Designer。

* 被動式命令列安裝：安裝程式會顯示進度列，指出安裝進行中，但不會顯示提示或錯誤訊息。 啟動後，便無法取消安裝。

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* 無訊息命令列安裝：安裝程式執行安裝時不會顯示使用者介面。 不顯示提示、訊息或對話方塊。 啟動後，便無法取消安裝。

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## 更新AEM Forms Designer {#update-forms-designer}

更新最新版AEM Forms Designer 6.5.16.0有兩個情況：

* **案例1**：當使用者的AEM Forms Designer版本早於6.5.15.0時。
* **案例2**：當使用者有6.5.15.0 AEM Forms Designer版本時。

+++**當使用者使用6.5.15.0之前的AEM Forms Designer版本時。**

如果您使用AEM Forms Designer的獨立安裝程式，請執行以下步驟：

1. 安裝之前 **AEM Forms Designer 6.5.16.0**，使用者必須解除安裝任何舊版。
1. 下載並安裝 [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 從AEM Form發行頁面。
1. 成功安裝後 **AEM Forms Designer 6.5.15.0**，下載並安裝 [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 在下載的安裝程式檔案上按兩下。

+++

+++**當使用者有6.5.15.0 AEM Forms Designer版本時**

如果您使用AEM Forms Designer的獨立安裝程式，請執行以下步驟：
1. 從下載最新版AEM Forms Designer [軟體發佈入口網站](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. 連按兩下下載的安裝程式檔案，安裝最新版的AEM Forms Designer。

+++