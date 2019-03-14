---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: Общие сведения о ASP.NET MVC | Документация Майкрософт
author: microsoft
description: Дополнительные сведения о различиях между приложения ASP.NET MVC и приложений, веб-форм ASP.NET. Узнайте, как решить, когда для создания приложения ASP.NET MVC.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: 61a7841ee238ec365b7d1909221bbe3d834faf84
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025541"
---
<a name="aspnet-mvc-overview"></a>Общие сведения об ASP.NET MVC
====================
по [Microsoft](https://github.com/microsoft)

> Дополнительные сведения о различиях между приложения ASP.NET MVC и приложений, веб-форм ASP.NET. Узнайте, как решить, когда для создания приложения ASP.NET MVC.


Шаблон архитектуры Model-View-Controller (MVC) разделяет приложение на три основных компонента: модель, представление и контроллер. Платформа ASP.NET MVC представляет собой альтернативу шаблону веб-форм ASP.NET MVC веб-приложений. Платформа ASP.NET MVC — это платформа представления легковесной, (как и в случае с приложениями на основе веб-форм) интегрируется с существующими функциями ASP.NET, такие как главные страницы и проверки подлинности на основе членства. Платформа MVC определяется в **System.Web.Mvc** пространства имен и является основной, поддерживаемых частью **System.Web** пространства имен.   
  
MVC — это стандартный шаблон, который многие разработчики знакомы с. Платформа MVC отразится некоторые виды веб-приложений. Другие продолжат использовать традиционной схемы приложения ASP.NET, основанный на веб-формах и обратной передаче. Другие виды веб-приложений будет сочетание двух подходов; одной схемы не исключает другой.   
  
В состав платформы MVC входят следующие компоненты:


[![Вызов действия контроллера, который ожидает, что значение параметра](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**Рис 01**: Вызов действия контроллера, который ожидает, что значение параметра ([Просмотр полноразмерного изображения](asp-net-mvc-overview/_static/image2.png))


- **Модели**. Объекты модели являются частями приложения, реализующими логику для домена данных приложения s. Часто объекты модели извлечения и сохраняют состояние модели в базе данных. Например у объекта продукта может получать сведения из базы данных, работать с ними и затем записывать обновленные данные в таблицу продуктов в SQL Server.

В небольших приложениях эта модель подразумевает концептуальной разделение, а не физическое. Например если приложение только считывает набор данных и отправляет его в представление, приложение не имеет физический слой модели и связанных классов. В этом случае набор данных принимает роль объекта модели.

- **Представления**. Представления служат для отображения пользовательского интерфейса (UI) s приложения. Как правило этот пользовательский Интерфейс создается на основе модели данных. Примером может служить представление для редактирования таблицы Products, которое содержит текстовые поля, раскрывающиеся списки и флажки, на основании текущего состояния объекта продуктов.

- **Контроллеры**. Контроллеры — это компоненты, которые управления взаимодействием с пользователем, работы с моделью и выбора для отображения представления, отображающего пользовательский Интерфейс. В приложении MVC представление служит только для отображения информации. Обработку введенных данных, формирование ответа и взаимодействие с пользователем обеспечивает контроллер. Например контроллер обрабатывает значения строки запроса и передает эти значения в модели, которая в свою очередь запрашивает базу данных с помощью значений.

Шаблон MVC позволяет создавать приложения, различные аспекты приложения (логика ввода, бизнес-логика и логика пользовательского интерфейса), при этом слабые взаимозависимости между этими элементами. Эта схема указывает расположение каждого вида логики в приложении. Логика пользовательского интерфейса относится к представлению. Логика ввода относится к контроллеру. Бизнес-логика размещается в модели. Это разделение позволяет справляться с трудностями при создании приложения, так как он позволяет вам сосредоточиться на один из аспектов реализации за раз. Например можно сосредоточиться на создании представления отдельно в зависимости от бизнес-логики.   
  
В дополнение к упрощению шаблона MVC упрощает для тестирования приложений, а не для тестирования веб-форм ASP.NET веб-приложения. Например в основе веб-форм ASP.NET веб-приложения, один класс используется для отображения выходных данных и реагировать на ввод данных пользователем. Создание автоматических тестов для приложений ASP.NET на основе веб-форм может быть сложным, так как для тестирования отдельной страницы, необходимо создать экземпляр класса page, все его дочерние элементы управления и других зависимых классов приложения. Так как экземпляров так много классов, необходимое для запуска страницы, может быть трудно писать тесты, сосредоточиться исключительно на отдельные части приложения. Тесты для приложений на основе веб-форм ASP.NET, таким образом может быть сложнее тестирования приложения MVC. Кроме того тестов в приложении на базе веб-форм ASP.NET требуется веб-сервера. Платформа MVC разделяет компоненты и активно использует интерфейсы, что позволяет тестировать отдельные элементы вне остальной структуры.   
  
Связь между три основных компонента приложения MVC также облегчает параллельную разработку. К примеру один разработчик может создавать представление, второй разработчик может работать на логике контроллера и третий разработчик может сосредоточиться на бизнес-логику в модели.

## <a name="deciding-when-to-create-an-mvc-application"></a>Когда необходимо создавать приложения MVC

Необходимо внимательно рассмотреть необходимость реализации веб-приложения с помощью платформы ASP.NET MVC или модели веб-форм ASP.NET. Платформа MVC не заменяет модели веб-форм; Обе модели можно использовать для веб-приложений. (При наличии существующих приложений на основе веб-форм, это продолжать работать так же, как они всегда имеют.)   
  
Прежде чем вы решите использовать платформы MVC или модели веб-форм для определенного веб-сайта, взвесить все преимущества каждого подхода.

### <a name="advantages-of-an-mvc-based-web-application"></a>Преимущества MVC веб-приложения

Платформа ASP.NET MVC предоставляет следующие преимущества:

- Он облегчает управление сложными структурами путем разделения приложения на модель, представление и контроллер.
- Он не использует состояние просмотра или серверные формы. Это делает платформу MVC идеальной для разработчиков, которым необходим полный контроль над поведением приложения.
- Она использует схему основного контроллера, который обрабатывает запросы веб-приложений через один контроллер. Это позволяет создать приложение, которое поддерживает расширенную инфраструктуру маршрутизации. Дополнительные сведения см. в разделе [интерфейсного контроллера](https://go.microsoft.com/fwlink/?LinkId=106357 "интерфейсного контроллера") на сайте MSDN.
- Он обеспечивает лучшую поддержку для разработки приложений на основе тестирования (TDD).
- Он хорошо подходит для веб-приложений, поддерживаемых крупными коллективами разработчиков и дизайнеров, которым требуется высокая степень контроля над поведением приложения.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Преимущества веб-приложения на веб-форм

Платформа на основе веб-форм имеет следующие преимущества:

- Она поддерживает модель событий, которая сохраняет состояние по протоколу HTTP, что выгодно для разработки бизнес-веб-приложений. Приложения на основе веб-форм предоставляет множество событий, которые поддерживаются в сотни серверных элементов управления.
- Она использует шаблон контроллера страницы, добавляющий функции к отдельным страницам. Дополнительные сведения см. в разделе [контроллера страницы](https://go.microsoft.com/fwlink/?LinkId=106359 "контроллера страницы") на веб-сайте MSDN.
- Она использует состояние представления или формы на основе сервера, которые может облегчить управление информацией о состоянии.
- Он хорошо подходит для небольших коллективов веб-разработчиков, желающих воспользоваться преимуществами большое число компонентов, доступных для быстрой разработки приложений.
- Как правило, менее сложна для разработки приложений, так как компоненты ( **страницы** класса элементов управления и т. д.) тесно интегрированы и требуют меньшего объема кода, чем в модели MVC.

## <a name="features-of-the-aspnet-mvc-framework"></a>Компоненты платформы ASP.NET MVC

Платформа ASP.NET MVC предоставляет следующие возможности:

- Разделение задач приложения (логика ввода, бизнес-логика и логика пользовательского интерфейса), пригодности для тестирования и разработка с тестированием (TDD) по умолчанию. Все основные контракты платформы MVC основаны на интерфейсе и может быть проверен с помощью макетов объекта, которые имитируют поведение реальных объектов приложения. Можно модульном тестировании приложения без необходимости запуска контроллеров в процессе ASP.NET, что делает модульное тестирование быстрой и гибкой. Можно использовать любую платформу модульного тестирования, совместимой с .NET Framework.
- Расширяемая и дополняемая платформа. Компоненты платформы ASP.NET MVC framework разработаны таким образом, чтобы легко заменить или настроить. Вы можете подключить собственный механизм представлений, политику маршрутизации URL-адрес, сериализацию параметров методов действий и другие компоненты. Платформа ASP.NET MVC также поддерживает использование моделей контейнера внедрения зависимостей (DI) и инверсии управления (IOC). Внедрение Зависимостей позволяет внедрять объекты в класс, не полагаясь на создаваемый класс сам объект. IOC указывает, что если один объект требует другой объект, первые объекты должны получить второй объект из внешнего источника, например файл конфигурации. Это облегчает тестирование.
- Мощный компонент сопоставления URL-, который позволяет создавать приложения с понятными и поддерживающими поиск URL-адресами. URL-адреса нет необходимости включать расширения имен файлов и предназначены для поддержки шаблонов именования URL-адреса, которые работают для поиска модуля оптимизации (систем SEO) и передачи репрезентативного состояния (REST) адресации.
- Поддержка использования разметки в существующую страницу ASP.NET (ASPX-файлы), пользовательский элемент управления (ASCX) и файлы разметки главной страницы (master-файлы) как шаблонов представлений. Можно использовать существующие функции ASP.NET с помощью платформы ASP.NET MVC, например вложенные главные страницы, встроенные выражения (&lt;% = %&gt;), декларативные серверные элементы управления, шаблоны, привязки данных, локализацию и т. д.
- Поддержка существующих функций ASP.NET. ASP.NET MVC позволяет использовать функции, такие как проверку подлинности форм и проверки подлинности Windows, авторизация URL-адреса, членства и ролей, выходных данных и кэширование данных, управление состоянием сеанса и профиля, наблюдение за работоспособностью, система конфигурации и поставщик архитектура.