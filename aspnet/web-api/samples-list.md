---
uid: web-api/samples-list
title: Список примеров веб-API — ASP.NET 4. x
author: rick-anderson
description: Список примеров веб-API ASP.NET для ASP.NET 4. x
ms.author: riande
ms.date: 09/18/2012
ms.custom: seoapril2019
ms.assetid: 8cbd9d7f-7027-4390-b098-cb81a63ecd6f
msc.legacyurl: /web-api/samples-list
msc.type: content
ms.openlocfilehash: 24368fc80e7fc3c840f1f1f9accf13fa15a06c1b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484266"
---
# <a name="web-api-samples-list"></a>Список примеров веб-API

## <a name="httpclient-samples"></a>Примеры HttpClient

**Пример использования Bing для преобразования** | [и источник VS 2012](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/BingTranslateSample)

Показывает, как вызвать [службу Microsoft Translator](https://msdn.microsoft.com/library/ff512419.aspx) с помощью класса **HttpClient** . API службы Microsoft Translator требует маркер OAuth, который получает приложение, отправив запрос серверу маркеров Azure для каждого запроса к службе переводчика. Результат, полученный от сервера маркеров, передается в запрос, отправленный службе перевода. Перед запуском этого примера необходимо получить [ключ приложения из Azure Marketplace](https://msdn.microsoft.com/library/hh454950.aspx) и ввести сведения в классе Sample акцесстокенмессажехандлер.

 | [подробного описания](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/downloading-a-google-map-to-local-file.aspx) для **примера Google Maps** | [VS 2012](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/GoogleMapsSample)

Использует **HttpClient** для загрузки карты Redmond, WA из [Google Maps API](https://developers.google.com/maps/), сохраняет ее в качестве локального файла и открывает средство просмотра изображений по умолчанию.

Пример | [подробного описания](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/extending-httpclient-with-oauth-to-access-twitter.aspx) **клиента Twitter** | [VS 2012 источник](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/TwitterSample)

Показывает, как написать простой клиент Twitter с помощью **HttpClient**. В примере используется **HttpMessageHandler** для вставки данных проверки подлинности OAuth в исходящий **HttpRequestMessage**. Результат из Twitter считывается с помощью JSON.NET. Перед запуском этого примера необходимо получить [ключ приложения из Twitter](https://dev.twitter.com/)и заполнить сведения в классе примера оаусмессажехандлер.

**Пример международного банка** | [подробное описание](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/httpclient-is-here.aspx) | [vs 2010 Source](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net40) | [VS 2012 Source](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net45)

Показывает, как получить данные с сайта мирового банка данных, используя JSON.NET для анализа результата.

## <a name="web-api-samples"></a>Примеры веб-API

**Начало работы с веб-API ASP.NET** | [источника VS 2012](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)

Показывает, как создать базовый веб-API, поддерживающий HTTP-запросы GET. Содержит исходный код для учебника, посвященного [первому веб-API ASP.NETу](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).

**Веб-API ASP.NET сценарии JavaScript: комментарии** | [VS 2012, источник](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)

Показывает, как использовать веб-API ASP.NET для создания веб-API, поддерживающих клиенты браузера, и легко вызывать их с помощью jQuery.

**Диспетчер контактов** | [источник VS 2010](https://code.msdn.microsoft.com/Contact-Manager-Web-API-0e8e373d)

В этом примере для создания простого приложения диспетчера контактов используется веб-API ASP.NET. Приложение состоит из веб-API диспетчера контактов, который используется приложением MVC ASP.NET и приложением Windows Phone для просмотра списка контактов и управления им.

**Пример пакетной обработки** | [подробное описание](http://trocolate.wordpress.com/2012/07/19/mitigate-issue-260-in-batching-scenario/) | [VS 2012 Source](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/BatchSample)

Показывает, как реализовать пакетную обработку HTTP в ASP.NET. Пакетная обработка состоит в размещении нескольких HTTP-запросов в одном теле составного объекта MIME, который затем отправляется на сервер в качестве HTTP-запроса POST. Запросы обрабатываются по отдельности, а ответы помещаются в другой составной объект MIME, который возвращается клиенту.

**Образец контроллера содержимого** | [подробное описание](https://blogs.msdn.com/b/henrikn/archive/2012/02/24/async-actions-in-asp-net-web-api.aspx) | [vs 2010 Source](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net40) | [VS 2012 Source](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net45)

Показывает, как асинхронно считывать и записывать сущности запросов и ответов с помощью потоков. В примере контроллера есть два действия: действие вставки, которое считывает тело объекта запроса асинхронно и сохраняет его в локальном файле и действие GET, которое возвращает содержимое локального файла.

**Пример пользовательского распознавателя сборок** | [источник VS 2012](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomAssemblyResolverSample)

Показывает, как изменить веб-API ASP.NET для поддержки обнаружения контроллеров из динамически загруженной сборки библиотеки. В примере реализуется пользовательский **иассемблиесресолвер** , который вызывает реализацию по умолчанию, а затем добавляет сборку библиотеки к результатам по умолчанию.

**Образец модуля форматирования пользовательских типов мультимедиа** | [подробное описание](https://blogs.msdn.com/b/henrikn/archive/2012/04/23/using-cookies-with-asp-net-web-api.aspx) | [VS 2010 Source](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomMediaTypeFormatterSample)

Показывает, как создать пользовательский модуль форматирования типа мультимедиа с помощью базового класса **буффередмедиатипеформаттер** . Этот базовый класс предназначен для модулей форматирования, которые в основном используют синхронные операции чтения и записи. В примере показано, как подключить модуль форматирования типов мультимедиа, зарегистрировав его как часть **HttpConfiguration** для вашего приложения. Обратите внимание, что также можно напрямую использовать базовый класс **MediaTypeFormatter** для модулей форматирования, в которых в основном используются асинхронные операции чтения и записи.

**Образец настраиваемой привязки параметров** | [подробное описание](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx) | [VS 2010 Source](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomParameterBinding)

Показывает, как настроить процесс привязки параметров, который определяет, каким способом данные из запроса привязаны к параметрам действий. В этом примере контроллер Home имеет четыре действия:

1. БиндпринЦипал показывает, как привязать параметр IPrincipal из пользовательского универсального субъекта, а не из HTTP-сообщения GET.
2. Биндкустомкомплекстипефромуриорбоди показывает, как привязать параметр сложного типа, который может поступать либо из тела сообщения, либо из URI запроса HTTP-сообщения POST.
3. Биндкустомкомплекстипефромуривисренамедпроперти показывает, как привязать параметр сложного типа к переименованному свойству, которое берется из URI запроса сообщения HTTP POST.
4. Постмултиплепараметерсфромбоди показывает, как привязать несколько параметров к тексту сообщения POST;

**Пример загрузки файла** | [подробное описание](https://blogs.msdn.com/b/henrikn/archive/2012/03/01/file-upload-and-asp-net-web-api.aspx) | [VS 2012 Source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/FileUploadSample)

Показывает, как передавать файлы в **ApiController** с помощью передачи составного файла MIME, а также как настроить уведомления о ходе выполнения с помощью **HttpClient** с использованием **прогресснотификатионхандлер**. Контроллер считывает содержимое файла HTML асинхронно и записывает одну или несколько частей текста в локальный файл. Ответ содержит сведения о отправленном файле (или файлах).

**Отправка файла в хранилище BLOB-объектов Azure образец** | [подробное описание](https://blogs.msdn.com/b/yaohuang1/archive/2012/07/02/asp-net-web-api-and-azure-blob-storage.aspx) | [VS 2012 Source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/AzureBlobsFileUploadSample)

Этот пример похож на пример передачи файла, но вместо сохранения отправленных файлов на локальном диске он асинхронно отправляет файлы в [хранилище BLOB-объектов Azure](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs) с помощью [пакета Windows Azure SDK для .NET](https://www.windowsazure.com/develop/net/). Он также предоставляет механизм для перечисления больших двоичных объектов, имеющихся в [контейнере хранилища BLOB-объектов Azure](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs). Вы можете испытать пример, выполняемый в **эмуляторе хранения Azure** , который поставляется вместе с пакетом Azure SDK. Если у вас есть [учетная запись хранения Azure](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs), вы также можете использовать ее в реальной службе хранилища.

**Пример конвейера обработчика сообщений Http** | [подробное описание](https://blogs.msdn.com/b/henrikn/archive/2012/08/07/httpclient-httpclienthandler-and-httpwebrequesthandler.aspx) | [VS 2010 Source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/HttpMessageHandlerPipelineSample)

Показывает, как подключать экземпляры **HttpMessageHandler** как на клиенте (**HttpClient**), так и на сервере (веб-API ASP.NET). В этом примере один и тот же обработчик используется как на клиенте, так и на сервере. Несмотря на то, что один и тот же обработчик в обоих местах будет работать редко, объектная модель одинакова на стороне клиента и сервера.

**Пример передачи JSON** | [источник VS 2012](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/JsonUploadSample)

Показывает, как отправить и скачать JSON в **ApiController**и из него. В примере используется минимальный **ApiController** и осуществляется доступ к нему с помощью **HttpClient**.

**Пример гибридного веб** -приложения | [подробное описание](https://blogs.msdn.com/b/henrikn/archive/2012/03/03/async-mashups-using-asp-net-web-api.aspx) | [VS 2012, источник](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MashupSample)

Показывает, как асинхронно обращаться к нескольким удаленным сайтам из действия **ApiController** . При каждом попадании в действие запросы выполняются асинхронно, поэтому потоки не блокируются.

**Пример трассировки памяти** | [подробное описание](https://blogs.msdn.com/b/roncain/archive/2012/04/12/tracing-in-asp-net-web-api.aspx) | [VS 2010 Source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MemoryTracingSample)

Этот пример проекта создает пакет NuGet, который будет устанавливать пользовательский модуль записи трассировки в памяти в веб-API ASP.NET приложения.

**MongoDB образец** | [подробное описание](https://blogs.msdn.com/b/henrikn/archive/2012/02/19/using-web-api-with-mongodb.aspx) | [VS 2012 Source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MongoSample)

Показывает, как использовать MongoDB в качестве постоянного хранилища для **ApiController**с помощью шаблона репозитория.

**Образец обработчика текста ответа** , | [источник VS 2012](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ResponseEntityProcessorSample)

Показывает, как скопировать сущность ответа (то есть текст ответа HTTP) в локальный файл перед его передачей клиенту и асинхронно выполнить дополнительную обработку этого файла. В примере реализуется **HttpMessageHandler** , который заключает в оболочку сущность Response, которая записывает себя в выходные данные как обычные и в локальный файл.

**Отправка образца** | [подробного описания](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/push-and-pull-streams-using-httpclient.aspx) | [VS 2012 в источнике](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/UploadXDocumentSample)

Показывает, как передать объект XDocument в **ApiController** с помощью **пушстреамконтент** и **HttpClient**.

**Пример проверки** | [источник VS 2010](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ValidationSample)

Показывает, как можно использовать атрибуты проверки в моделях в ASP.NET WebAPI для проверки содержимого HTTP-запроса. Демонстрирует, как помечать свойства как обязательные, как использовать как определенные платформой, так и пользовательские атрибуты проверки, чтобы закомментировать модель и как вернуть ответы об ошибках для недопустимых состояний модели.

**Пример веб-формы** | [подробное описание](https://blogs.msdn.com/b/henrikn/archive/2012/02/23/using-asp-net-web-api-with-asp-net-web-forms.aspx) | [VS 2010 Source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/WebFormSample)

Показывает ApiController, добавленный в проект веб-форм.

**[Пример Рестбугс](https://github.com/howarddierking/RestBugs)**

Рестбугс — это простое приложение для отслеживания ошибок, которое показывает, как использовать веб-API ASP.NET и новую клиентскую библиотеку HTTP для создания системы, управляемой на основе файлов мультимедиа. Пример включает как клиентские, так и серверные реализации с использованием веб-API ASP.NET. Сервер использует пользовательский модуль форматирования Razor для создания представлений ресурсов. В примере также представлен сервер Node. js, иллюстрирующий преимущества использования технологии «компакт-диска» для отделения клиентов от серверов.
