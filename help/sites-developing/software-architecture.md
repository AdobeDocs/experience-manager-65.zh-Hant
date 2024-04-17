---
title: 軟體架構
description: 瞭解為Adobe Experience Manager設計軟體架構的一些最佳實務。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# 軟體架構{#software-architecture}

## 針對升級而設計 {#design-for-upgrades}

擴充現成行為時，請務必牢記升級事項。 請一律在/apps目錄中套用自訂，並覆蓋在/libs目錄中對應的節點上方，或使用sling：resourceSuperType來擴充現成行為。 雖然可能需要進行一些修改才能支援新的AEM版本，但若遵循此作法，新版本不應覆寫您的自訂。

### 儘可能重複使用範本和元件 {#reuse-template-and-components-when-possible}

這麼做可讓網站維持一致的外觀和風格，並簡化程式碼維護作業。 當需要新範本時，請務必從共用基礎範本擴充，以便可以在一個位置對clientlib包含等全域需求進行編碼。 當需要新元件時，請尋找從現有元件擴充的機會。

### 設計範本設計 {#design-template-designs}

透過定義頁面上每個parsys可包含的元件，可以控制網站外觀/感覺的一致性。 透過限制對頁面上設計的存取，可允許「超級作者」修改每頁允許的元件，而不需要開發人員干預，同時確保其他作者遵循企業標準。

### 開發SOLID架構 {#develop-a-solid-architecture}

SOLID是縮寫，說明應遵守的五個架構原則：

* **S**&#x200B;單一職責原則 — 每個模組、類別、方法等只能有一個職責。
* **O**&#x200B;開啟/關閉原則 — 模組應該開啟以供延伸，並關閉以供修改。
* **L** iskov Substitution Principal — 型別應該由其子型別取代。
* **I**&#x200B;介面分隔原則 — 不應強制任何使用者端依賴其未使用的方法。
* **D**&#x200B;相依性反轉原則 — 高階模組不應依賴低階模組。 兩者都應該依賴抽象。 抽象不應該依賴細節。 詳細資訊應取決於抽象概念。

努力遵守這五項原則應該會導致系統有嚴格的分開考量。

>[!TIP]
>
>SOLID是物件導向程式設計中常用的概念，在產業文獻中會廣泛討論每個元素。
>
>此資訊只是為了提升意識而呈現的簡短摘要，建議您更深入地熟悉這些概念。

### 遵循健全性原則 {#follow-the-robustness-principle}

穩健性原則指出您在傳送內容上應持保守態度，但在接受內容上應持開放態度。 換言之，在將訊息傳送給第三方時，您應該完全符合規格。 但是，當您收到來自協力廠商的訊息時，只要訊息的含義明確，您就應該接受不符合的訊息。

### 在自己的模組中實作尖峰 {#implement-spikes-in-their-own-modules}

尖峰和測試程式碼是任何Agile軟體實施的一部分。 但是，您想要確保在沒有適當監督層級的情況下，他們不會進入生產計畫碼基底。 因此，建議在其本身的模組中建立尖峰。

### 在其本身的模組中實作資料移轉指令碼 {#implement-data-migration-scripts-in-their-own-module}

資料移轉指令碼雖然是生產程式碼，但在網站初次啟動時只會執行一次。 因此，當網站上線時，指令碼會變成廢棄的程式碼。 為確保您不會建立相依於移轉指令碼的實作程式碼，這些程式碼應在自己的模組中實作。 如此一來，我們就可以在啟動後立即移除並淘汰此程式碼，從系統中清除廢棄的程式碼。

### 遵循POM檔案中已發佈的Maven慣例 {#follow-published-maven-conventions-in-pom-files}

Apache已發佈樣式慣例，位於 [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). 最好遵循這些慣例，因為這樣可讓新資源更易於快速上線。
