---
title: 軟體體系結構
seo-title: 軟體體系結構
description: 設計軟體的最佳作法
seo-description: 設計軟體的最佳作法
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 423e17dadf2e506eb68b37851dde5e68ed950866
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 軟體體系結構{#software-architecture}

## 升級設計{#design-for-upgrades}

在擴展OOTB行為時，請務必牢記升級。 請一律在/apps目錄中套用自訂，並覆蓋/libs目錄中對應節點的頂端，或使用sling:resourceSuperType來擴充現成可用的行為。 雖然可能需要一些修改以支援新的AEM版本，但如果遵循此作法，新版本不應覆寫您的自訂。

### 盡可能重複使用模板和元件{#reuse-template-and-components-when-possible}

這可讓網站維持更一致的外觀和風格，並簡化程式碼維護。 當需要新範本時，請務必從共用基礎範本延伸，以便將clientlib包含等全域需求編碼在一個位置。 需要新元件時，請尋找從現有元件擴充的機會。

### 設計模板設計{#design-template-designs}

定義可包含在頁面上每個parsys中的元件後，即可控制網站外觀/風格的一致性。 借由限制頁面上對設計的存取，「超級作者」可以修改每頁允許的元件，而無需開發人員干預，同時確保其他作者遵守公司標準。

### 開發SOLID體系結構{#develop-a-solid-architecture}

SOLID是一個縮略語，描述了應該遵守的五個架構原則：

* ****&#x200B;單一責任原則 — 每個模組、類別、方法等應僅有一項責任。
* ****&#x200B;開啟/關閉原則 — 模組應開啟以供擴充，並關閉以供修改。
* **** Liskov替代原則 — 類型應由其子類型取代。
* ****&#x200B;介面隔離原則 — 不應強制任何客戶端依賴其不使用的方法。
* ****&#x200B;依賴性反演原則 — 高階模組不應依賴低階模組。兩者都應該取決於抽象性。 抽象化不應取決於細節。 詳情應取決於抽象化。

努力遵守這五項原則應導致一種嚴格分離關切的制度。

>[!TIP]
>
>SOLID是物件導向寫程式中常用的概念，在工業文獻中，每個元素都被廣泛討論。
>
>這只是提供的簡短摘要，建議您更深入了解這些概念。

### 遵循健壯性原則{#follow-the-robustness-principle}

健全性原則規定，我們應該在所發送的內容上保守，但在所接受的內容上保持自由。 換句話說，向第三方發送報文時，要完全符合規範，但是從第三方收到報文時，只要報文的含義明確，就要接受不符的報文。

### 在自己的模組中實作尖峰{#implement-spikes-in-their-own-modules}

尖峰和測試程式碼是任何Agile軟體實作的必備部分，但我們希望確保它們不會進入我們的生產程式碼庫，而沒有適當的監督層級。 因此，建議您在自己的模組中建立尖峰。

### 在自己的模組{#implement-data-migration-scripts-in-their-own-module}中實作資料移轉指令碼

資料移轉指令碼雖然是生產程式碼，但通常只會在網站初次啟動時執行一次。 因此，網站一上線，就會變成無用程式碼。 為確保我們不會建立依賴移轉指令碼的實施程式碼，應在自己的模組中實施。 這也可讓我們在啟動後立即移除和淘汰此程式碼，從系統中消除無效程式碼。

### 在POM檔案{#follow-published-maven-conventions-in-pom-files}中遵循已發佈的Maven慣例

Apache已在[https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html)發佈樣式慣例。 最好遵循這些慣例，因為這樣可讓新資源更容易快速上手。
