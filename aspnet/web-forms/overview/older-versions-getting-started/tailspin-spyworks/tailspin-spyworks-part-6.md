---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: Часть 6. членство в ASP.NET | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. Часть 6 добавляет членство в ASP.NET.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454884"
---
# <a name="part-6-aspnet-membership"></a>Часть 6. членство в ASP.NET

кем [Джо Stagner)](https://github.com/JoeStagner)

> В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET. Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.
> 
> В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. Часть 6 добавляет членство в ASP.NET.

## <a id="_Toc260221672"></a>Работа с членством в ASP.NET

![](tailspin-spyworks-part-6/_static/image1.png)

Щелкните Безопасность.

![](tailspin-spyworks-part-6/_static/image1.jpg)

Убедитесь, что используется проверка подлинности с помощью форм.

![](tailspin-spyworks-part-6/_static/image2.jpg)

Используйте ссылку "создать пользователя", чтобы создать несколько пользователей.

![](tailspin-spyworks-part-6/_static/image3.jpg)

По завершении просмотрите окно обозреватель решений и обновите представление.

![](tailspin-spyworks-part-6/_static/image2.png)

Обратите внимание, что ASPNETDB. Создан MDF. Этот файл содержит таблицы для поддержки основных служб ASP.NET, таких как членство.

Теперь мы можем приступить к реализации процесса извлечения.

Начните с создания страницы CheckOut. aspx.

Страница CheckOut. aspx должна быть доступна только пользователям, вошедшим в систему, поэтому мы будем ограничивать доступ к вошедшему в систему пользователям и перенаправлять пользователей, которые не вошли на страницу входа.

Для этого добавьте следующий элемент в раздел конфигурации нашего файла Web. config.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

Шаблон для приложений веб-форм ASP.NET автоматически добавил раздел проверки подлинности в наш файл Web. config и создал страницу входа по умолчанию.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

Необходимо изменить файл кода для Login. aspx, чтобы перенести корзину анонимных покупок при входе пользователя в систему. Измените событие загрузки страницы\_, как показано ниже.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

Затем добавьте обработчик событий с ведением журнала следующего вида, чтобы задать имя сеанса для вновь вошедшего в систему пользователя и изменить временный идентификатор сеанса в корзине для покупок на пользователя, вызвав метод Мигратекарт в нашем классе Мишоппингкарт. (Реализовано в CS-файле)

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

Реализуйте метод Мигратекарт () следующим образом.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

В файле Checkout. aspx мы будем использовать EntityDataSource и GridView на странице извлечения, как это делалось на странице покупательской корзины.

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

Обратите внимание, что наш элемент управления GridView Указывает обработчик событий "ондатабаунд" с именем Милист\_RowDataBound, так что давайте реализуем этот обработчик событий следующим образом.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

Этот метод сохраняет накопленный итог корзины покупок по мере привязки каждой строки и обновляет нижнюю строку GridView.

На этом этапе мы реализовали представление заказа для просмотра.

Давайте обработаем пустого сценария корзины, добавив несколько строк кода на нашу страницу\_загрузить событие:

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

Когда пользователь нажимает кнопку "Отправить", в обработчике событий нажатия кнопки "Отправить" будет выполнен следующий код.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

"Мясо" процесса отправки заказа должен быть реализован в методе Субмитордер () нашего класса Мишоппингкарт.

Субмитордер будет:

- Возьмите все строки из корзины для покупок и используйте их для создания новой записи заказа и связанных записей OrderDetails.
- Рассчитайте дату отгрузки.
- Очистите корзину для покупок.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

Для целей этого примера приложения мы вычислим дату отгрузки, просто добавив два дня к текущей дате.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

Запуск приложения теперь позволит нам протестировать процесс покупки с начала до конца.

> [!div class="step-by-step"]
> [Назад](tailspin-spyworks-part-5.md)
> [Вперед](tailspin-spyworks-part-7.md)
