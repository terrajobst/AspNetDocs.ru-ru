---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
title: 'Итерация #4 — сделайте приложение слабо связанным (C#) | Документация Майкрософт'
author: microsoft
description: В этой четвертой итерации мы используем преимущества нескольких шаблонов проектирования программного обеспечения, чтобы упростить обслуживание и изменение приложения Contact Manager. Для ...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 829f589f-e201-4f6e-9ae6-08ae84322065
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
msc.type: authoredcontent
ms.openlocfilehash: ce8e3c4ff8a59be9f2f572813db599604216119d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437976"
---
# <a name="iteration-4--make-the-application-loosely-coupled-c"></a>Итерация #4 — сделайте приложение слабо связанным (C#)

по [Майкрософт](https://github.com/microsoft)

[Скачать код](iteration-4-make-the-application-loosely-coupled-cs/_static/contactmanager_4_cs1.zip)

> В этой четвертой итерации мы используем преимущества нескольких шаблонов проектирования программного обеспечения, чтобы упростить обслуживание и изменение приложения Contact Manager. Например, мы выполним рефакторинг нашего приложения для использования шаблона репозитория и шаблона внедрения зависимостей.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Создание приложения для управления контактами ASP.NET MVCC#()

В этой серии учебников мы создадим все приложение управления контактами от начала до конца. Приложение диспетчера контактов позволяет хранить контактные данные, имена телефонов и адреса электронной почты. список людей.

Мы создаем приложение для нескольких итераций. При каждой итерации мы постепенно улучшаем приложение. Цель этого нескольких итераций — позволить вам понять причину каждого изменения.

- Итерация #1 — Создайте приложение. В первой итерации мы создаем Диспетчер контактов проще всего. Добавлена поддержка основных операций с базой данных: создание, чтение, обновление и удаление (CRUD).

- Итерация #2 — сделайте приложение привлекательным. В этой итерации мы улучшаем внешний вид приложения путем изменения главной страницы ASP.NET представления MVC по умолчанию и каскадной таблицы стилей.

- Итерация #3 — Добавление проверки формы. В третьей итерации мы добавим проверку базовой формы. Мы запрещаем пользователям отправлять форму, не заполняя обязательные поля формы. Мы также проверяем адреса электронной почты и номера телефонов.

- Итерация #4 — сделайте приложение слабо связанным. В этой четвертой итерации мы используем преимущества нескольких шаблонов проектирования программного обеспечения, чтобы упростить обслуживание и изменение приложения Contact Manager. Например, мы выполним рефакторинг нашего приложения для использования шаблона репозитория и шаблона внедрения зависимостей.

- Итерация #5 — Создание модульных тестов. В пятой итерации мы сделаем наше приложение проще в обслуживании и изменении, добавляя модульные тесты. Мы размакетирования наши классы модели данных и создаем модульные тесты для наших контроллеров и логики проверки.

- Итерация #6 — Используйте разработку на основе тестирования. В этой шестой итерации мы добавим новые функции в наше приложение, создав модульные тесты в первую очередь и записав код в модульные тесты. В этой итерации мы добавляем группы контактов.

- Итерация #7 — Добавление функциональности AJAX. В седьмой итерации мы улучшаем скорость реагирования и производительность нашего приложения, добавив поддержку AJAX.

## <a name="this-iteration"></a>Эта итерация

В этой четвертой итерации приложения диспетчера контактов мы выполним рефакторинг приложения, чтобы сделать приложение более слабо связанным. Если приложение слабо связано, можно изменить код в одной части приложения, не требуя изменения кода в других частях приложения. Слабо связанные приложения являются более устойчивыми к изменениям.

В настоящее время вся логика доступа к данным и проверки, используемая приложением диспетчера контактов, содержится в классах контроллера. Это плохо идея. Каждый раз, когда необходимо изменить одну часть приложения, вы рискуете разбить ошибки на другую часть приложения. Например, при изменении логики проверки вы рискуете добавить новые ошибки в логику доступа к данным или контроллера.

> [!NOTE] 
> 
> (SRP) класс не должен иметь более одной причины для изменения. Сочетание контроллера, проверки и логики базы данных является огромным нарушением принципа единой ответственности.

Существует несколько причин, по которым может потребоваться изменить приложение. Может потребоваться добавить в приложение новую функцию, возможно, потребуется исправить ошибку в приложении или изменить способ реализации компонента приложения в службах. Приложения редко являются статическими. Они обычно увеличиваются и изменяются со временем.

Предположим, например, что вы решили изменить способ реализации уровня доступа к данным. Сейчас приложение диспетчера контактов использует Microsoft Entity Framework для доступа к базе данных. Однако вы можете перейти на новую или альтернативную технологию доступа к данным, например ADO.NET Data Services или NHibernate. Однако поскольку код доступа к данным не изолирован от кода проверки и контроллера, невозможно изменить код доступа к данным в приложении без изменения другого кода, который напрямую не связан с доступом к данным.

С другой стороны, если приложение слабо связано, вы можете вносить изменения в одну часть приложения, не затрагивая другие части приложения. Например, можно переключать технологии доступа к данным, не изменяя логику проверки или контроллера.

В этой итерации мы воспользуемся несколькими шаблонами разработки программного обеспечения, которые позволяют оптимизировать приложение диспетчера контактов в более слабо связанном приложении. Когда все будет готово, Диспетчер контактов выиграл t ничего не сделал. Однако в будущем мы сможем быстро изменить приложение.

> [!NOTE] 
> 
> Рефакторинг — это процесс перезаписи приложения таким образом, что он не теряет существующих функциональных возможностей.

## <a name="using-the-repository-software-design-pattern"></a>Использование шаблона проектирования программного обеспечения репозитория

Первое изменение заключается в том, чтобы воспользоваться преимуществами шаблона разработки программного обеспечения, который называется шаблоном репозитория. Мы будем использовать шаблон репозитория, чтобы изолировать наш код доступа к данным от остальной части нашего приложения.

Для реализации шаблона репозитория необходимо выполнить следующие два действия:

1. Выбор интерфейса
2. Создание конкретного класса, реализующего интерфейс

Сначала необходимо создать интерфейс, который описывает все методы доступа к данным, которые необходимо выполнить. Интерфейс Иконтактманажеррепоситори содержится в листинге 1. Этот интерфейс описывает пять методов: Креатеконтакт (), DeleteContact (), Едитконтакт (), Contact и Листконтактс ().

**Листинг 1. Моделс\иконтактманажеррепоситори.КС**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample1.cs)]

Далее необходимо создать конкретный класс, реализующий интерфейс Иконтактманажеррепоситори. Так как мы используем Microsoft Entity Framework для доступа к базе данных, мы создадим новый класс с именем Ентитиконтактманажеррепоситори. Этот класс содержится в листинге 2.

**Листинг 2. Моделс\ентитиконтактманажеррепоситори.КС**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample2.cs)]

Обратите внимание, что класс Ентитиконтактманажеррепоситори реализует интерфейс Иконтактманажеррепоситори. Класс реализует все пять методов, описываемых этим интерфейсом.

Может возникнуть вопрос, почему нам нужно попытаться получить интерфейс. Зачем нужно создавать интерфейс и класс, реализующий его?

За одним исключением, оставшаяся часть нашего приложения будет взаимодействовать с интерфейсом, а не конкретным классом. Вместо вызова методов, предоставляемых классом Ентитиконтактманажеррепоситори, мы будем вызывать методы, предоставляемые интерфейсом Иконтактманажеррепоситори.

Таким образом, мы можем реализовать интерфейс с новым классом без изменения оставшейся части нашего приложения. Например, в будущем может потребоваться реализовать класс Датасервицесконтактманажеррепоситори, реализующий интерфейс Иконтактманажеррепоситори. Класс Датасервицесконтактманажеррепоситори может использовать службы данных ADO.NET для доступа к базе данных вместо Microsoft Entity Framework.

Если наш код приложения запрограммирован на интерфейс Иконтактманажеррепоситори, а не на конкретный класс Ентитиконтактманажеррепоситори, мы можем переключать конкретные классы, не изменяя никакой оставшейся части нашего кода. Например, можно переключиться с класса Ентитиконтактманажеррепоситори на класс Датасервицесконтактманажеррепоситори, не изменяя логику доступа к данным или проверки.

Программирование для интерфейсов (абстракций) вместо конкретных классов делает приложение более устойчивым для изменения.

> [!NOTE] 
> 
> Вы можете быстро создать интерфейс из конкретного класса в Visual Studio, выбрав пункт меню Рефакторинг, извлечь интерфейс. Например, можно сначала создать класс Ентитиконтактманажеррепоситори, а затем использовать извлечение интерфейса для автоматического создания интерфейса Иконтактманажеррепоситори.

## <a name="using-the-dependency-injection-software-design-pattern"></a>Использование шаблона разработки по для внедрения зависимостей

Теперь, когда мы перенесли код доступа к данным в отдельный класс репозитория, нам нужно изменить наш контроллер связи, чтобы использовать этот класс. Мы будем использовать шаблон разработки программного обеспечения, именуемый внедрением зависимостей, для использования класса репозитория в нашем контроллере.

Измененный контактный контроллер содержится в листинге 3.

**Листинг 3. Контроллерс\контактконтроллер.КС**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample3.cs)]

Обратите внимание, что контактный контроллер в листинге 3 имеет два конструктора. Первый конструктор передает конкретный экземпляр интерфейса Иконтактманажеррепоситори второму конструктору. Класс Contact Controller использует *внедрение зависимостей конструктора*.

В первом конструкторе используется только один класс Ентитиконтактманажеррепоситори. Оставшаяся часть класса использует интерфейс Иконтактманажеррепоситори, а не конкретный класс Ентитиконтактманажеррепоситори.

Это позволяет легко переключать реализации класса Иконтактманажеррепоситори в будущем. Если вы хотите использовать класс Датасервицесконтактрепоситори вместо класса Ентитиконтактманажеррепоситори, просто измените первый конструктор.

Внедрение зависимостей конструктора также делает класс контроллера контакта очень тестируемым. В модульных тестах можно создать экземпляр контроллера связи путем передачи макета реализации класса Иконтактманажеррепоситори. Эта функция внедрения зависимостей будет очень важна для нас в следующей итерации при построении модульных тестов для приложения диспетчера контактов.

> [!NOTE] 
> 
> Если вы хотите полностью отделить класс контроллера контакта от конкретной реализации интерфейса Иконтактманажеррепоситори, можно воспользоваться преимуществами платформы, поддерживающей внедрение зависимостей, например StructureMap или Microsoft Entity Framework (MEF). Используя преимущества инфраструктуры внедрения зависимостей, вам не нужно ссылаться на конкретный класс в коде.

## <a name="creating-a-service-layer"></a>Создание слоя служб

Возможно, вы заметили, что наша логика проверки по-прежнему отличается от логики контроллера в измененном классе контроллера в листинге 3. По той же причине рекомендуется изолировать логику доступа к данным, но рекомендуется изолировать нашу логику проверки.

Чтобы устранить эту проблему, можно создать отдельный [*слой служб*](http://martinfowler.com/eaaCatalog/serviceLayer.html). Слой служб — это отдельный слой, который можно вставить между нашими классами контроллера и репозитория. Уровень служб содержит бизнес-логику, включая всю логику проверки.

Контактманажерсервице содержится в листинге 4. Он содержит логику проверки из класса Contact Controller.

**Листинг 4. Моделс\контактманажерсервице.КС**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample4.cs)]

Обратите внимание, что конструктору для Контактманажерсервице требуется Валидатиондиктионари. Уровень служб взаимодействует с уровнем контроллера через этот Валидатиондиктионари. Мы подробно рассмотрим Валидатиондиктионари в следующем разделе, когда мы обсудим шаблон декоратора.

Кроме того, обратите внимание, что Контактманажерсервице реализует интерфейс Иконтактманажерсервице. Всегда следует пристараться программировать к интерфейсам, а не к конкретным классам. Другие классы в приложении диспетчера контактов не взаимодействуют с классом Контактманажерсервице напрямую. Вместо этого за одним исключением оставшаяся часть приложения диспетчера контактов запрограммирована с помощью интерфейса Иконтактманажерсервице.

Интерфейс Иконтактманажерсервице содержится в листинге 5.

**Листинг 5. Моделс\иконтактманажерсервице.КС**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample5.cs)]

Измененный класс контактного контроллера содержится в листинге 6. Обратите внимание, что контактный контроллер больше не взаимодействует с репозиторием ContactManager. Вместо этого контактный контроллер взаимодействует со службой ContactManager. Каждый уровень изолирован от других слоев, насколько это возможно.

**Листинг 6. Контроллерс\контактконтроллер.КС**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample6.cs)]

Наше приложение больше не работает афаул принципа единой ответственности (SRP). Контактный контроллер в листинге 6 был удален из каждой ответственности, кроме управления потоком выполнения приложения. Вся логика проверки была удалена из контроллера контакта и отправлена на слой служб. Вся логика базы данных была отправлена на слой репозитория.

## <a name="using-the-decorator-pattern"></a>Использование шаблона декоратора

Мы хотим иметь возможность полностью отделить уровень служб от нашего уровня контроллера. В принципе, мы должны уметь компилировать наш уровень служб в отдельной сборке на уровне контроллера, не требуя добавлять ссылку на наше приложение MVC.

Однако уровень служб должен иметь возможность передавать сообщения об ошибках проверки обратно на уровень контроллера. Как можно включить уровень службы для обмена сообщениями об ошибках проверки, не связывая контроллер и слой служб? Мы можем воспользоваться преимуществами шаблона разработки программного обеспечения, именуемого [шаблоном декоратора](http://en.wikipedia.org/wiki/Decorator_pattern).

Контроллер использует ModelStateDictionary с именем ModelState для представления ошибок проверки. Таким образом, может показаться, что вы можете передать ModelState из уровня контроллера в слой служб. Однако использование ModelState на уровне служб сделает уровень служб зависимым от функции платформы ASP.NET MVC. Это было бы неплохим, так как, когда-нибудь, может потребоваться использовать слой служб с приложением WPF вместо приложения ASP.NET MVC. В этом случае вам не нужно ссылаться на платформу ASP.NET MVC для использования класса ModelStateDictionary.

Шаблон декоратора позволяет создать оболочку для существующего класса в новом классе, чтобы реализовать интерфейс. Наш проект диспетчера контактов включает класс Моделстатевраппер, содержащийся в листинге 7. Класс Моделстатевраппер реализует интерфейс в листинге 8.

**Листинг 7 — Моделс\валидатион\моделстатевраппер.КС**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample7.cs)]

**Листинг 8. Моделс\валидатион\ивалидатиондиктионари.КС**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample8.cs)]

Если взглянуть на листинг 5, вы увидите, что слой служб ContactManager использует исключительно интерфейс Ивалидатиондиктионари. Служба ContactManager не зависит от класса ModelStateDictionary. Когда контактный контроллер создает службу ContactManager, контроллер переносит его ModelState следующим образом:

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample9.cs)]

## <a name="summary"></a>Сводка

В этой итерации мы не добавили новые функции в приложение диспетчера контактов. Цель этой итерации — выполнить рефакторинг приложения диспетчера контактов, чтобы упростить обслуживание и изменение.

Сначала мы реализовали шаблон проектирования программного обеспечения репозитория. Мы перенесли весь код доступа к данным в отдельный класс репозитория ContactManager.

Мы также изолируем логику проверки на основе логики контроллера. Мы создали отдельный слой служб, который содержит весь код проверки. Уровень контроллера взаимодействует с уровнем служб, а уровень служб взаимодействует с уровнем репозитория.

Когда мы создали слой служб, мы использовали преимущества шаблона декоратора, чтобы изолировать ModelState от нашего уровня служб. На нашем уровне служб мы запрограммированы на интерфейс Ивалидатиондиктионари, а не на ModelState.

Наконец, мы использовали шаблон разработки программного обеспечения, именуемый шаблоном внедрения зависимостей. Этот шаблон позволяет программировать по интерфейсам (абстракциям) вместо конкретных классов. Реализация шаблона разработки внедрения зависимостей также делает наш код более тестируемым. В следующей итерации мы добавляем модульные тесты в наш проект.

> [!div class="step-by-step"]
> [Назад](iteration-3-add-form-validation-cs.md)
> [Вперед](iteration-5-create-unit-tests-cs.md)
