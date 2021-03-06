---
title: Xamarin.Essentials
description: Xamarin.Essentials bietet eine einzelne plattformübergreifende-API, die arbeitet mit iOS, Android oder uwp-Anwendung, die aus zugegriffen werden kann, freigegebenen Code unabhängig davon, wie die Benutzeroberfläche erstellt wird.
ms.assetid: B2669C48-B659-4854-BD80-FEB0E876F5B9
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 2e0abff4d0408d3db11ab95f1debc6621f609d86
ms.sourcegitcommit: c024f29ff730ae20c15e99bfe0268a0e1c9d41e5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/23/2018
---
# <a name="get-started-with-xamarinessentials"></a>Erste Schritte mit Xamarin.Essentials

![Vorabversion NuGet](~/media/shared/pre-release.png)

Xamarin.Essentials bietet eine einzelne plattformübergreifende-API, die arbeitet mit iOS, Android oder uwp-Anwendung, die aus zugegriffen werden kann, freigegebenen Code unabhängig davon, wie die Benutzeroberfläche erstellt wird.

## <a name="platform-support"></a>Plattformunterstützung

Xamarin.Essentials unterstützt die folgenden Plattformen und Betriebssysteme:

| Plattform | Version |
| --- | --- |
| Android | 4.4 (API-19) oder höher |
| iOS |10,0 oder höher |
| UWP | 10.0.16299.0 oder höher |

## <a name="installation"></a>Installation

Xamarin.Essentials steht als NuGet-Paket, das alle vorhandenen oder neuen Projekt, das mit Visual Studio hinzugefügt werden kann.

1. Herunterladen und installieren [Visual Studio](http://visualstudio.com) mit der [Visual Studio-Tools für Xamarin](~/cross-platform/get-started/installation/index.md).

2. Öffnen Sie ein vorhandenes Projekt, oder erstellen ein neues Projekts mithilfe der Vorlage der leeren App unter **Visual Studio c#** (Android, iPhone und iPad oder Cross-Platform). **Wichtige**: Wenn hinzufügen zu einem uwp-Projekt stellen Sie sicher in den Projekteigenschaften Build 16299 oder höher festgelegt ist.

3. Hinzufügen der **Xamarin.Essentials** NuGet-Paket jedem Projekt:

    # <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

    Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Namen der Projektmappe, und wählen Sie **NuGet-Pakete verwalten**. Suchen Sie nach **Xamarin.Essentials** und installieren Sie das Paket in **alle** Projekte, einschließlich Android, iOS, universelle Windows-Plattform und .NET Standard-Bibliotheken.

    > [!TIP]
    > Überprüfen Sie die **Vorabversion einschließen** Feld während der [ **Xamarin.Essentials** NuGet](https://www.nuget.org/packages/Xamarin.Essentials) ist in der Vorschau.

    # <a name="visual-studio-for-mactabmacos"></a>[Visual Studio für Mac](#tab/macos)

    Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Projektnamen, und wählen Sie **hinzufügen > NuGet-Pakete hinzufügen...** . Suchen Sie nach **Xamarin.Essentials** und installieren Sie das Paket in **alle** Projekte, einschließlich Android, iOS und .NET Standard-Bibliotheken.

    > [!TIP]
    > Überprüfen Sie die **Vorabversion Pakete anzeigen, die** Feld während der [ **Xamarin.Essentials** NuGet](https://www.nuget.org/packages/Xamarin.Essentials) ist in der Vorschau.

    -----

4. Fügen Sie einen Verweis auf Xamarin.Essentials in einer C#-Klasse, die APIs verweisen.

    ```csharp
    using Xamarin.Essentials;
    ```

5. Xamarin.Essentials fordert plattformspezifischen-Setup:

    # <a name="androidtabandroid"></a>[Android](#tab/android)

    In der Android-Projekts `MainLauncher` oder eine beliebige `Activity` also gestartete Xamarin.Essentials muss initialisiert werden, der `OnCreate` Methode:

    ```csharp
    Xamarin.Essentials.Platform.Init(this, bundle);
    ```

    Behandeln Sie Common Language Runtime-Berechtigungen für Android müssen Xamarin.Essentials erhalten alle `OnRequestPermissionsResult`. Fügen Sie den folgenden Code für alle `Activity` Klassen:

    ```csharp
    public override void OnRequestPermissionsResult(int requestCode, string[] permissions, [GeneratedEnum] Android.Content.PM.Permission[] grantResults)
    {
        Xamarin.Essentials.Platform.OnRequestPermissionsResult(requestCode, permissions, grantResults);

        base.OnRequestPermissionsResult(requestCode, permissions, grantResults);
    }
    ```

    # <a name="iostabios"></a>[iOS](#tab/ios)

    Ohne zusätzliche Einrichtung erforderlich.

    # <a name="uwptabuwp"></a>[UNIVERSELLE WINDOWS-PLATTFORM](#tab/uwp)

    Ohne zusätzliche Einrichtung erforderlich.

    -----

6. Führen Sie die [Xamarin.Essentials Handbücher](index.md) , mit denen Sie kopieren und fügen Codeausschnitte für jede Funktion.

## <a name="other-resources"></a>Weitere Ressourcen

Wir empfehlen Entwicklern, die noch nicht mit Xamarin Besuch [erste Schritte mit Xamarin-Entwicklung](~/cross-platform/getting-started/index.md).

Besuchen Sie die [Xamarin.Essentials GitHub-Repository](http://github.com/xamarin/Essentials) , finden Sie unter dem aktuellen Quellcode, was als Nächstes kommt Ausführen der Beispiele, und schließen das Repository. Beiträge aus der Community sind Willkommen!

Navigieren Sie durch die [API-Dokumentation](xref:Xamarin.Essentials) für jede Funktion der Xamarin.Essentials.
