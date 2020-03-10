---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: Жизненный цикл приложения ASP.NET MVC 5 | Документация Майкрософт
author: cephalin
description: Скачайте PDF-документ, в котором приведена схема жизненного цикла приложения ASP.NET MVC 5. Этот документ содержит обобщенное представление жизненного цикла MVC...
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: f4a9b3fb61552b070db11fba617b5627fcd71cd5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470328"
---
# <a name="lifecycle-of-an-aspnet-mvc-5-application"></a>Жизненный цикл приложения ASP.NET MVC 5

по [Цефас](https://github.com/cephalin)

[Скачать PDF-документ](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

Здесь можно скачать документ в формате PDF, который выводит на диаграмму жизненный цикл каждого приложения ASP.NET MVC 5, от получения HTTP-запроса до отправки ответа HTTP обратно клиенту. Он разработан как образовательный инструмент для тех, кто не знаком с ASP.NET MVC, а также как справочные материалы для тех, кто должен перейти к конкретным аспектам приложения. Документ PDF имеет следующие возможности.

- Соответствующие этапы [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) помогут вам понять, где MVC интегрируется в [жизненный цикл приложения ASP.NET](https://msdn.microsoft.com/library/bb470252.aspx).
- Высокоуровневое представление жизненного цикла приложения MVC, в котором можно понять основные этапы, через которые проходит каждое приложение MVC в конвейере обработки запросов.  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- Подробное представление, в котором отображаются подробные сведения о конвейере обработки запросов. Вы можете сравнить представление высокого уровня и подробное представление, чтобы увидеть, как сведения о жизненных циклах собираются на различных этапах. [Загрузите PDF-файл](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) , чтобы увидеть более крупное представление.
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- Размещение и назначение всех переопределяемых методов для объекта [контроллера](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) в конвейере обработки запросов. Вам может потребоваться переопределить какой-либо из методов, но важно понимать их роль в жизненном цикле приложения, чтобы можно было писать код на соответствующем этапе жизненного цикла для желаемого результата.
- Готовые схемы, показывающие, как вызывается каждый из типов фильтров (проверка подлинности, авторизация, действие и результат).
- Ссылка на полезную статью или блог из каждой интересующей точки в подробном представлении.

## <a name="next-steps"></a>Next Steps

Соответствует ли этот документ вашим нуждам? Мы ценим ваши отзывы. Если у вас есть вопрос о жизненном цикле ASP.NET MVC в своем приложении, [StackOverflow](http://stackoverflow.com/help) и [форумы ASP.NET MVC](https://forums.asp.net/1146.aspx) являются отличными местами. [Подпишитесь](https://twitter.com/Cephas_MSFT) на Twitter, чтобы получать обновления в моих последних учебных курсах.
