---
uid: aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
title: По промежуточного слоя OWIN в интегрированном конвейере IIS | Документация Майкрософт
author: Praburaj
description: В этой статье показано, как запускать компоненты по промежуточного слоя OWIN (ОМКС) в конвейере, интегрированном со службами IIS, и как задать событие конвейера, на котором выполняется ОМК. Необходимо...
ms.author: riande
ms.date: 11/07/2013
ms.assetid: d031c021-33c2-45a5-bf9f-98f8fa78c2ab
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
msc.type: authoredcontent
ms.openlocfilehash: 7d157fb6bd9e2ae9b55af41ef06c1eb5e6310ce1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500262"
---
# <a name="owin-middleware-in-the-iis-integrated-pipeline"></a>По промежуточного слоя OWIN в интегрированном конвейере IIS

[Прабураж сиагаражан](https://github.com/Praburaj), [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этой статье показано, как запускать компоненты по промежуточного слоя OWIN (ОМКС) в конвейере, интегрированном со службами IIS, и как задать событие конвейера, на котором выполняется ОМК. Прежде чем читать этот учебник, ознакомьтесь [с обзором](an-overview-of-project-katana.md) определения класса Katana и типа [запуска OWIN](owin-startup-class-detection.md) . Этот учебник написан на Рик Андерсон (( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Крис Росс (, прабураж Сиагаражан и Говард дайеркинг ( [@howard\_Дайеркинг](https://twitter.com/howard_dierking) ).

Хотя компоненты промежуточного слоя [OWIN](an-overview-of-project-katana.md) (ОМКС) в основном предназначены для работы в независимом от сервера конвейере, в интегрированном конвейере IIS можно также запустить ОМК (**классический режим *не* поддерживается**). ОМК можно сделать для работы в конвейере, интегрированном со службами IIS, установив следующий пакет из консоли диспетчера пакетов (PMC):

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample1.cmd)]

Это означает, что все платформы приложений, даже те, которые еще не могут работать вне IIS и System. Web, могут воспользоваться преимуществами существующих компонентов по промежуточного слоя OWIN. 

> [!NOTE]
> Все `Microsoft.Owin.Security.*` пакеты, поставляемые с новой системой идентификации в Visual Studio 2013 (например, файлы cookie, учетная запись Майкрософт, Google, Facebook, Twitter, [маркер носителя](http://self-issued.info/docs/draft-ietf-oauth-v2-bearer.html), OAuth, сервер авторизации, JWT, Azure Active Directory и службы федерации Active Directory), создаются как Омкс и могут использоваться как в самостоятельно размещенных, так и в размещенных в IIS сценариях.

## <a name="how-owin-middleware-executes-in-the-iis-integrated-pipeline"></a>Как выполняется по промежуточного слоя OWIN в интегрированном конвейере IIS

Для консольных приложений OWIN конвейер приложений, созданный с помощью [конфигурации запуска](owin-startup-class-detection.md) , задается порядком добавления компонентов с помощью метода `IAppBuilder.Use`. То есть конвейер OWIN в среде выполнения [Katana](an-overview-of-project-katana.md) будет обрабатывать Омкс в том порядке, в котором они были зарегистрированы с помощью `IAppBuilder.Use`. В конвейере интеграции IIS конвейер запросов состоит из [HttpModule](https://msdn.microsoft.com/library/ms178468(v=vs.85).aspx) , подписанных на предварительно определенный набор событий конвейера, таких как [beginRequest](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx), [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx), [AuthorizeRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)и т. д.

Если сравнить ОМК с объектом [HttpModule](https://msdn.microsoft.com/library/zec9k340(v=vs.85).aspx) в ASP.NET мире, то ОМК должен быть зарегистрирован в правильном предварительно определенном событии конвейера. Например, `MyModule` HttpModule будет вызываться, когда запрос поступает на стадию [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx) в конвейере:

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample2.cs?highlight=10)]

Чтобы ОМК мог участвовать в таком же порядке выполнения на основе событий, код среды выполнения [Katana](an-overview-of-project-katana.md) просматривает [конфигурацию запуска](owin-startup-class-detection.md) и подписывает каждый из компонентов по промежуточного слоя в интегрированное событие конвейера. Например, следующий ОМК и код регистрации позволяют просматривать регистрацию событий по умолчанию для компонентов по промежуточного слоя. (Более подробные инструкции по созданию класса запуска OWIN см. в разделе [Обнаружение класса запуска OWIN](owin-startup-class-detection.md).)

1. Создайте пустой проект веб-приложения и назовите его **owin2**.
2. В консоли диспетчера пакетов (PMC) выполните следующую команду: 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample3.cmd)]
3. Добавьте `OWIN Startup Class` и присвойте ему имя `Startup`. Замените созданный код следующим (изменения выделены):  

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample4.cs?highlight=5-7,15-36)]
4. Нажмите клавишу F5, чтобы запустить приложение.

Конфигурация запуска настраивает конвейер с тремя компонентами по промежуточного слоя, первые два отображения диагностических сведений и Последнее реагирование на события (а также отображение диагностической информации). Метод `PrintCurrentIntegratedPipelineStage` отображает событие интегрированного конвейера, которое вызывается этим по промежуточного слоя и сообщением. Выходные окна выводят следующие данные:

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample5.cmd)]

Среда выполнения Katana сопоставила каждый из компонентов по промежуточного слоя OWIN в [приксекутерекуессандлер](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx) по умолчанию, что соответствует событию конвейера IIS [PreRequestHandlerExecute](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx).

## <a name="stage-markers"></a>Маркеры этапа

Можно пометить Омкс для выполнения на конкретных стадиях конвейера с помощью метода расширения `IAppBuilder UseStageMarker()`. Чтобы запустить набор компонентов по промежуточного слоя на определенном этапе, вставьте маркер этапа сразу после последнего компонента, установленного во время регистрации. Существуют правила, на которых этап конвейера можно выполнить по промежуточного слоя и компоненты заказа, которые должны быть выполнены (правила объясняются далее в этом руководстве). Добавьте метод `UseStageMarker` в код `Configuration`, как показано ниже:

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample6.cs?highlight=13,19)]

`app.UseStageMarker(PipelineStage.Authenticate)` вызов настраивает все ранее зарегистрированные компоненты по промежуточного слоя (в данном случае два компонента диагностики) для запуска на этапе проверки подлинности конвейера. Последний компонент по промежуточного слоя (который отображает диагностику и реагирует на запросы) будет выполняться на `ResolveCache` этапе (событие [ресолверекуесткаче](https://msdn.microsoft.com/library/system.web.httpapplication.resolverequestcache.aspx) ).

Нажмите клавишу F5, чтобы запустить приложение. В окне Вывод отображается следующее:

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample7.cmd)]

## <a name="stage-marker-rules"></a>Правила маркера этапа

Компоненты промежуточного слоя Owin (ОМК) можно настроить для запуска в следующих событиях этапа конвейера OWIN:

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample8.cs)]

1. По умолчанию Омкс выполняется в последнем событии (`PreHandlerExecute`). Именно поэтому наш первый пример кода выводит «Приксекутерекуессандлер».
2. Можно использовать метод `app.UseStageMarker`, чтобы зарегистрировать ОМК для выполнения ранее, на любом этапе конвейера OWIN, указанном в перечислении `PipelineStage`.
3. Конвейер OWIN и конвейер IIS упорядочены, поэтому вызовы `app.UseStageMarker` должны выполняться по порядку. Обработчику событий нельзя присвоить событие, которое предшествует последнему событию, зарегистрированному в `app.UseStageMarker`. Например, *после* вызова:

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample9.cmd)]

   вызовы `app.UseStageMarker`, передающие `Authenticate` или `PostAuthenticate`, не будут учитываться и исключения не будут выдаваться. Омкс запускается на последнем этапе, по умолчанию `PreHandlerExecute`. Маркеры этапа используются для того, чтобы они выполнялись раньше. Если маркеры этапа заданы не по порядку, мы округляем до более раннего маркера. Иными словами, при добавлении маркера этапа будет указано "выполнять не позднее, чем на этапе X". ОМК запускается на более раннем маркере этапа, добавленном после них в конвейере OWIN.
4. Самый ранний этап вызовов `app.UseStageMarker` WINS. Например, при переключении порядка вызовов `app.UseStageMarker` из нашего предыдущего примера:

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample10.cs?highlight=13,19)]

   В окне вывода отобразятся следующие данные: 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample11.cmd)]

   Омкс все выполняется на этапе `AuthenticateRequest`, поскольку последняя ОМК, зарегистрированная в событии `Authenticate`, и событие `Authenticate` предшествуют всем остальным событиям.
