---
title: 安裝和設定Designer
description: Designer可作為獨立安裝程式提供，且與Workbench搭配。 瞭解如何安裝獨立式Designer。
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin, User, Developer
feature: Forms Designer,Designer
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 4ce52d90f9d3300e543563ce3dc242f28e00912e
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# 安裝和設定Designer{#installing-and-configuring-designer}

## 必要條件 {#pre-requisites}

+++ 若是64位元AEM Forms Designer （建議使用）

* 安裝[Visual C++ 2019可轉散發套件(x64)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)的64位元版本。 在開始安裝之前，請確定已安裝前述的可轉散發執行階段套件。
* 具有管理員許可權的使用者可安裝或解除安裝AEM Forms Designer。

+++

+++ 適用於32位元AEM Forms Designer

* 安裝32位元版本的[Visual C++ 2019可轉散發套件(x64)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)。 在開始安裝之前，請確定已安裝前述的可轉散發執行階段套件。
* 具有管理員許可權的使用者可安裝或解除安裝AEM Forms Designer。

+++

>[!NOTE]
>
>* 64位元版本的設計工具是隨AEM 6.5 Forms Service Pack 19 (6.5.19.0)推出的。
>* 自[AEM Forms Service Pack 21 (6.5.21.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)發行以來，已棄用32位元版本的設計工具。
> * Forms Designer的支援平台與AEM Forms支援的平台一致。 若要瞭解Forms Designer的支援平台，[請按一下這裡](/help/forms/using/aem-forms-jee-supported-platforms.md)。

如需有關安裝Forms Designer的詳細資訊，請造訪[常見問題](#fandq)。

## 安裝AEM Forms Designer {#install-designer}

Designer可作為獨立安裝程式提供，並且與WorkBench搭配。 如果您使用AEM Forms Designer的獨立安裝程式，請執行以下步驟：

1. 解除安裝舊版AEM Forms Designer （如果已經安裝）。
1. 根據您的需求，下載64位元AEM Forms Designer （建議）或32位元AEM Forms Designer 。

   >[!NOTE]
   > 
   >* 32位元Forms Designer預定在AEM 6.5 Forms Service Pack 20 (6.5.20.0)版本中淘汰。 Adobe建議您升級至64位元Forms designer。
   >* 64位元Forms Designer僅適用於AEM 6.5 Forms Service Pack 19 (6.5.19.0)或更新版本。
   >* Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0)之後的Forms Designer版本也包含Service Pack版本。 例如，Service Pack 15的版本編號為6.5.15.20221112.1.0。在此範例中，6.5.15是Service Pack版本。

1. 按兩下setup.exe以啟動AEM Forms Designer安裝程式。
1. 繼續並在Personalization畫面上提供您的詳細資料和序號。

   >[!NOTE]
   >
   >* 從[Adobe授權網站](https://licensing.adobe.com/)取得您的Forms Designer授權金鑰。

1. 如果您接受授權合約，請按[下一步]繼續。
1. （可選）如果您想要在選擇的位置安裝Designer，請變更預設安裝路徑。 按一下「下一步」。
1. 按一下「上一步」以變更任何偏好設定。 若要安裝Designer，請按一下「安裝」。
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
* **案例2**：使用者有6.5.15.0 AEM Forms Designer版本時。

+++**當使用者的AEM Forms Designer版本早於6.5.15.0。**

如果您使用AEM Forms Designer的獨立安裝程式，請執行以下步驟：

1. 在安裝&#x200B;**AEM Forms Designer 6.5.16.0**&#x200B;之前，使用者必須先解除安裝任何舊版。
1. 從AEM表單發行頁面下載並安裝[AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。
1. 成功安裝&#x200B;**AEM Forms Designer 6.5.15.0**&#x200B;後，在下載的安裝程式檔案上按兩下，即可下載並安裝[AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。

+++

+++**當使用者擁有6.5.15.0 AEM Forms Designer版本**

如果您使用AEM Forms Designer的獨立安裝程式，請執行以下步驟：
1. 從[軟體發佈入口網站](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)下載最新版的AEM Forms Designer。
1. 連按兩下下載的安裝程式檔案，安裝最新版的AEM Forms Designer。

+++

## 常見問題 {#fandq}

* **使用者可以直接升級或安裝64位元設計工具嗎？**
   * 是的，使用者可以直接升級或安裝64位元設計工具。 若要升級，請安裝[SP19](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/Designer-Patch/sp19_x64/aemforms_designer_6_5_0_wwe_win.zip)設計工具完整安裝程式，並套用後續設計工具修補程式版本。

     >[!NOTE]
     > 在升級為64位元設計工具之前，請先解除安裝32位元設計工具（如果存在）。

* **使用者是否可以在他們的系統上同時安裝32位元和64位元？**
   * 否，32位元和64位元安裝無法在同一部電腦上運作。 使用者可以有32位元設計工具或64位元設計工具。

* **如何檢查使用者是否使用64位元設計工具或32位元設計工具？**
   * 有兩種方式可檢查Forms Designer版本：

      1. 開啟Designer，前往說明，按一下關於設計工具，您會看到設計工具版本資訊以及位元資訊，例如，您會看到64位元寫入版本結尾處，如下所示：
         `6.5.21.20240522.1.161 | 64 bit`
      1. 開啟Designer，左上角會出現一個品牌圖示，其中包含產品名稱的64位元資訊。