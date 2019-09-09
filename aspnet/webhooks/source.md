---
uid: webhooks/source
title: ASP.NET веб-перехватчики и пакеты NuGet | Документация Майкрософт
author: rick-anderson
description: Ссылки на исходный код веб-перехватчиков ASP.NET и пакеты NuGet
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000706"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET веб-перехватчики, исходный код и пакеты NuGet

Microsoft ASP.NET веб-перехватчики входят в Microsoft ASP.NET семейства модулей и размещаются в виде проекта с [открытым исходным кодом на сайте GitHub](https://github.com/aspnet/WebHooks). Это означает, что мы принимаем вклады, но перед отправкой запроса на вытягивание ознакомьтесь с [рекомендациями по публикации](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) .

Эта интерактивная документация, которую вы читаете сейчас, также размещена [на сайте GitHub в виде открытого кода](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) , а также принимает вклады.

## <a name="nuget-packages"></a>Пакеты NuGet

[Пакеты NuGet](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) делятся на три части:

* [Общие](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Общий пакет, который совместно используется отправителями и получателями.

* [Отправитель](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Набор пакетов, поддерживающих отправку собственных веб-перехватчиков другим пользователям. Функция отправки веб-перехватчиков более подробно описана в разделе [отправляются](sending/senders.md)вызовы.

* [Получатели](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Набор пакетов, поддерживающих получение веб-перехватчиков от других. Дополнительные сведения о возможностях получения веб-перехватчиков [см. в](receiving/index.md)этой статье.
