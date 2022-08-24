---
title: 軟體體系結構
seo-title: Software Architecture
description: 設計軟體的最佳實踐
seo-description: Best practices for architecting your software
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# 軟體體系結構{#software-architecture}

## 升級設計 {#design-for-upgrades}

在擴展OOTB行為時，必須牢記升級。 始終在/apps目錄中應用自定義項，並覆蓋/libs目錄中相應節點的上方，或使用sling:resourceSuperType擴展開箱行為。 雖然可能需要一些修改來支援新版AEM本，但如果遵循此慣例，則新版本不應覆蓋您的自定義設定。

### 盡可能重複使用模板和元件 {#reuse-template-and-components-when-possible}

這將使站點保持更一致的外觀和感覺，並簡化代碼維護。 當需要新模板時，請確保從共用基本模板擴展，以便可以將客戶端庫包含等全局要求編碼到一個位置。 當需要新元件時，請尋找從現有元件擴展的機會。

### 設計模板設計 {#design-template-designs}

通過定義哪些元件可以包括在頁面上的每個參數中，可以控制站點的外觀/感覺的一致性。 通過限制對頁面上設計的訪問，「超級作者」可以允許修改每頁允許的元件，而不需要開發人員干預，同時確保其他作者遵守公司標準。

### 開發SOLID體系結構 {#develop-a-solid-architecture}

SOLID是一個縮略語，它描述了應該遵循的五個體系結構原則：

* **S**&#x200B;單一責任原則 — 每個模組、類、方法等應僅負一個責任。
* **O** pen/Closed Principle — 模組應開啟以進行擴展，關閉以進行修改。
* **L** iskov替代原則 — 類型應由其子類型替換。
* **我**&#x200B;介面隔離原則 — 不應強制任何客戶依賴它不使用的方法。
* **D**&#x200B;依賴性反演原理 — 高級模組不應依賴於低級模組。 兩者都應取決於抽象。 抽象不應取決於細節。 細節應該取決於抽象。

努力遵守這五項原則，應形成一種嚴格分離的制度。

>[!TIP]
>
>SOLID是物件導向寫程式中常用的概念，各元素在工業文獻中得到廣泛討論。
>
>這只是一個簡短的摘要，供大家參考，我們鼓勵大家更深入地瞭解這些概念。

### 遵循魯棒性原則 {#follow-the-robustness-principle}

健壯性原則指出，我們應該保守派，但接受派，應該自由。 換句話說，在向第三方發送消息時，我們應該完全符合規範，但是在收到來自第三方的消息時，只要消息的含義明確，我們就應該接受不符合規範的消息。

### 在自己的模組中實施尖峰 {#implement-spikes-in-their-own-modules}

尖峰和test代碼是任何敏捷軟體實施過程中不可或缺的一部分，但我們希望確保它們在沒有適當級別監督的情況下不進入我們的生產代碼庫。 因此，建議在其自己的模組中建立尖峰。

### 在自己的模組中實施資料遷移指令碼 {#implement-data-migration-scripts-in-their-own-module}

雖然生產代碼，但資料遷移指令碼通常在站點初始啟動時只運行一次。 因此，一旦站點開始運行，就會變成死代碼。 為了確保我們不構建依賴遷移指令碼的實施代碼，應在其自己的模組中實施這些指令碼。 這還允許我們在啟動後立即刪除此代碼，從系統中消除死代碼。

### 在POM檔案中遵循已發佈的Maven約定 {#follow-published-maven-conventions-in-pom-files}

Apache已在以下位置發佈樣式約定： [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html)。 最好遵循這些慣例，因為這將使新資源更容易迅速地趕上。
