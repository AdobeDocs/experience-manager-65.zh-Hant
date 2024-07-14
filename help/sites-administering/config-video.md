---
title: 設定視訊元件
description: 瞭解如何使用Adobe Experience Manager中的視訊元件，將預先定義的現成視訊資產放置在頁面上。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# 設定視訊元件 {#configure-the-video-component}

[視訊元件](/help/sites-authoring/default-components-foundation.md#video)可讓您在頁面上放置預先定義的現成視訊資產。

為了進行適當的轉碼，管理員會單獨安裝FFmpeg。 請參閱[安裝FFmpeg並設定AEM](#install-ffmpeg)。 管理員也[設定視訊設定檔](#configure-video-profiles)以搭配HTML5元素使用。

>[!CAUTION]
>
>已棄用此基礎元件。 Adobe建議改用[核心元件內嵌元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html)。

>[!CAUTION]
>
>若無廣泛的專案層級自訂，此元件就不能再正常運作。

## 設定視訊設定檔 {#configure-video-profiles}

若要使用HTML5元素，請定義視訊設定檔。 此處選取的專案會依序使用。 若要存取，請使用[設計模式](/help/sites-authoring/default-components-designmode.md) （僅限傳統UI）並選取&#x200B;**[!UICONTROL 設定檔]**&#x200B;索引標籤：

![chlimage_1-317](assets/chlimage_1-317.png)

在此對話方塊中，您也可以為[!UICONTROL 播放]、[!UICONTROL Flash]和[!UICONTROL 進階]設定視訊元件和引數的設計。

## 安裝FFmpeg並設定AEM {#install-ffmpeg}

視訊元件仰賴協力廠商開放原始碼產品FFmpeg轉碼視訊。 已從[https://ffmpeg.org/](https://ffmpeg.org/)下載。 安裝FFmpeg後，請設定AEM使用特定的音訊轉碼器和特定的執行階段選項。

若要在&#x200B;**Windows**&#x200B;上安裝FFmpeg，請執行下列步驟：

1. 將編譯的二進位檔下載為`ffmpeg.zip`。
1. 取消封存至資料夾。
1. 將系統環境變數`PATH`設定為&lt;*your-ffmpeg-location*>`\bin`。
1. 重新啟動AEM。

若要在&#x200B;**macOS X**&#x200B;上安裝FFmpeg，請遵循下列步驟：

1. 安裝位於[developer.apple.com/xcode](https://developer.apple.com/xcode/)的Xcode。
1. 安裝位於[XQuartz](https://www.xquartz.org)以取得[X11](https://support.apple.com/en-us/100724)。
1. 安裝位於[www.macports.org](https://www.macports.org/)的MacPorts。
1. 在主控台中，執行`sudo port install ffmpeg`命令並遵循熒幕上的指示。 請確定`FFmpeg`可執行檔的路徑已新增至`PATH`系統變數。

若要使用預先編譯的版本，在&#x200B;**macOS X 10.6**&#x200B;上安裝FFmpeg，請執行下列步驟：

1. 下載先行編譯版本。
1. 將其取消封存到`/usr/local`目錄。
1. 在主控台中，執行`sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`。 視需要變更路徑。

若要&#x200B;**設定AEM**，請遵循下列步驟：

>[!NOTE]
>
>只有在需要進一步自訂轉碼器時，才需要執行這些步驟。

1. 在網頁瀏覽器中開啟[!UICONTROL CRXDE Lite]。 存取[http://localhost:4502/crx/de](http://localhost:4502/crx/de)。
2. 選取`/libs/settings/dam/video/format_aac/jcr:content`節點，並確定節點屬性如下：

   * `audioCodec`是`aac`。
   * `customArgs`是`-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`。

3. 若要自訂設定，請在`/apps/settings/`節點中建立覆蓋，並將相同的結構移動到`/conf/global/settings/`節點下。 無法在`/libs`節點中編輯它。 例如，若要覆蓋路徑`/libs/settings/dam/video/fullhd-bp`，請在`/conf/global/settings/dam/video/fullhd-bp`建立它。

   >[!NOTE]
   >
   >覆蓋並編輯整個設定檔節點，而不僅僅是需要修改的屬性。 這類資源無法透過SlingResourceMerger解析。

4. 如果您變更其中一個屬性，請按一下[全部儲存]。****

>[!NOTE]
>
>升級AEM執行個體時，不會保留預設現成工作流程模型的變更。 Adobe建議您先複製修改過的工作流程模型，然後再進行編輯。 例如，先複製現成的[!UICONTROL DAM Update Asset]模型，然後再編輯[!UICONTROL DAM Update Asset]模型中的FFmpeg轉碼步驟，以挑選升級前存在的視訊設定檔名稱。 接著，您可以覆蓋`/apps`節點，讓AEM擷取現成可用模型的自訂變更。
