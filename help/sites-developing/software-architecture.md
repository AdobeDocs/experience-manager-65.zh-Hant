---
title: 軟體架構
seo-title: 軟體架構
description: 建立軟體架構的最佳實務
seo-description: 建立軟體架構的最佳實務
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
translation-type: tm+mt
source-git-commit: 423e17dadf2e506eb68b37851dde5e68ed950866
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 軟體體系結構{#software-architecture}

## 升級設計{#design-for-upgrades}

在擴展OOTB行為時，請務必牢記升級。 請一律在/apps目錄中套用自訂項目，或在/libs目錄中對應節點上方覆蓋，或使用sling:resourceSuperType來擴充開箱即用行為。 雖然可能需要進行某些修改才能支援新AEM版本，但如果遵循此慣例，新版本不應覆寫您的自訂設定。

### 盡可能{#reuse-template-and-components-when-possible}重複使用範本和元件

這可讓網站維持更一致的外觀和感覺，並簡化程式碼維護。 當需要新範本時，請務必從共用的基本範本延伸，如此全域需求（例如clientlib內含項目）就可以在單一位置編碼。 當需要新元件時，請尋找從現有元件擴充的機會。

### 設計範本設計{#design-template-designs}

定義頁面上每個參數中可包含哪些元件，即可控制網站外觀／感覺的一致性。 借由限制頁面上對設計的存取權，「超級作者」可以修改每頁允許的元件，而不需開發人員介入，同時確保其他作者遵守公司標準。

### 開發SOLID體系結構{#develop-a-solid-architecture}

SOLID是一個縮略語，它描述了應該遵循的五個體系結構原則：

* **單**&#x200B;一責任原則——每個模組、類別、方法等應僅負一個責任。
* **開**&#x200B;放／關閉原則——模組應開啟以進行擴展，關閉以進行修改。
* **利斯**&#x200B;科夫替代原則——類型應由其子類型替換。
* **界**&#x200B;面隔離原則——任何客戶端都不應強制依賴於它不使用的方法。
* **相**&#x200B;依性反演原則——高階模組不應依賴低階模組。兩者都應依賴抽象概念。 抽象不應該取決於細節。 細節應該取決於抽象。

堅持這五條原則，應當形成嚴格的分離制度。

>[!TIP]
>
>SOLID是物件導向寫程式中常用的概念，各個元素在工業文獻中得到廣泛的討論。
>
>這只是提供的簡短摘要，讓您更深入地瞭解這些概念。

### 遵循健壯性原則{#follow-the-robustness-principle}

健壯性原則指出，我們應該保守所傳的內容，但在所接受的內容上要自由。 也就是說，向第三方發送資訊時，要完全符合規範，但接收到第三方的資訊時，只要消息含義明確，就應該接受不符的資訊。

### 在自己的模組中實施尖峰{#implement-spikes-in-their-own-modules}

尖峰和測試程式碼是任何Agile軟體實作的一部份，但我們希望確保它們不會進入我們的生產程式碼庫，而不受適當的監督。 因此，建議在自己的模組中建立尖峰。

### 在自己的模組{#implement-data-migration-scripts-in-their-own-module}中實施資料遷移指令碼

雖然生產程式碼，但資料移轉指令碼通常在網站初次啟動時只執行一次。 因此，當網站上線時，就會變成無用程式碼。 為了確保我們不建立依賴移轉指令碼的實施程式碼，這些程式碼應該建置在自己的模組中。 這也允許我們在啟動後立即移除和淘汰此程式碼，從系統中消除死代碼。

### 遵循POM檔案{#follow-published-maven-conventions-in-pom-files}中發佈的Maven約定

Apache已發佈樣式慣例，位於[https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html)。 最好依循這些慣例，因為新資源更容易快速上手。
