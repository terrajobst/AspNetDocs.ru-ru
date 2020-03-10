---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: Создание клиентского приложения OData V4 (C#) | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448122"
---
# <a name="create-an-odata-v4-client-app-c"></a>Создание клиентского приложения OData v4 (C#)

по [Майк Уоссон](https://github.com/MikeWasson)

В предыдущем руководстве вы создали базовую службу OData, которая поддерживает операции CRUD. Теперь создадим клиент для службы.

Запустите новый экземпляр Visual Studio и создайте новый проект консольного приложения. В диалоговом окне **Новый проект** выберите **установленные** **шаблоны** &gt; &gt; **Visual C#**  &gt; **Рабочий стол Windows**и выберите шаблон **консольное приложение** . Присвойте проекту имя &quot;Продуктсапп&quot;.

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> Вы также можете добавить консольное приложение в то же решение Visual Studio, которое содержит службу OData.

## <a name="install-the-odata-client-code-generator"></a>Установка генератора клиентского кода OData

Откройте меню **Средства** и выберите пункт **Расширения и обновления**. Выберите в **интернете** &gt; **галерею Visual Studio**. В поле поиска найдите &quot;генератор кода клиента OData&quot;. Нажмите кнопку **скачать** , чтобы установить VSIX. Возможно, вам будет предложено перезапустить Visual Studio.

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a>Локальное выполнение службы OData

Запустите проект Продуктсервице из Visual Studio. По умолчанию Visual Studio запускает браузер в корне приложения. Обратите внимание на URI; Это будет необходимо на следующем шаге. Не закрывайте приложение.

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> Если оба проекта помещаются в одно решение, запустите проект Продуктсервице без отладки. На следующем шаге необходимо, чтобы служба была запущена при изменении проекта консольного приложения.

## <a name="generate-the-service-proxy"></a>Создание прокси-сервера службы

Прокси-сервер службы — это класс .NET, который определяет методы для доступа к службе OData. Прокси-сервер преобразует вызовы метода в HTTP-запросы. Класс прокси будет создан путем запуска [шаблона T4](https://msdn.microsoft.com/library/bb126445.aspx).

Щелкните проект правой кнопкой мыши. Щелкните **Добавить** &gt; **Создать элемент**.

![](create-an-odata-v4-client-app/_static/image5.png)

В диалоговом окне **Добавление нового элемента** выберите **визуальные C# элементы** &gt; **код** &gt; **клиент OData**. Присвойте шаблону имя &quot;ProductClient.tt&quot;. Щелкните **Добавить** и щелкните предупреждение безопасности.

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

На этом этапе вы получите ошибку, которую можно проигнорировать. Visual Studio автоматически запускает шаблон, но сначала необходимо настроить некоторые параметры конфигурации.

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

Откройте файл Продуктклиент. OData. config. В элементе `Parameter` вставьте URI из проекта Продуктсервице (предыдущий шаг). Пример:

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

Снова запустите шаблон. В обозреватель решений щелкните правой кнопкой мыши файл ProductClient.tt и выберите команду **Запустить пользовательский инструмент**.

Шаблон создает файл кода с именем ProductClient.cs, определяющий прокси-сервер. При разработке приложения, если вы измените конечную точку OData, снова запустите шаблон, чтобы обновить учетную запись-посредник.

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a>Использование прокси-сервера службы для вызова службы OData

Откройте файл Program.cs и замените стандартный код следующим.

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

Замените значение *ServiceUri* на URI службы ранее.

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

При запуске приложения он должен вывести следующее:

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
