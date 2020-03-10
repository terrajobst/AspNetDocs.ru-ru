---
uid: mvc/overview/getting-started/introduction/getting-started
title: Начало работы с ASP.NET MVC 5 | Документация Майкрософт
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ca39bc37c757c0452cf56624c8e37c04df4b41f2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487956"
---
# <a name="getting-started-with-aspnet-mvc-5"></a>Начало работы с ASP.NET MVC 5

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](../../../../includes/razor.md)]

В этом учебнике рассматриваются основы создания веб-приложения ASP.NET MVC 5 с помощью [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017). Окончательный исходный код для учебника находится на сайте [GitHub](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie).

Это руководство было написано [Скотт Гатри (](https://weblogs.asp.net/scottgu/) (Twitter[@scottgu](https://twitter.com/scottgu) ), [скотт Hanselman](http://www.hanselman.com/blog/) (Twitter: [@shanselman](https://twitter.com/shanselman) ) и [Рик Андерсон (](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )

Для развертывания этого приложения в Azure требуется учетная запись Azure:

- Вы можете [открыть учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) — вы получаете кредиты, которые можно использовать для пробного использования платных служб Azure, и даже после их использования вы можете удержать учетную запись и использовать бесплатные службы Azure.
- Вы имеете возможность [активировать преимущества подписчика MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) — ваша подписка MSDN каждый месяц приносит вам кредиты, которые можно использовать для оплаты за службы Azure.

## <a name="get-started"></a>Начало работы

Начните с [установки Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017). Затем откройте Visual Studio.

Visual Studio — это интегрированная среда разработки (IDE). Как и при использовании Microsoft Word для написания документов, для создания приложений используется интегрированная среда разработки. В Visual Studio есть список, в нижней части которого показаны различные доступные параметры. Также есть меню, предоставляющее еще один способ выполнения задач в интегрированной среде разработки. Например, вместо выбора **нового проекта** на **начальной странице**можно использовать строку меню и выбрать **файл** > **Новый проект**.

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a>Создание первого приложения

На **начальной странице**выберите **Новый проект**. В диалоговом окне **Новый проект** выберите категорию **визуальные C# элементы** слева, затем **веб**, а затем выберите шаблон проекта **веб-приложение ASP.NET (.NET Framework)** . Присвойте проекту имя "MvcMovie" и нажмите кнопку **ОК**.

![](getting-started/_static/image2.png)

В диалоговом окне **Создание веб-приложения ASP.NET** выберите **MVC** и нажмите кнопку **ОК**.

![](getting-started/_static/image3.png)

Visual Studio использовала шаблон по умолчанию для только что созданного проекта MVC ASP.NET, поэтому у вас есть рабочее приложение, не делая ничего. Это простой "Hello World!" и это хорошее место для запуска приложения.

![](getting-started/_static/image4.png)

Нажмите клавишу **F5**, чтобы запустить отладку. При нажатии клавиши **F5**Visual Studio запускает [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) и запускает веб-приложение. Затем Visual Studio запустит браузер и откроет домашнюю страницу приложения. Обратите внимание, что в адресной строке браузера указано `localhost:port#` и не что-то вроде `example.com`. Это связано с тем, что `localhost` всегда указывает на локальный компьютер, который в данном случае выполняет только что созданное приложение. Когда Visual Studio выполняет веб-проект, для веб-сервера используется случайный порт. На рисунке ниже показан номер порта 1234. При запуске приложения вы увидите другой номер порта.

![](getting-started/_static/image5.png)

Этот шаблон по умолчанию предназначается для `Home`, `Contact`и `About` страниц. На рисунке ниже не показаны ссылки **Домашняя страница**, **сведения о программе**и **контакт** . В зависимости от размера окна браузера может потребоваться щелкнуть значок навигации, чтобы просмотреть эти ссылки.

![](getting-started/_static/image6.png)

Приложение также обеспечивает поддержку для регистрации и входа в систему. Следующим шагом является изменение способа работы этого приложения и немного подробнее о ASP.NET MVC. Закройте приложение ASP.NET MVC и давайте изменим код.

Список текущих руководств см. в [статье рекомендации по MVC](../mvc-learning-sequence.md).

## <a name="see-this-app-running-on-azure"></a>См. приложение, работающее в Azure

Вы хотите увидеть готовый сайт, работающий как активное веб-приложение? Вы можете развернуть полную версию приложения в учетной записи Azure, просто нажав кнопку ниже.

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

Для развертывания этого решения в Azure необходима учетная запись Azure. Если у вас еще нет учетной записи, используйте один из следующих параметров, чтобы создать его.

- [Откройте учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) — вы получаете кредиты, которые можно использовать для пробного использования платных служб Azure, и даже после их использования вы можете удержать учетную запись и использовать бесплатные службы Azure.
- [Активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers) . Ваша подписка Visual Studio предоставляет Вам кредиты каждый месяц, который можно использовать для платных служб Azure.

> [!div class="step-by-step"]
> [Дальше](adding-a-controller.md)
