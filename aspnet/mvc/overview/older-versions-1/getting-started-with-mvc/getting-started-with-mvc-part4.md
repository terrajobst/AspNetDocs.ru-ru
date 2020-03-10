---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: Создание базы данных | Документация Майкрософт
author: shanselman
description: Это руководство для начинающих, в котором представлены основы ASP.NET MVC. Создание простого веб-приложения, считывающего и записывающего данные из базы данных.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469674"
---
# <a name="creating-a-database"></a>Создание базы данных

по [Скотт Hanselman](https://github.com/shanselman)

> Это руководство для начинающих, в котором представлены основы ASP.NET MVC. Вы создадите простое веб-приложение, считывающее и записывающее данные из базы данных. Посетите [центр обучения ASP.NET MVC](../../../index.md) , чтобы найти другие руководства и примеры для ASP.NET MVC.

В этом разделе мы создадим новую базу данных SQL Express, которая будет использоваться для хранения и извлечения данных фильмов. В интегрированной среде разработки Visual Web Developer выберите вид | обозреватель сервера. Щелкните правой кнопкой мыши подключения к данным и выберите Добавить подключение...

![аддконнектион](getting-started-with-mvc-part4/_static/image1.png)

В диалоговом окне Выбор источника данных выберите Microsoft SQL Server и нажмите кнопку продолжить.

![](getting-started-with-mvc-part4/_static/image2.png)

В диалоговом окне Добавление соединения введите ".\SQLEXPRESS" в качестве имени сервера и введите "Movies" в качестве имени новой базы данных.

[диалоговое окно добавления соединения ![](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)

Нажмите кнопку ОК, и вам будет предложено создать эту базу данных. Выберите Да.

[![создавать фильмы?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)

Теперь у вас есть пустая база данных в обозреватель сервера.

![Добавить новую таблицу](getting-started-with-mvc-part4/_static/image7.png)

Щелкните правой кнопкой мыши таблицы и выберите команду Добавить таблицу. Появится конструктор таблиц. Добавьте столбцы для ID, Title, ReleaseDate, жанра и цены. Щелкните правой кнопкой мыши столбец идентификатор и выберите пункт Задать первичный ключ. Вот как выглядят мои области разработки.

[Редактор таблиц базы данных ![](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)

Кроме того, выберите столбец идентификатор и в разделе Свойства столбца ниже измените "Спецификация идентификатора" на "Да".

[![свойства столбца Identity](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)

Когда все будет готово, щелкните значок сохранить на панели инструментов или выберите файл | В меню выберите команду Сохранить и присвойте таблице имя**Movie**(единственное значение). У нас есть база данных и таблица!

[![выберите имя](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)

Вернитесь к обозреватель сервера и щелкните правой кнопкой мыши таблицу фильмов, а затем выберите команду "отобразить данные таблицы". Введите несколько фильмов, чтобы в базе данных были данные.

[Изменение таблицы базы данных ![](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)

## <a name="creating-a-model"></a>Создание модели

Теперь вернитесь к обозреватель решений в правой части интегрированной среды разработки и щелкните правой кнопкой мыши папку Models и выберите Добавить | Новый элемент.

[![аддневмоделитем](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)

Мы создадим модель сущностей из нашей новой базы данных. Это приведет к добавлению в наш проект набора классов, который упрощает для нас запрос и обработку данных в базе данных. Выберите узел данных в левой части диалогового окна, а затем выберите шаблон элемента ADO.NET EDM. Назовите его movies. edmx.

[![Аддневдатамодел](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)

Нажмите кнопку "Добавить". После этого будет запущен мастер EDM.

В появившемся диалоговом окне выберите Создать из базы данных. Так как мы только что сделали базу данных, нам нужно только сообщить Entity Framework о нашей новой базе данных и ее таблице. Нажмите кнопку Далее, чтобы сохранить подключение к базе данных в конфигурации веб-приложения. Теперь установите флажок таблицы и фильм и нажмите кнопку Готово.

[Мастер EDM ![](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)

Теперь мы можем увидеть нашу новую таблицу фильмов в Entity Framework Designer и получить к ней доступ из кода.

[![фильмов — Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)

В области конструктора можно увидеть класс "Movie". Этот класс сопоставляется с таблицей "Movie" в нашей базе данных, и каждое свойство в нем сопоставляется со столбцом с таблицей. Каждый экземпляр класса "Movie" будет соответствовать строке в таблице "Movie".

Если вам не нравятся соглашения об именовании и сопоставлении по умолчанию, используемые Entity Framework, можно использовать конструктор Entity Framework для их изменения или настройки. Для этого приложения мы будем использовать значения по умолчанию и просто сохраняем файл как есть.

Теперь давайте выполним работу с некоторыми реальными данными!

> [!div class="step-by-step"]
> [Назад](getting-started-with-mvc-part3.md)
> [Вперед](getting-started-with-mvc-part5.md)
