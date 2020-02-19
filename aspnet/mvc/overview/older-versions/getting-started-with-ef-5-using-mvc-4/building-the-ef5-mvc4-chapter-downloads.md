---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: Создание загружаемых материалов для учебников по EF 5 для MVC 4 | Документация Майкрософт
author: Rick-Anderson
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 10237af40e3914b65e5181f17555697e86adea4b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457860"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a>Создание загружаемых материалов для разделов руководства по EF 5 MVC 4

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012. Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

## <a name="building-the-chapter-downloads"></a>Создание загрузок для глав

1. Скачайте и распакуйте пример ZIP-файла проекта. В распакованном пакете загрузки вы найдете дополнительные ZIP-файлы, по одной для завершения каждой главы.
2. Щелкните правой кнопкой мыши нужный ZIP-файл, выберите пункт **Свойства**и нажмите кнопку **разблокировать** .  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. Распакуйте файл.
4. Дважды щелкните файл *Кукс. sln* , чтобы запустить Visual Studio.
5. В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем — **консоль диспетчера пакетов**.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. В консоли диспетчера пакетов (PMC) нажмите кнопку **восстановить**.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. Закройте Visual Studio.
8. Перезапустите Visual Studio, открыв файл решения, который вы закрыли на предыдущем шаге.
9. В консоли диспетчера пакетов (PMC) введите команду `Update-Database`:  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > Если возникает следующее сообщение об ошибке:  
    >   
    >  *Термин "обновление базы данных" не распознается как имя командлета, функции, файла сценария или исполняемой программы. Проверьте правильность написания имени или, если путь включен, проверьте правильность пути и повторите попытку.*  
    > Закройте и перезапустите Visual Studio.

    При каждом выполнении миграции будет запущен метод SEED. Теперь можно запустить приложение.

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [Назад](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
