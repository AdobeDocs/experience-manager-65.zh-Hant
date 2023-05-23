---
title: 安裝和配置設計器
seo-title: Installing and configuring Designer
description: 設計器作為獨立安裝程式提供，也與Workbench捆綁在一起。 瞭解如何安裝獨立設計器。
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

# 安裝和配置設計器{#installing-and-configuring-designer}

## 先決條件 {#pre-requisites}

* 安裝32位版本  [Visual C++ 2019可再發行版(x86)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)。 在開始安裝之前，請確保已安裝上述可再發行運行時軟體包。
* 具有安裝或卸載AEM Forms設計器的管理員權限的用戶。

## 安裝AEM Forms設計器 {#install-designer}

設計器可作為獨立安裝程式使用，也與WorkBench捆綁在一起。 如果正在為AEM Forms設計器使用獨立安裝程式，請執行以下步驟：

1. 卸載以前版本的AEM Forms設計器（如果已安裝）。
1. 從下載設計器 [Adobe許可網站](https://licensing.adobe.com/)。

   >[!NOTE]
   >
   > * Adobe Experience Manager6.5FormsService Pack 15(6.5.15.0)以後的Forms設計器版本也包括Service Pack版本。 例如，對於Service Pack 15，版本號為6.5.15.20221112.1.0。在本示例中， 6.5.15是Service Pack版本。


1. 按兩下setup.exe啟動AEM Forms設計器安裝程式。
1. 繼續，在「個性化」螢幕上提供詳細資訊和序列號。
1. 如果接受許可協定，請按一下「下一步」繼續。
1. （可選）如果要在所選位置安裝設計器，請更改預設安裝路徑。 按一下下一步。
1. 按一下「上一步」(Back)更改任何首選項。 要安裝設計器，請按一下「安裝」。
1. 安裝完成後，按一下「完成」。

或者，可以使用被動或靜默模式通過命令行安裝AEM Forms設計器。

* 被動命令行安裝：安裝程式顯示一個進度欄，該進度欄指示安裝正在進行，但不顯示提示或錯誤消息。 啟動後，無法取消安裝。

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* 靜默命令行安裝：安裝程式運行安裝時不顯示用戶介面。 不顯示提示、消息或對話框。 啟動後，無法取消安裝。

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## 更新AEM Forms設計器 {#update-forms-designer}

更新AEM Forms設計器6.5.16.0的最新版本時有兩種情況：

* **案例1**:當用戶具有早於6.5.15.0的AEM Forms設計器版本時。
* **案例2**:當用戶具有6.5.15.0AEM Forms設計器版本時。

+++**當用戶具有早於6.5.15.0的AEM Forms設計器版本時。**

如果正在為AEM Forms設計器使用獨立安裝程式，請執行以下步驟：

1. 安裝前 **AEM Forms設計6.5.16.0**，用戶必須卸載任何以前的版本。
1. 下載並安裝 [AEM Forms設計6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 的子AEM菜單。
1. 成功安裝後 **AEM Forms設計6.5.15.0**，下載並安裝 [AEM Forms設計6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 按兩下下載的安裝程式檔案。

+++

+++**當用戶具有6.5.15.0AEM Forms設計器版本時**

如果正在為AEM Forms設計器使用獨立安裝程式，請執行以下步驟：
1. 從下載最新版本的AEM Forms設計器 [軟體分發門戶](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。
1. 按兩下下載的安裝程式檔案，安裝最新版本的AEM Forms設計器。

+++