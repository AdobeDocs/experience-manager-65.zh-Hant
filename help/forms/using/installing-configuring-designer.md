---
title: 安裝和配置設計工具
seo-title: Installing and configuring Designer
description: Designer是獨立安裝程式，也與Workbench搭配使用。 了解如何安裝獨立設計工具。
seo-description: Designer is available as a stand-alone installer and is also bundled with Workbench. Learn how to install stand-alone Designer.
uuid: c5b779d1-cb6a-48f4-87d6-48464753e516
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f3a5b5ce-2262-4d5d-a8ae-d59a3a4229e7
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: 1b2d743f8f2172c4e4663917d598734cb1ea1ea4
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# 安裝和配置設計工具{#installing-and-configuring-designer}

## 先決條件 {#pre-requisites}

* 安裝32位版本  [Visual C++ 2019可再發行(x86)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). 開始安裝之前，請確定已安裝先前提到的可再分發的執行階段套件。
* 具有管理員權限的使用者，可安裝或解除安裝AEM Forms Designer。

## 安裝AEM Forms Designer {#install-designer}

Designer作為獨立安裝程式提供，並與WorkBench捆綁。 如果您使用AEM Forms Designer的獨立安裝程式，請執行下列步驟：

1. 解除安裝舊版AEM Forms Designer（如果已安裝）。
1. 從下載Designer [Adobe授權網站](https://licensing.adobe.com/).

   >[!NOTE]
   >
   > * Adobe Experience Manager 6.5 Forms Service Pack 15(6.5.15.0)以上的Forms Designer版本也包含Service Pack版本。 例如，對於Service Pack 15，版本號為6.5.15.20221112.1.0。在此示例中，6.5.15是Service Pack版本。


1. 按兩下setup.exe以啟動AEM Forms Designer安裝程式。
1. 繼續，在「個人化」畫面上提供您的詳細資訊和序號。
1. 如果您接受許可協定，請按一下「下一步」以繼續。
1. （可選）如果要在所選位置安裝Designer，請更改預設安裝路徑。 按一下下一步。
1. 按一下「上一步」以變更任何偏好設定。 要安裝設計器，請按一下「安裝」。
1. 安裝完成後，按一下「完成」。

或者，您也可以使用被動或靜默模式，透過命令列安裝AEM Forms Designer。

* 被動命令行安裝：安裝程式將顯示進度欄，該進度欄指示安裝正在進行，但不顯示提示或錯誤消息。 啟動後，無法取消安裝。

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* 靜默命令行安裝：安裝程式會執行安裝，而不顯示使用者介面。 不顯示提示、消息或對話框。 啟動後，無法取消安裝。

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## 更新AEM Forms Designer {#update-forms-designer}

更新AEM Forms Designer 6.5.16.0的最新版本時，有兩種情況：

* **案例1**:當使用者的AEM Forms Designer版本早於6.5.15.0時。
* **案例2**:使用者有6.5.15.0 AEM Forms Designer版本時。

+++**當使用者的AEM Forms Designer版本早於6.5.15.0時。**

如果您使用AEM Forms Designer的獨立安裝程式，請執行下列步驟：

1. 安裝前 **AEM Forms Designer 6.5.16.0**，使用者必須解除安裝任何舊版。
1. 下載並安裝 [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 從AEM表單發行頁面。
1. 成功安裝 **AEM Forms Designer 6.5.15.0**，下載並安裝 [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 按兩下下載的安裝程式檔案，即可執行此作業。

+++

+++**使用者有6.5.15.0 AEM Forms Designer版本時**

如果您使用AEM Forms Designer的獨立安裝程式，請執行下列步驟：
1. 從下載最新版的AEM Forms Designer [軟體發佈門戶](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. 按兩下下載的安裝程式檔案，以安裝最新版的AEM Forms Designer。

+++