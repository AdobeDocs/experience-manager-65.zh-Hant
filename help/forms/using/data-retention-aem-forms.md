---
title: AEM Forms中的資料保留
description: 瞭解Adobe Experience Manager (AEM) Forms在預設情況下如何充當傳遞伺服器，而不會儲存一般使用者資料，以支援資料隱私權。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin, User
solution: Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ca1448119778a2bcfeca7189aab5b360d992d99d
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 0%
---
# AEM Forms中的資料保留 {#data-retention-in-aem-forms}

AEM Forms是否會儲存表單資料？ 依預設，否。 Adobe Experience Manager (AEM) Forms是透過Adaptive Forms所擷取資料的傳遞伺服器，不會將一般使用者資料儲存在AEM存放庫中。 相反地，伺服器會將提交的資料傳遞至您擁有和設定的目的地。 此預設行為可協助您達成資料隱私權和合規性目標，適用於OSGi上的AEM Forms和JEE上的AEM Forms 。

由於AEM Forms是可擴充的平台，因此您可以自訂AEM來變更此預設行為。 如果您的自訂會將透過最適化表單提交的資料儲存在AEM存放庫或寫入AEM記錄檔，您必須確保生產和中繼系統上不會保留此類資料。

## 具有現成可用功能的預設行為 {#default-behavior}

使用現成最適化Forms功能時，AEM Forms不會儲存一般使用者資料。 伺服器會將提交的資料直接傳遞至您擁有和設定的目的地。

將表單連線到您擁有的目的地的現成機制包括表單資料模型(FDM)、現成聯結器和提交動作。 這些都會將資料傳送至您擁有和設定的位置，因此不會保留在AEM存放庫中。 表單也可以從規則或提交動作叫用外部或第三方服務（例如REST API），並將資料轉送至該服務，而不需在AEM上儲存資料。

如果您使用AEM工作流程與涉及核准步驟的長期流程，AEM Forms可能會將資料儲存在記憶體和暫時儲存中，以完成操作。 如需有關如何防止此資料儲存在AEM的資訊，請參閱[長期工作流程中的資料](#long-lived-workflow-processes)區段。

Forms Portal提交動作會保留透過Adaptive Forms擷取或提交的資料，但資料會儲存至您提供並擁有的儲存位置，不會儲存在AEM存放庫或記錄檔中。 如需詳細資訊，請參閱[表單入口網站提交動作儲存的安全資料](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-saved-by-forms-portal-submit-action)。

## 傳輸中的資料 {#data-in-transit}

雖然AEM Forms預設不會儲存一般使用者資料，但資料仍會在一般使用者、AEM Forms以及您設定的目的地之間移動。 使用傳輸層安全性(TLS)保護此流量，讓傳輸中的資料經過加密。

若要保護瀏覽器與AEM之間的連線，請在AEM執行個體上啟用HTTPS。 如需相關步驟，請參閱預設的[SSL/TLS](/help/sites-administering/ssl-by-default.md)。

此外，請確定AEM Forms傳送資料的目的地（例如雲端設定、提交動作URL和表單資料模型資料來源）使用安全的HTTPS端點。 由於AEM Forms不會儲存其傳遞的資料，靜態加密不適用於該資料。 如需保護連線的詳細指引，請參閱[安全傳輸層](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-transport-layer)。

## 外部資料存放區的表單資料模型 {#form-data-model}

若要讀取和寫入資料存放區的資料，請使用表單資料模型(FDM)。 FDM是將表單連線到您擁有及管理的資料來源（例如資料庫或RESTful Web服務）的建議機制。

如需詳細資訊，請參閱[ AEM Forms資料整合簡介](/help/forms/using/data-integration.md)。 如需保護FDM所處理資料的指引，請參閱[由表單資料模型(FDM)所處理的安全資料](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-handled-by-form-data-model-fdm)。

## 長期工作流程中的資料 {#long-lived-workflow-processes}

如果您使用長期工作流程，AEM可暫時將資料儲存為工作流程裝載的一部分。 承載此裝載的工作流程變數會儲存在AEM存放庫的工作流程例項中繼資料中，且可能包含一般使用者在填寫最適化表單時提供的個人識別資訊(PII)或敏感個人資料(SPD)。

若要將此資料儲存在您擁有並管理的存放庫（例如Azure Blob儲存）中，而不是放在AEM上，請使用AEM的資料外部化功能。 將變數外部化時，資料不會儲存在AEM存放庫中，而是儲存在您自己的資料存放庫中。

如需外部化資料的步驟，請參閱[將敏感資料引數化至工作流程變數並儲存在外部資料存放區](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)。

## 自訂和記錄 {#customization-and-logging}

AEM是可自訂的解決方案。 如果您自訂AEM，請確保您的自訂不會將任何資料儲存在AEM存放庫或記錄中。

使用預設功能時，AEM Forms不會將一般使用者資料寫入記錄中。

自訂程式碼可以將資料寫入記錄檔。 如果您在開發期間新增追蹤或記錄，請在將程式碼部署到中繼和生產環境之前，移除傳送至記錄的追蹤和資料。

## 關於AEM Forms資料保留的常見問題 {#faq}

**AEM Forms是否儲存表單資料？**

否。 依預設，Adobe Experience Manager (AEM) Forms是透過Adaptive Forms擷取的資料之傳遞伺服器，不會將一般使用者資料儲存在AEM存放庫中。 伺服器會將提交的資料傳遞至您擁有並設定的目的地，例如表單資料模型資料來源、提交動作目標或外部API。 此預設行為同時適用於OSGi上的AEM Forms和JEE上的AEM Forms 。

**最適化表單資料儲存於何處？**

提交的最適化表單資料會儲存在您擁有和設定的目的地，而非Adobe Experience Manager (AEM)存放庫。 現成可用的機制，例如表單資料模型(FDM)、聯結器和提交動作，可將資料傳送至您自己的位置。 表單也可以將資料轉送至外部服務（例如REST API），而無需將其儲存在AEM上。 Forms Portal提交動作也會將資料儲存至您提供並擁有的儲存位置。

**長期工作流程是否儲存表單資料？**

Adobe Experience Manager (AEM) Forms中的長期工作流程可以暫時將資料儲存為工作流程裝載的一部分，該裝載儲存在AEM存放庫的工作流程例項中繼資料中。 若要將此資料保留在您擁有並管理的存放庫（例如Azure Blob儲存體）中，而不是在AEM上，請針對工作流程變數](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)使用[AEM資料外部化功能。

**AEM Forms會將資料寫入記錄檔嗎？**

否。 使用預設功能時，Adobe Experience Manager (AEM) Forms不會將一般使用者資料寫入記錄中。 由於AEM是可自訂的平台，因此自訂程式碼可以將資料寫入記錄檔。 如果您在開發期間新增追蹤或記錄，請在部署到中繼和生產環境之前，移除這些追蹤和任何記錄資料。 自訂不得將資料儲存在AEM存放庫或記錄中。

**如何保護傳輸中的資料？**

Adobe Experience Manager (AEM) Forms中的傳輸層安全性(TLS)可保護傳輸中的資料。 在AEM執行個體上啟用HTTPS，以保護瀏覽器與AEM之間的連線。 此外，請確定AEM Forms傳送資料的目的地（例如雲端設定、提交動作URL和表單資料模型資料來源）使用安全的HTTPS端點。 由於AEM Forms不會儲存其傳遞的資料，靜態加密不適用於該資料。

## 相關資源 {#related-resources}

* [AEM Forms資料整合簡介](/help/forms/using/data-integration.md)
* [將工作流程變數的敏感資料引數化，並儲存在外部資料存放區中](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)
* [設定提交動作](/help/forms/using/configuring-submit-actions.md)
* [在OSGi環境中強化及保護AEM Forms](/help/forms/using/hardening-securing-aem-forms-environment.md)
