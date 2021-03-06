---
title: Erste Schritte mit iOS
ms.prod: xamarin
ms.assetid: D5453695-69C9-44BC-B226-5B86950956E2
author: topgenorth
ms.author: toopge
ms.date: 11/14/2017
ms.openlocfilehash: ab841c461356bd435db0c68e82c5e30d398d806a
ms.sourcegitcommit: 0a72c7dea020b965378b6314f558bf5360dbd066
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2018
---
# <a name="getting-started-with-ios"></a>Erste Schritte mit iOS

## <a name="requirements"></a>Anforderungen

Zusätzlich zu den aus unserem [Einstieg in Objective-C](~/tools/dotnet-embedding/get-started/objective-c/index.md) Handbuch, müssen Sie auch:

* [Xamarin.iOS 10.11](https://www.visualstudio.com/xamarin/) oder höher

## <a name="hello-world"></a>Hello World

Erstellen Sie zuerst ein einfaches Hello World-Beispiel in C# geschrieben.

### <a name="create-c-sample"></a>Erstellen der C#-Beispiel

Öffnen Sie Visual Studio für Mac, erstellen Sie eine neue iOS Class Library-Projekts, nennen Sie sie **Hello aus Csharp**, und speichern Sie es **~/Projects/hello-from-csharp**.

Ersetzen Sie den Code in der **MyClass.cs** -Datei mit den folgenden Codeausschnitt:

```csharp
using UIKit;
public class MyUIView : UITextView
{
    public MyUIView ()
    {
        Text = "Hello from C#";
    }
}
```

Erstellen Sie das Projekt, und die resultierende Assembly als gespeichert **~/Projects/hello-from-csharp/hello-from-csharp/bin/Debug/hello-from-csharp.dll**.

### <a name="bind-the-managed-assembly"></a>Die verwaltete Assembly binden

Nachdem Sie eine verwaltete Assembly haben, müssen binden Sie es, indem .NET Einbetten von aufrufen.

Wie in beschrieben die [Installation](~/tools/dotnet-embedding/get-started/install/install.md) Anleitung hierzu als Postbuildschritt in Ihrem Projekt eine benutzerdefinierte MSBuild-Ziel oder manuell:

```shell
cd ~/Projects/hello-from-csharp
objcgen ~/Projects/hello-from-csharp/hello-from-csharp/bin/Debug/hello-from-csharp.dll --target=framework --platform=iOS --outdir=output -c --debug
```

Das Framework wird in abgelegt **~/Projects/hello-from-csharp/output/hello-from-csharp.framework**.

### <a name="use-the-generated-output-in-an-xcode-project"></a>Verwenden Sie die generierte Ausgabe in einem Xcode-Projekt

Xcode öffnen, erstellen Sie eine neue iOS einzelne Ansicht-Anwendung, nennen Sie sie **Hello aus Csharp**, und wählen Sie die **Objective-C** Sprache.

Öffnen der **~/Projects/hello-from-csharp/output** Verzeichnis im Finder wählen **Hello aus csharp.framework**, ziehen Sie es in Xcode-Projekt, und legen Sie sie direkt über die **Hello aus Csharp**  Ordner des Projekts.

! [Drag & Drop-Framework] Images/Hello-from-CSharp-IOS-Drag-Drop-Framework.PNG)

Stellen Sie sicher, dass **Elemente kopieren, bei Bedarf** in der angezeigten Dialogfeld aktiviert ist, und klicken Sie auf **Fertig stellen**.

![Kopieren von Elementen, bei Bedarf](ios-images/hello-from-csharp-ios-copy-items-if-needed.png)

Wählen Sie die **Hello aus Csharp** Projekt, und navigieren Sie zu der **Hello aus Csharp** des Ziels **Registerkarte "Allgemein"**. In der **eingebettete binäre** Abschnitt, fügen Sie **Hello aus csharp.framework**.

![Eingebettete Binärdateien](ios-images/hello-from-csharp-ios-embedded-binaries.png)

Open **ViewController.m**, und Ersetzen Sie den Inhalt mit:

```objective-c
#import "ViewController.h"
#include "hello-from-csharp/hello-from-csharp.h"

@interface ViewController ()
@end

@implementation ViewController
- (void)viewDidLoad {
    [super viewDidLoad];

    MyUIView *view = [[MyUIView alloc] init];
    view.frame = CGRectMake(0, 200, 200, 200);
    [self.view addSubview: view];
}
@end
```

Einbetten von .NET unterstützt derzeit Bitcode iOS, nicht die für einige Projektvorlagen Xcode aktiviert ist. 

Deaktivieren sie in den projekteinstellungen:

![Bitcode-Option](../../images/ios-bitcode-option.png)

Führen Sie schließlich die Xcode-Projekt, und etwa Folgendes angezeigt wird:

![Hallo von C#-Beispiel im Simulator ausführen](ios-images/hello-from-csharp-ios.png)
