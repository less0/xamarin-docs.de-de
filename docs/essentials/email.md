---
title: Xamarin.Essentials-e-Mail
description: Die e-Mail-Klasse ermöglicht einer Anwendung die Standard-e-Mail-Anwendung mit einer angegebenen Informationen, einschließlich der Betreff, Text und die Empfängerliste (TO, CC, BCC) zu öffnen.
ms.assetid: 5FBB6FF0-0E7B-4C29-8F06-91642AF12629
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 3fee30e31dc18665d59f944462959fd3f8166968
ms.sourcegitcommit: 4db5f5c93f79f273d8fc462de2f405458b62fc02
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/19/2018
---
# <a name="xamarinessentials-email"></a>Xamarin.Essentials-e-Mail

![Vorabversion NuGet](~/media/shared/pre-release.png)

Die **E-Mail** Klasse ermöglicht einer Anwendung, die die Standard-e-Mail-Anwendung mit einer angegebenen Informationen, einschließlich der Betreff, Text und die Empfängerliste (TO, CC, BCC) zu öffnen.

## <a name="using-email"></a>Per E-Mail

Fügen Sie einen Verweis auf Xamarin.Essentials in Ihrer Klasse hinzu:

```csharp
using Xamarin.Essentials;
```

Die e-Mail-Funktionalität kann durch Aufrufen der `ComposeAsync` Methode eine `EmailMessage` , Informationen über die e-Mail-Adresse enthält:

```csharp
public class EmailTest
{
    public async Task SendEmail(string subject, string body, List<string> recipients)
    {
        try
        {
            var message = new EmailMessage
            {
                Subject = subject,
                Body = body,
                To = recipients,
                //Cc = ccRecipients,
                //Bcc = bccRecipients
            }
            await Email.ComposeAsync(message);
        }
        catch (FeatureNotSupportedException fbsEx)
        {
            // Sms is not supported on this device
        }
        catch (Exception ex)
        {
            // Some other exception occured
        }
    }
}
```

## <a name="api"></a>API

- [E-Mail-Quellcode](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Email)
- [E-Mail-API-Dokumentation](xref:Xamarin.Essentials.Email)
