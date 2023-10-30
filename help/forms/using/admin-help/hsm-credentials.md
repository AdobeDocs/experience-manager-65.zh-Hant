---
title: 管理HSM認證
description: 瞭解如何管理HSM認證。 您可以從「信任存放區管理」頁面管理HSM。 您可以檢視、檢查、更新、重設和刪除HSM元件。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: facbeab2-de95-4778-894c-faa771d3391e
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 0%

---

# 管理HSM認證 {#managing-hsm-credentials}

您可以從「信任存放區管理」頁面管理「硬體安全性模組(HSM)」認證。 HSM是協力廠商PKCS#11裝置，可用來安全地產生和儲存私密金鑰。 HSM可實際保護對私密金鑰的存取與使用。

使用者端軟體必須與HSM通訊。 HSM使用者端軟體必須與AEM Forms安裝在同一部電腦上。

AEM Forms數位簽名可使用儲存在HSM上的憑證來套用伺服器端數位簽名。 請依照本節中的指示，為「數位簽名」將使用的每個HSM認證建立別名。 別名包含HSM所需的所有引數。

>[!NOTE]
>
>變更HSM組態後，請重新啟動AEM表單伺服器。

## 當HSM裝置上線時，建立HSM認證的別名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「HSM認證」，然後按一下「新增」。
1. 在「設定檔名稱」方塊中，輸入用於識別別名的字串。 此值會用作某些數位簽名作業（例如「簽名欄位」作業）的屬性。
1. 在「PKCS11程式庫」方塊中，輸入伺服器上HSM使用者端程式庫的完整路徑。 例如 `c:\Program Files\LunaSA\cryptoki.dll`。在叢集環境中，叢集內所有伺服器的這個路徑必須相同。
1. 按一下「測試HSM連線」。 如果AEM Forms能夠連線至HSM裝置，則會顯示一則訊息，說明HSM可供使用。 按一下「下一步」。
1. 使用「權杖名稱」、「插槽ID」或「插槽清單索引」來識別認證儲存在HSM上的位置。

   * **Token名稱：** 對應到要使用的HSM分割區名稱（例如HSMPART1）。
   * **位置識別碼：** 插槽ID是資料型別長型別的插槽識別碼。
   * **位置清單索引：** 如果您選取「槽清單索引」，請將「槽資訊」設定為與槽相對應的整數。 這是以0為基礎的索引，這表示如果先在HSMPART1資料分割中註冊使用者端，將會使用SlotListIndex值0參照HSMPART1。

1. 在Token Pin方塊中，輸入存取HSM金鑰所需的密碼，然後按一下「下一步」。
1. 在「認證」方塊中，選取認證。 按一下「儲存」。

## 當HSM裝置離線時，建立HSM認證的別名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「HSM認證」，然後按一下「新增」。
1. 在「設定檔名稱」方塊中，輸入用於識別別名的字串。 此值會用作某些數位簽名作業（例如「簽名欄位」作業）的屬性。
1. 在「PKCS11程式庫」方塊中，輸入伺服器上HSM使用者端程式庫的完整路徑。 例如 `c:\Program Files\LunaSA\cryptoki.dll`。在叢集環境中，叢集內所有伺服器的這個路徑必須相同。
1. 選取「建立離線設定檔」核取方塊。 按一下「下一步」。
1. 在HSM裝置清單中，選取儲存認證的HSM裝置製造商。
1. 在「槽型別」清單中，選取「槽標識」、「槽索引」或「Token名稱」，並在「槽資訊」方塊中指定一個值。 AEM Forms使用這些設定來決定認證儲存在HSM上的位置。

   * **Token名稱：** 對應至分割區名稱（例如HSMPART1）。
   * **位置識別碼：** 插槽ID是與插槽相對應的整數，而插槽又與分割區相對應。 例如，使用者端（表單伺服器）會先向HSMPART1資料分割註冊。 這會將插槽1對應至此使用者端的HSMPART1磁碟分割。 由於HSMPART1是第一個登入的磁碟分割，因此插槽ID為1，而您會將Slot Info設為1。

     插槽ID是依使用者端而設定。 如果您將第二部電腦註冊到不同的磁碟分割（例如，同一個HSM裝置上的HSMPART2），則插槽1會與該使用者端的HSMPART2磁碟分割相關聯。

   * **位置索引：** 如果您選取「槽索引」，請將「槽資訊」設定為與槽相對應的整數。 這是以0為基礎的索引，這表示如果先在HSMPART1資料分割中註冊使用者端，則插槽1會對應至此使用者端的HSMPART1。 因為HSMPART1是第一個登入的磁碟分割，所以插槽索引為0。

1. 選取其中一個選項，並提供路徑：

   * **憑證**：（使用SHA1時不需要使用）按一下「瀏覽」 ，然後找到您使用之認證的公開金鑰路徑。
   * **憑證SHA1：** （使用實體憑證時不需要）針對您使用的認證，輸入公開金鑰(.cer)檔案的SHA1值（指紋）。 請確定SHA1值中未使用空格。

1. 在「密碼」方塊中，輸入存取指定之插槽資訊的HSM金鑰所需的密碼，然後按一下「儲存」。

## 檢視HSM認證別名屬性 {#view-hsm-credential-alias-properties}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「HSM認證」。
1. 按一下認證別名的別名名稱以檢視特性，然後按一下確定。

## 檢查HSM認證的狀態 {#check-the-status-of-an-hsm-credential}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「HSM認證」。
1. 按一下您要檢查的認證旁的核取方塊，然後按一下檢查狀態。

「狀態」欄會反映認證的目前狀態。 如果失敗，「狀態」欄中會顯示紅色的X。 將滑鼠游標停留在X上以顯示包含失敗原因的工具提示。

## 更新HSM認證別名屬性 {#update-hsm-credential-alias-properties}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「HSM認證」。
1. 按一下認證別名的別名。
1. 按一下「更新認證」，並視需要更新設定。

## 重設所有HSM連線 {#reset-all-hsm-connections}

在Forms伺服器與HSM裝置之間的網路工作階段發生任何中斷後，重設與HSM裝置的開啟連線。 例如，網路中斷或HSM裝置因軟體更新而離線都會造成中斷。 中斷後，現有連線會過時，針對這些連線提出的任何簽署請求都會失敗。 使用「重設所有HSM連線」選項可清除舊連線。

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「HSM認證」。
1. 按一下「重設所有HSM連線」。

## 刪除HSM認證別名 {#delete-an-hsm-credential-alias}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「HSM認證」。
1. 選取您要刪除之HSM認證的核取方塊，按一下「刪除」，然後按一下「確定」。

## 設定遠端HSM支援 {#configure-remote-hsm-support}

AEM Forms使用Web服務式IPC/RPC機制。 此機制可讓AEM表單使用安裝在遠端電腦上的HSM。 若要使用此功能，請在安裝HSM的遠端電腦上安裝Web服務。 另請參閱 [在Windows 64位元平台上使用Sun JDK為AEM Forms ES設定HSM支援](https://kb2.adobe.com/cps/808/cpsid_80835.html)以取得詳細資訊。

此機制不支援線上建立HSM設定檔或狀態檢查。 但是，有兩種方法可建立HSM設定檔並執行狀態檢查：

* 透過傳遞簽署者的憑證來建立AEM Forms使用者端認證。 請依照中的步驟操作 [在Windows 64位元平台上使用Sun JDK為AEM Forms ES設定HSM支援](https://kb2.adobe.com/cps/808/cpsid_80835.html). Web服務位置會以Credential屬性的形式傳入。 也支援使用憑證或憑證SHA-1十六進位來建立離線HSM設定檔。 不過，如果您已從舊版AEM表單升級至AEM表單，請進行使用者端變更，因為認證包含憑證和Web服務資訊。
* 在Signature服務的管理主控台中指定Web服務位置。 (請參閱 [簽名服務設定](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) 在此處，使用者端僅攜帶信任存放區中HSM設定檔的別名。 即使您從舊版AEM表單升級至AEM表單，您仍可順暢地使用此選項，不需進行任何使用者端變更。 此選項不支援使用憑證SHA-1的HSM設定檔。
