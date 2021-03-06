---
title: Verwalten des Android-Emulators über den Xamarin Android Device Manager
description: In diesem Handbuch wird erläutert, wie Sie den Xamarin Android-Geräte-Manager verwenden, um virtuelle Android-Geräte (AVDs) zu erstellen und zu konfigurieren, die Android-Geräte emulieren. Sie können diese virtuellen Geräte verwenden, um Ihre App auszuführen und zu testen, ohne von einem physischen Gerät abhängig zu sein.
ms.prod: xamarin
ms.assetid: ECB327F3-FF1C-45CC-9FA6-9C11032BD5EF
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 05/03/2018
ms.openlocfilehash: 420ffc905659c6fd6245dc8cc3bdae4cb9401a63
ms.sourcegitcommit: e16517edcf471b53b4e347cd3fd82e485923d482
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2018
---
# <a name="xamarin-android-device-manager"></a>Xamarin Android-Geräte-Manager

_In diesem Handbuch wird erläutert, wie Sie Xamarin Android Device Manager verwenden, um virtuelle Android-Geräte (AVDs) zu erstellen und zu konfigurieren, die Android-Geräte emulieren. Sie können diese virtuellen Geräte verwenden, um Ihre App auszuführen und zu testen, ohne von einem physischen Gerät abhängig zu sein._

## <a name="overview"></a>Übersicht

Nachdem Sie überprüft haben, dass die Hardwarebeschleunigung aktiviert ist (wie unter [Hardware Acceleration](~/android/get-started/installation/android-emulator/hardware-acceleration.md) (Hardwarebeschleunigung für Android-Emulator) beschrieben), ist der nächste Schritt das Erstellen virtueller Geräte für das Testen und Debuggen Ihrer App mithilfe von Xamarin Android Device Manager.


# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

In diesem Handbuch wird erklärt, wie Sie Xamarin Android Device Manager für Visual Studio unter Windows (oder [Mac](?tabs=vsmac)) verwenden:

[![Screenshot des Xamarin Android-Geräte-Managers auf der Registerkarte „Geräte“](xamarin-device-manager-images/win/01-devices-dialog-sml.png)](xamarin-device-manager-images/win/01-devices-dialog.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

In diesem Handbuch wird erklärt, wie Sie Xamarin Android Device Manager für Visual Studio für Mac (oder [Windows](?tabs=vswin)) verwenden:

[![Screenshot des Xamarin Android-Geräte-Managers auf der Registerkarte „Geräte“](xamarin-device-manager-images/mac/01-devices-dialog-sml.png)](xamarin-device-manager-images/mac/01-devices-dialog.png#lightbox)

> [!NOTE]
> Dieser Leitfaden gilt nur für Visual Studio für Mac.
Xamarin Studio ist nicht mit dem Xamarin Android-Geräte-Manager kompatibel.

-----

Der Xamarin Android-Geräte-Manager wird verwendet, um *virtuelle Android-Geräte* (AVDs) zu erstellen und zu konfigurieren, die im [Android SDK-Emulator](~/android/deploy-test/debugging/android-sdk-emulator/index.md) ausgeführt werden.
Jedes virtuelle Android-Gerät stellt eine Emulatorkonfiguration dar, die ein physisches Android-Gerät simuliert. Dadurch wird das Ausführen und Testen Ihrer App mit einer Vielzahl von Konfigurationen ermöglicht, die verschiedene physische Android-Geräte simulieren. Der Xamarin Android-Geräte-Manager ersetzt den eigenständigen AVD-Manager von Google (der als veraltet gilt).

In diesem Handbuch wird erklärt, wie virtuelle Geräte mit dem Xamarin Android-Geräte-Manager erstellt, dupliziert, angepasst und gestartet werden. Dieses Handbuch erläutert außerdem die Konfiguration von Eigenschaften für jedes virtuelle Gerät (z.B. API-Ebene, CPU, Arbeitsspeicher und Auflösung), das Aktivieren und Deaktivieren von simulierten Sensoren wie dem Beschleunigungsmesser, GPS und dem Ausrichtungs- und Lichtsensor sowie die Konfiguration der Art der Hardwarebeschleunigung, die vom virtuellen Gerät verwendet wird.

## <a name="requirements"></a>Anforderungen

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Sie benötigen Folgendes, um den Xamarin Android-Geräte-Manager verwenden zu können:

- Visual Studio 2017, Version 15.7 oder höher. Visual Studio Community Edition und höher wird unterstützt.

- Xamarin für Visual Studio Version 4.9 oder höher. Weitere Informationen zum Updaten von Xamarin finden Sie unter [Change the Updates Channel (Ändern des Updatekanals)](https://developer.xamarin.com/recipes/cross-platform/ide/change_updates_channel/).

- **Android SDK** &ndash; Android SDK muss installiert sein (siehe [Android SDK Setup (Setup von Android SDK)](~/android/get-started/installation/android-sdk.md)), und Version 26.0 oder höher von Android SDK Tools muss (gemäß den Erläuterungen im folgenden Abschnitt) installiert sein. Achten Sie darauf, Android SDK an folgendem Speicherort zu installieren (wenn das SDK nicht bereits installiert ist): **C:\\Programme (x86)\\Android\\android-sdk**.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

- Visual Studio für Mac 7.5 oder höher.

- **Android SDK** &ndash; Android SDK 8.0 (API 26) oder höher muss über den SDK-Manager installiert werden.

-----

## <a name="launching-the-device-manager"></a>Starten des Geräte-Managers

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Starten Sie Xamarin Android Device Manager über das Menü **Extras** durch Klicken auf **Tools > Android-Emulator-Manager**:

[![Start über das Menü „Extras“](xamarin-device-manager-images/win/04-tools-menu-sml.png)](xamarin-device-manager-images/win/04-tools-menu.png#lightbox)

Wenn beim Starten folgendes Fehlerdialogfeld angezeigt wird, finden Sie im Abschnitt [Problembehandlung](#troubleshooting) Anweisungen zur Umgehung dieses Problems:

![Android SDK: Instanzfehler](xamarin-device-manager-images/win/32-sdk-error.png)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Starten Sie Xamarin Android Device Manager in Visual Studio für Mac, indem Sie auf **Extras > Emulator-Manager** klicken:

[![Start über das Menü „Extras“](xamarin-device-manager-images/mac/16-tools-menu-sml.png)](xamarin-device-manager-images/mac/16-tools-menu.png#lightbox)

-----

Bevor Sie den Android-Geräte-Manager verwenden können, müssen Sie Version 26.0.0 oder höher von Android SDK Tools installieren. Wenn Android SDK Tools 26.0.0 oder höher nicht installiert ist, wird beim Starten folgendes Fehlerdialogfeld angezeigt:

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

![Android SDK: Instanzfehler (Dialogfeld)](xamarin-device-manager-images/win/02-sdk-instance-error.png)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

![Android SDK: Instanzfehler (Dialogfeld)](xamarin-device-manager-images/mac/02-sdk-instance-error.png)

-----

Wenn Ihnen dieses Fehlerdialogfeld angezeigt wird, klicken Sie auf **OK**, um den Android SDK-Manager zu öffnen. Klicken Sie im Android SDK-Manager auf die Registerkarte **Tools**, und installieren Sie **Android SDK Tools 26.0.2** oder höher, **Android SDK Platform-Tools 26.0.0** oder höher und **Android SDK Build-Tools 26.0.0** oder höher:

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

[![Installieren von Android SDK Tools 26.0](xamarin-device-manager-images/win/03-sdk-tools-sml.png)](xamarin-device-manager-images/win/03-sdk-tools.png#lightbox)

Nachdem diese Pakete installiert wurden, können Sie den SDK-Manager schließen und den Android-Geräte-Manager erneut starten.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

[![Installieren von Android SDK Tools 26.0](xamarin-device-manager-images/mac/03-sdk-tools-sml.png)](xamarin-device-manager-images/mac/03-sdk-tools.png#lightbox)

-----

## <a name="main-screen"></a>Hauptbildschirm

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Wenn Sie den Android-Geräte-Manager zum ersten Mal starten, wird ein Bildschirm mit allen derzeit konfigurierten virtuellen Geräten angezeigt. Für jedes Gerät werden der **Name**, das **Betriebssystem** (Ebene der Android-API), die **CPU**, die Größe des **Arbeitsspeichers** und die Bildschirmauflösung angezeigt:

[![Liste der installierten Geräte und deren Parameter](xamarin-device-manager-images/win/05-installed-list-sml.png)](xamarin-device-manager-images/win/05-installed-list.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Wenn Sie den Android-Geräte-Manager zum ersten Mal starten, wird ein Bildschirm mit allen derzeit konfigurierten virtuellen Geräten angezeigt. Für jedes Gerät werden der **Name**, das **Systemimage** (Ebene der Android-API), die **CPU**, die Größe des **Arbeitsspeichers** und die Bildschirmauflösung angezeigt:

[![Liste der installierten Geräte und deren Parameter](xamarin-device-manager-images/mac/05-devices-list-sml.png)](xamarin-device-manager-images/mac/05-devices-list.png#lightbox)

-----

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Wenn Sie ein Gerät in der Liste anklicken, wird die Schaltfläche **Starten** auf der rechten Seite angezeigt. Sie können auf die Schaltfläche **Starten** klicken, um den Emulator mit diesem virtuellen Gerät zu starten:

[![Schaltfläche „Starten“ für ein Geräteimage](xamarin-device-manager-images/win/06-start-button-sml.png)](xamarin-device-manager-images/win/06-start-button.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Klicken Sie auf die Schaltfläche **Wiedergeben**, um den Emulator mit dem gewünschten virtuellen Gerät zu starten:

[![Schaltfläche „Starten“ für ein Geräteimage](xamarin-device-manager-images/mac/06-start-button-sml.png)](xamarin-device-manager-images/mac/06-start-button.png#lightbox)

-----

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Nachdem der Emulator mit dem ausgewählten virtuellen Gerät startet, ändert sich die Schaltfläche **Starten** in die Schaltfläche **Beenden**. Diese können Sie verwenden, um den Emulator anzuhalten:

[![Schaltfläche „Beenden“ für das ausgeführte Gerät](xamarin-device-manager-images/win/07-stop-button-sml.png)](xamarin-device-manager-images/win/07-stop-button.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Nachdem der Emulator mit dem ausgewählten virtuellen Gerät startet, ändert sich die Schaltfläche **Wiedergeben** in die Schaltfläche **Beenden**. Diese können Sie verwenden, um den Emulator anzuhalten:

[![Schaltfläche „Beenden“ für das ausgeführte Gerät](xamarin-device-manager-images/mac/07-stop-button-sml.png)](xamarin-device-manager-images/mac/07-stop-button.png#lightbox)

-----

### <a name="new-device"></a>Neues Gerät

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Klicken Sie auf die Schaltfläche **Neu** im oberen rechten Bereich des Bildschirms, um ein neues Gerät zu erstellen:

[![Schaltfläche „Neu“ zum Erstellen eines neuen Geräts](xamarin-device-manager-images/win/08-new-button-sml.png)](xamarin-device-manager-images/win/08-new-button.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Klicken Sie auf die Schaltfläche **Neues Gerät** im oberen rechten Bereich des Bildschirms, um ein neues Gerät zu erstellen:

[![Schaltfläche „Neu“ zum Erstellen eines neuen Geräts](xamarin-device-manager-images/mac/08-new-button-sml.png)](xamarin-device-manager-images/mac/08-new-button.png#lightbox)

-----

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Durch das Klicken auf **Neu** wird der Bildschirm **Neues Gerät** angezeigt:

[![Bildschirm „Neues Gerät“ des Geräte-Managers](xamarin-device-manager-images/win/09-new-device-editor-sml.png)](xamarin-device-manager-images/win/09-new-device-editor.png#lightbox)

Befolgen Sie diese Schritte, um ein neues Gerät im Bildschirm **Neues Gerät** zu konfigurieren:

1. Wählen Sie das zu emulierende physische Gerät aus, indem Sie auf das Pulldownmenü **Gerät** klicken:

    [![Pulldownmenü des Geräts](xamarin-device-manager-images/win/10-device-menu-sml.png)](xamarin-device-manager-images/win/10-device-menu.png#lightbox)

2. Wählen Sie ein Systemimage aus, das mit diesem virtuellen Gerät verwendet werden soll, indem Sie auf das Pulldownmenü **System image** (Systemimage) klicken. In diesem Menü werden die installierten Systemimages unter **Installiert** aufgeführt. Im Abschnitt **Herunterladen** werden Systemimages aufgeführt, die derzeit nicht auf Ihrem Entwicklungscomputer verfügbar sind, aber automatisch installiert werden können:

    [![Pulldownmenü „Systemimage“](xamarin-device-manager-images/win/11-system-image-menu-sml.png)](xamarin-device-manager-images/win/11-system-image-menu.png#lightbox)

3. Weisen Sie dem Gerät einen neuen Namen zu. Im folgenden Beispiel lautet der Name des Geräts **Nexus 5 API 25**:

    [![Benennen des neuen Geräts](xamarin-device-manager-images/win/12-device-name-sml.png)](xamarin-device-manager-images/win/12-device-name.png#lightbox)

4. Bearbeiten Sie alle Eigenschaften, die Sie ändern müssen. Weitere Informationen zum Ändern von Eigenschaften finden Sie weiter unten in diesem Handbuch unter [Profileigenschaften](#properties).

5. Fügen Sie sämtliche zusätzliche Eigenschaften hinzu, die Sie explizit festlegen müssen. Auf dem Bildschirm **Neues Gerät** werden nur häufig geänderte Eigenschaften angezeigt. Sie können jedoch auf das Pulldownmenü **Eigenschaft hinzufügen** im unteren linken Bereich klicken, um zusätzliche Eigenschaften hinzuzufügen. Im folgenden Beispiel wird die `hw.lcd.backlight`-Eigenschaft hinzugefügt:

    [![Pulldownmenü „Eigenschaft hinzufügen“](xamarin-device-manager-images/win/13-add-property-menu-sml.png)](xamarin-device-manager-images/win/13-add-property-menu.png#lightbox)

6. Klicken Sie auf die Schaltfläche **Erstellen** im unteren rechten Bereich, um ein neues Gerät zu erstellen:

    ![Schaltfläche „Erstellen“](xamarin-device-manager-images/win/14-create-button.png)

7. Möglicherweise wird Ihnen der Bildschirm **Zustimmung zur Lizenz** angezeigt. Klicken Sie auf **Zustimmen**, wenn Sie den Lizenzbedingungen zustimmen:

    ![Bildschirm „Zustimmung zur Lizenz“](xamarin-device-manager-images/win/15-license-acceptance.png)

8. Der Android-Geräte-Manager fügt das neue Gerät zur Liste der installierten virtuellen Geräte hinzu. Dabei zeigt die Statusanzeige **Creating** (Wird erstellt) an, während das Gerät erstellt wird:

    [![Statusanzeige „Erstellung“](xamarin-device-manager-images/win/16-creating-the-device-sml.png)](xamarin-device-manager-images/win/16-creating-the-device.png#lightbox)

9. Wenn der Erstellungsvorgang abgeschlossen ist, ist das neue Gerät startbereit und wird in der Liste der installierten virtuellen Geräte mit der Schaltfläche **Starten** angezeigt:

   [![Das startbereite neu erstellte Gerät](xamarin-device-manager-images/win/17-created-device-sml.png)](xamarin-device-manager-images/win/17-created-device.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Durch das Klicken auf **Neues Gerät** wird der Bildschirm **Neues Gerät** angezeigt:

[![Bildschirm „Neues Gerät“ des Geräte-Managers](xamarin-device-manager-images/mac/09-new-device-editor-sml.png)](xamarin-device-manager-images/mac/09-new-device-editor.png#lightbox)

Befolgen Sie diese Schritte, um ein neues Gerät im Bildschirm **Neues Gerät** zu konfigurieren:

1. Wählen Sie das zu emulierende physische Gerät aus, indem Sie auf das Pulldownmenü **Gerät** klicken:

    [![Pulldownmenü des Geräts](xamarin-device-manager-images/mac/10-device-menu-sml.png)](xamarin-device-manager-images/mac/10-device-menu.png#lightbox)

2. Wählen Sie ein Systemimage aus, das mit diesem virtuellen Gerät verwendet werden soll, indem Sie auf das Pulldownmenü **System image** (Systemimage) klicken. In diesem Menü werden die installierten Systemimages unter **Installiert** aufgeführt. Im Abschnitt **Herunterladen** (wenn dieser angezeigt wird) werden Systemimages aufgeführt, die derzeit nicht auf Ihrem Entwicklungscomputer verfügbar sind, aber automatisch installiert werden können:

    [![Pulldownmenü „Systemimage“](xamarin-device-manager-images/mac/11-system-image-menu-sml.png)](xamarin-device-manager-images/mac/11-system-image-menu.png#lightbox)

3. Weisen Sie dem Gerät einen neuen Namen zu. Im folgenden Beispiel lautet der Name des Geräts **Nexus 5X API 25**:

    [![Benennen des neuen Geräts](xamarin-device-manager-images/mac/12-device-name-sml.png)](xamarin-device-manager-images/mac/12-device-name.png#lightbox)

4. Bearbeiten Sie alle Eigenschaften, die Sie ändern müssen. Weitere Informationen zum Ändern von Eigenschaften finden Sie weiter unten in diesem Handbuch unter [Profileigenschaften](#properties).

5. Fügen Sie sämtliche zusätzliche Eigenschaften hinzu, die Sie explizit festlegen müssen. Auf dem Bildschirm **Neues Gerät** werden nur häufig geänderte Eigenschaften angezeigt. Sie können jedoch auf das Pulldownmenü **Eigenschaft hinzufügen** im unteren linken Bereich klicken, um zusätzliche Eigenschaften hinzuzufügen:

    [![Pulldownmenü „Eigenschaft hinzufügen“](xamarin-device-manager-images/mac/13-add-property-menu-sml.png)](xamarin-device-manager-images/mac/13-add-property-menu.png#lightbox)

6. Sie können ebenfalls auf **Benutzerdefiniert** klicken, um eine neue Eigenschaft für das Gerät zu definieren:

    ![Schaltfläche „Erstellen“](xamarin-device-manager-images/mac/14-custom-button.png)

7. Klicken Sie auf die Schaltfläche **Erstellen** im unteren rechten Bereich, um ein neues Gerät zu erstellen:

    ![Schaltfläche „Erstellen“](xamarin-device-manager-images/mac/15-create-button.png)

8. Möglicherweise wird Ihnen der Bildschirm **Zustimmung zur Lizenz** angezeigt. Klicken Sie auf **Zustimmen**, wenn Sie den Lizenzbedingungen zustimmen.

9. Während das Gerät erstellt wird, fügt der Android-Geräte-Manager das neue Gerät mit der Statusanzeige **Creating** (Wird erstellt) zur Geräteliste hinzu:

    [![Statusanzeige „Erstellung“](xamarin-device-manager-images/mac/17-creating-the-device-sml.png)](xamarin-device-manager-images/mac/17-creating-the-device.png#lightbox)

10. Wenn der Erstellungsvorgang abgeschlossen ist, ist das neue Gerät startbereit und wird in der Geräteliste mit der Schaltfläche **Wiedergeben** angezeigt:

   [![Das startbereite neu erstellte Gerät](xamarin-device-manager-images/mac/18-created-device-sml.png)](xamarin-device-manager-images/mac/18-created-device.png#lightbox)

-----


<a name="device-edit" />


### <a name="edit-device"></a>Bearbeiten von Geräten

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Wählen Sie zum Bearbeiten eines vorhandenen virtuellen Geräts ein Gerät aus, und klicken Sie auf die Schaltfläche **Bearbeiten**, die sich im oberen rechten Bereich des Bildschirms befindet:

[![Schaltfläche „Bearbeiten“ zum Bearbeiten eines neuen Geräts](xamarin-device-manager-images/win/19-edit-button-sml.png)](xamarin-device-manager-images/win/19-edit-button.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Klicken Sie auf das Pulldownmenü **Zusätzliche Optionen** (Zahnradsymbol) und dann auf **Bearbeiten**, um ein vorhandenes virtuelles Gerät zu bearbeiten:
 
[![Menüauswahl „Bearbeiten“ zum Bearbeiten eines neuen Geräts](xamarin-device-manager-images/mac/19-edit-button-sml.png)](xamarin-device-manager-images/mac/19-edit-button.png#lightbox)
 
-----

Wenn Sie auf **Bearbeiten** klicken, wird der Geräte-Editor für das ausgewählte virtuelle Gerät gestartet:

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

[![Bildschirm „Geräte-Editor“](xamarin-device-manager-images/win/20-device-editor-sml.png)](xamarin-device-manager-images/win/20-device-editor.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)
 
[![Bildschirm „Geräte-Editor“](xamarin-device-manager-images/mac/20-device-editor-sml.png)](xamarin-device-manager-images/mac/20-device-editor.png#lightbox)
 
-----

Der Bildschirm **Device Editor** (Geräte-Editor) führt in der ersten Spalte die Eigenschaften des virtuellen Geräts auf. In der zweiten Spalte sind die entsprechenden Werte für jede Eigenschaft enthalten. Wenn Sie eine Eigenschaft auswählen, wird rechts eine ausführliche Beschreibung dieser Eigenschaft angezeigt.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Im folgenden Screenshot wird beispielsweise die Eigenschaft `hw.lcd.density` von **420** in **240** geändert:

[![Beispiel für das Bearbeiten eines Geräts](xamarin-device-manager-images/win/21-device-editing-sml.png)](xamarin-device-manager-images/win/21-device-editing.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Im folgenden Screenshot wird beispielsweise die Eigenschaft `hw.lcd.density` von **320** in **240** und die Eigenschaft `hw.ramSize` in **768** geändert:
 
[![Beispiel für das Bearbeiten eines Geräts](xamarin-device-manager-images/mac/21-device-editing-sml.png)](xamarin-device-manager-images/mac/21-device-editing.png#lightbox)
 
-----

Klicken Sie auf die Schaltfläche **Speichern**, nachdem Sie die erforderlichen Änderungen an der Konfiguration vorgenommen haben.
Weitere Informationen zum Ändern der Eigenschaften von virtuellen Geräten finden Sie weiter unten in diesem Handbuch unter [Profileigenschaften](#properties).


 
### <a name="additional-options"></a>Zusätzliche Optionen

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Zusätzliche Optionen für die Arbeit mit Geräten sind im &hellip;-Menü in der oberen rechten Ecke verfügbar:

[![Position des Menüs „Zusätzliche Optionen“](xamarin-device-manager-images/win/22-overflow-menu-sml.png)](xamarin-device-manager-images/win/22-overflow-menu.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Zusätzliche Optionen für die Arbeit mit einem Gerät sind in dem Pulldownmenü verfügbar, das sich auf der linken Seite der Schaltfläche **Wiedergeben** befindet:

[![Position des Menüs „Zusätzliche Optionen“](xamarin-device-manager-images/mac/22-overflow-menu-sml.png)](xamarin-device-manager-images/mac/22-overflow-menu.png#lightbox)

-----

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Das Menü „Zusätzliche Optionen“ enthält folgende Elemente:

-   **Duplizieren und Bearbeiten:** Dupliziert das derzeit ausgewählte Gerät und öffnet dieses im Bildschirm **New Device** mit einem anderen eindeutigen Namen. Wenn Sie beispielsweise **VisualStudio_android-23_x86_phone** auswählen und auf **Duplicate and Edit** (Duplizieren und Bearbeiten) klicken, wird ein Zähler an den Namen angefügt:

    [![Bildschirm „Duplizieren und Bearbeiten“](xamarin-device-manager-images/win/23-dupe-and-edit-sml.png)](xamarin-device-manager-images/win/23-dupe-and-edit.png#lightbox)

-   **Im Explorer anzeigen:** Öffnet ein Fenster des Windows-Explorers in dem Ordner, der die Dateien für das virtuelle Gerät enthält. Wenn Sie beispielsweise **Nexus 5X API 25** auswählen und auf **Im Explorer anzeigen** klicken, wird folgendes Fenster geöffnet:

    [![Ergebnis beim Klicken auf „Im Explorer anzeigen“](xamarin-device-manager-images/win/24-reveal-in-explorer-sml.png)](xamarin-device-manager-images/win/24-reveal-in-explorer.png#lightbox)

-   **Auf Werkseinstellungen zurücksetzen:** Setzt das ausgewählte Gerät auf die Standardeinstellungen zurück. Dabei werden alle Benutzeränderungen am internen Zustand des Geräts, die während der Ausführung vorgenommen wurden, gelöscht. Dies wirkt sich nicht auf Änderungen aus, die während der Erstellung und Bearbeitung des virtuellen Geräts vorgenommen werden. Es wird ein Dialogfeld mit der Erinnerung angezeigt, dass das Zurücksetzen nicht rückgängig gemacht werden kann. Klicken Sie auf **Wipe user data** (Benutzerdaten löschen), um das Zurücksetzen zu bestätigen.

-   **Löschen:** Löscht das ausgewählte virtuelle Gerät dauerhaft.
    Es wird ein Dialogfeld mit der Erinnerung angezeigt, dass das Löschen eines Geräts nicht rückgängig gemacht werden kann. Klicken Sie auf **Löschen**, wenn Sie sich sicher sind, dass Sie das Gerät löschen möchten.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Das Menü „Zusätzliche Optionen“ enthält folgende Elemente:

-   **Bearbeiten:** Öffnet das derzeit ausgewählte Gerät wie zuvor in [Gerät bearbeiten](#device-edit) beschrieben im Geräte-Editor.

-   **Duplizieren und Bearbeiten:** Dupliziert das derzeit ausgewählte Gerät und öffnet dieses im Bildschirm **New Device** mit einem anderen eindeutigen Namen.
    Wenn Sie beispielsweise **Nexus 5X API 25** auswählen und auf **Duplicate and Edit** (Duplizieren und Bearbeiten) klicken, wird ein Zähler an den Namen angefügt:

    [![Bildschirm „Duplizieren und Bearbeiten“](xamarin-device-manager-images/mac/23-dupe-and-edit-sml.png)](xamarin-device-manager-images/mac/23-dupe-and-edit.png#lightbox)

-   **Im Finder zeigen:** Öffnet ein Fenster des macOS-Finders in dem Ordner, der die Dateien für das virtuelle Gerät enthält. Wenn Sie beispielsweise **Nexus 5X API 25** auswählen und auf **Im Finder zeigen** klicken, wird folgendes Fenster geöffnet:

    [![Ergebnis beim Klicken auf „Im Explorer anzeigen“](xamarin-device-manager-images/mac/24-reveal-in-finder-sml.png)](xamarin-device-manager-images/mac/24-reveal-in-finder.png#lightbox)

-   **Auf Werkseinstellungen zurücksetzen:** Setzt das ausgewählte Gerät auf die Standardeinstellungen zurück. Dabei werden alle Benutzeränderungen am internen Zustand des Geräts, die während der Ausführung vorgenommen wurden, gelöscht. Dies wirkt sich nicht auf Änderungen aus, die während der Erstellung und Bearbeitung des virtuellen Geräts vorgenommen werden. Es wird ein Dialogfeld mit der Erinnerung angezeigt, dass das Zurücksetzen nicht rückgängig gemacht werden kann. Klicken Sie auf **Wipe user data** (Benutzerdaten löschen), um das Zurücksetzen zu bestätigen.

-   **Löschen:** Löscht das ausgewählte virtuelle Gerät dauerhaft.
    Es wird ein Dialogfeld mit der Erinnerung angezeigt, dass das Löschen eines Geräts nicht rückgängig gemacht werden kann. Klicken Sie auf **Löschen**, wenn Sie sich sicher sind, dass Sie das Gerät löschen möchten.

-----

<a name="properties" />
 

## <a name="profile-properties"></a>Profileigenschaften

Die Bildschirme **Neues Gerät** und **Device Editor** (Geräte-Editor) führen in der ersten Spalte die Eigenschaften des virtuellen Geräts auf. In der zweiten Spalte sind die entsprechenden Werte für jede Eigenschaft enthalten. Wenn Sie eine Eigenschaft auswählen, wird rechts eine ausführliche Beschreibung dieser Eigenschaft angezeigt. Sie können die *Hardwareprofileigenschaften* und die *AVD-Eigenschaften* bearbeiten.
Hardwareprofileigenschaften (z.B. `hw.ramSize` und `hw.accelerometer`) beschreiben die physischen Merkmale des emulierten Geräts. Zu diesen Merkmalen gehören die Bildschirmgröße, die Menge des verfügbaren Arbeitsspeichers und ob ein Beschleunigungsmesser vorhanden ist. AVD-Eigenschaften geben die Vorgänge des virtuellen Android-Geräts bei der Ausführung an. AVD-Eigenschaften können beispielsweise konfiguriert werden, um anzugeben, wie das virtuelle Android-Gerät die Grafikkarte Ihres Entwicklungscomputers für das Rendering verwendet.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Sie können Eigenschaften mithilfe der folgenden Anleitung ändern:

-   Aktivieren Sie das Kontrollkästchen auf der rechten Seite einer booleschen Eigenschaft, um diese zu ändern:

    ![Ändern einer booleschen Eigenschaft](xamarin-device-manager-images/win/25-boolean-value.png)

-   Klicken Sie zum Ändern einer *enumerierten* Eigenschaft auf den Dropdownpfeil auf der rechten Seite der Eigenschaft, und wählen Sie einen neuen Wert aus.

    ![Ändern einer enumerierten Eigenschaft](xamarin-device-manager-images/win/27-enum-value.png)

-   Doppelklicken Sie zum Ändern einer Zeichenfolge oder einer ganzzahligen Eigenschaft auf die aktuelle Zeichenfolge oder auf die ganzzahlige Einstellung in der Wertespalte, und geben Sie einen neuen Wert ein.

    ![Ändern einer ganzzahligen Eigenschaft](xamarin-device-manager-images/win/26-integer-value.png)


# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Sie können Eigenschaften mithilfe der folgenden Anleitung ändern:

-   Aktivieren Sie das Kontrollkästchen auf der rechten Seite einer booleschen Eigenschaft, um diese zu ändern:

    ![Ändern einer booleschen Eigenschaft](xamarin-device-manager-images/mac/25-boolean-value.png)

-   Klicken Sie zum Ändern einer *enumerierten* Eigenschaft auf das Pulldownmenü auf der rechten Seite der Eigenschaft, und wählen Sie einen neuen Wert aus.

    ![Ändern einer enumerierten Eigenschaft](xamarin-device-manager-images/mac/27-enum-value.png)

-   Doppelklicken Sie zum Ändern einer Zeichenfolge oder einer ganzzahligen Eigenschaft auf die aktuelle Zeichenfolge oder auf die ganzzahlige Einstellung in der Wertespalte, und geben Sie einen neuen Wert ein.

    ![Ändern einer ganzzahligen Eigenschaft](xamarin-device-manager-images/mac/26-integer-value.png)


-----

In der folgenden Tabellen werden die Eigenschaften näher erläutert, die in den Bildschirmen **Neues Gerät** und **Device Editor** (Geräte-Editor) aufgeführt sind:

[!include[](~/android/includes/emulator-properties.md)]

Weitere Informationen zu diesen Eigenschaften finden Sie unter [Hardwareprofileigenschaften](https://developer.android.com/studio/run/managing-avds.html#hpproperties).


<a name="troubleshooting" />

## <a name="troubleshooting"></a>Problembehandlung

Im Folgenden werden häufige Probleme mit dem Xamarin Android-Geräte-Manager sowie Problemumgehungen beschrieben:

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

### <a name="android-sdk-in-non-standard-location"></a>Speicherort von Android SDK weicht vom Standard ab

Üblicherweise wird Android SDK an folgendem Speicherort installiert:

**C:\\Programme (x86)\\Android\\android-sdk**

Wenn die SDK nicht an diesem Speicherort installiert wurde, wird Ihnen beim Starten möglicherweise folgende Fehlermeldung angezeigt:

![Android SDK: Instanzfehler](xamarin-device-manager-images/win/32-sdk-error.png)

Gehen Sie folgendermaßen vor, um dieses Problem zu umgehen:

1. Navigieren Sie vom Windows-Desktop zu **C:\\Benutzer\\*Benutzername*\\AppData\\Roaming\\XamarinDeviceManager**:

    ![Speicherort der Protokolldatei des Xamarin-Geräte-Managers](xamarin-device-manager-images/win/33-log-files.png)

2. Doppelklicken Sie auf eine der Protokolldateien, um diese zu öffnen und den **Konfigurationsdateipfad** zu suchen. Zum Beispiel:

    [![Konfigurationsdateipfad in der Protokolldatei](xamarin-device-manager-images/win/34-config-file-path-sml.png)](xamarin-device-manager-images/win/34-config-file-path.png#lightbox)

3. Navigieren Sie zu diesem Speicherort, und doppelklicken Sie auf **user.config**, um die Datei zu öffnen. 

4. Suchen Sie in **user.config** das Element **&lt;UserSettings&gt;**, und fügen Sie diesem das Attribut **AndroidSdkPath** hinzu. Legen Sie dieses Attribut auf den Pfad fest, unter dem Android SDK auf Ihrem Computer installiert wurde, und speichern Sie die Datei. **&lt;UserSettings&gt;** würde beispielsweise folgendermaßen aussehen, wenn Android SDK unter **C:\\Programme\\Android\\SDK** installiert wäre:
        
    ```xml
    <UserSettings SdkLibLastWriteTimeUtcTicks="636409365200000000" AndroidSdkPath="C:\Programs\Android\SDK" />
    ```

Nachdem Sie diese Änderung an **user.config** vorgenommen haben, sollten Sie den Xamarin Android-Geräte-Manager starten können.

### <a name="snapshot-disables-wifi-on-android-oreo"></a>Momentaufnahme deaktiviert WLAN unter Android Oreo

Wenn Sie ein virtuelles Android-Gerät für Android Oreo mit simuliertem WLAN-Zugriff konfiguriert haben, verursacht ein Neustart des virtuellen Android-Geräts nach einer Momentaufnahme eventuell eine Deaktivierung des WLAN-Zugriffs.

Sie können Folgendes tun, um dieses Problem zu umgehen:

1. Wählen Sie das virtuelle Android-Gerät im Xamarin-Geräte-Manager aus.

2. Klicken Sie im Menü „Zusätzliche Optionen“ auf **Im Explorer anzeigen**.

3. Navigieren Sie zu **Momentaufnahme > default_boot**.

4. Löschen Sie die Datei **snapshot.pb**:

    [![Speicherort der snapshot.pb-Datei](xamarin-device-manager-images/win/36-delete-snapshot-sml.png)](xamarin-device-manager-images/win/36-delete-snapshot.png#lightbox)

5. Starten Sie das virtuelle Android-Gerät neu. 

Nach diesen Veränderungen startet das virtuelle Android-Gerät neu in einem Zustand, in dem das WLAN wieder funktioniert.


# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

### <a name="snapshot-disables-wifi-on-android-oreo"></a>Momentaufnahme deaktiviert WLAN unter Android Oreo

Wenn Sie ein virtuelles Android-Gerät für Android Oreo mit simuliertem WLAN-Zugriff konfiguriert haben, verursacht ein Neustart des virtuellen Android-Geräts nach einer Momentaufnahme eventuell eine Deaktivierung des WLAN-Zugriffs.

Sie können Folgendes tun, um dieses Problem zu umgehen:

1. Wählen Sie das virtuelle Android-Gerät im Xamarin-Geräte-Manager aus.

2. Klicken Sie im Menü „Zusätzliche Optionen“ auf **Im Finder zeigen**.

3. Navigieren Sie zu **Momentaufnahme > default_boot**.

4. Löschen Sie die Datei **snapshot.pb**:

    [![Speicherort der snapshot.pb-Datei](xamarin-device-manager-images/mac/36-delete-snapshot-sml.png)](xamarin-device-manager-images/mac/36-delete-snapshot.png#lightbox)

5. Starten Sie das virtuelle Android-Gerät neu. 

Nach diesen Veränderungen startet das virtuelle Android-Gerät neu in einem Zustand, in dem das WLAN wieder funktioniert.

-----


### <a name="generating-a-bug-report"></a>Erstellen eines Fehlerberichts

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Wenn Sie mit dem Xamarin Android-Geräte-Manager auf einen Fehler stoßen, der mit den oben genannten Tipps zur Problembehandlung nicht gelöst werden kann, erstellen Sie bitte einen Fehlerbericht, indem Sie einen Rechtsklick auf die Titelleiste ausführen und dann auf **Generate Bug Report** (Fehlerbericht erstellen) klicken:

![Ort des Menüelements zum Erstellen eines Fehlerberichts](xamarin-device-manager-images/win/35-bug-report.png)


# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio für Mac](#tab/vsmac)

Wenn Sie mit dem Xamarin.Android-Geräte-Manager auf einen Fehler stoßen, der mit den oben genannten Tipps zur Problembehandlung nicht gelöst werden kann, erstellen Sie bitte einen Fehlerbericht, indem Sie auf **Hilfe > Fehlerbericht erstellen** klicken:

![Ort des Menüelements zum Erstellen eines Fehlerberichts](xamarin-device-manager-images/mac/35-bug-report.png)

-----

 
 
## <a name="summary"></a>Zusammenfassung

In diesem Handbuch wurde der Xamarin Android-Geräte-Manager vorgestellt, der in Visual Studio für Mac und Xamarin für Visual Studio verfügbar ist. Es wurden grundlegende Features wie das Starten und Beenden des Android-Emulators, das Auswählen eines virtuellen Android-Geräts für die Ausführung, das Erstellen von neuen virtuellen Geräten sowie das Bearbeiten von virtuellen Geräten erläutert. Darüber hinaus wurde erläutert, wie Hardwareprofileigenschaften für die weitere Anpassung bearbeitet werden können.


## <a name="related-links"></a>Verwandte Links

- [Änderungen an den Tools des Android SDK](~/android/troubleshooting/sdk-cli-tooling-changes.md)
- [Debuggen mit dem Android SDK-Emulator](~/android/deploy-test/debugging/android-sdk-emulator/index.md)
- [Anmerkungen zu dieser Version von SDK Tools (Google)](https://developer.android.com/studiohttps://developer.xamarin.com/releases/sdk-tools.html)
- [avdmanager](https://developer.android.com/studio/command-line/avdmanager.html)
- [sdkmanager](https://developer.android.com/studio/command-line/sdkmanager.html)
