---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: Модульное тестирование приложений SignalR | Документация Майкрософт
author: bradygaster
description: В этой статье описывается, как использовать функции модульного тестирования SignalR 2,0.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467304"
---
# <a name="unit-testing-signalr-applications"></a>Модульное тестирование приложений SignalR

по [Патрик Флетчера](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этой статье описывается использование функций модульного тестирования SignalR 2.
>
> ## <a name="software-versions-used-in-this-topic"></a>Версии программного обеспечения, используемые в этом разделе
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR версии 2
>
>
>
> ## <a name="questions-and-comments"></a>Вопросы и комментарии
>
> Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы. Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a>Модульное тестирование приложений SignalR

Вы можете использовать функции модульных тестов в SignalR 2 для создания модульных тестов для приложения SignalR. SignalR 2 включает интерфейс [ихубкаллерконнектионконтекст](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) , который можно использовать для создания макета объекта для имитации методов концентратора для тестирования.

В этом разделе вы добавите модульные тесты для приложения, созданного в [Начало работы руководстве](../getting-started/tutorial-getting-started-with-signalr.md) , с помощью [xUnit.NET](https://github.com/xunit/xunit) и [MOQ](https://github.com/Moq/moq4).

XUnit.net будет использоваться для управления тестом; MOQ будет использоваться для создания [макета](http://en.wikipedia.org/wiki/Mock_object) объекта для тестирования. При необходимости можно использовать и другие платформы макетирования. [Нсубституте](http://nsubstitute.github.io/) также является хорошим выбором. В этом руководстве показано, как настроить макет объекта двумя способами: во-первых, с помощью объекта `dynamic` (представленного в .NET Framework 4) и секунд с помощью интерфейса.

### <a name="contents"></a>Содержимое

Этот учебник содержит следующие разделы.

- [Модульное тестирование с динамическим](#dynamic)
- [Модульное тестирование по типу](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a>Модульное тестирование с динамическим

В этом разделе вы добавите модульный тест для приложения, созданного в [Начало работы руководстве](../getting-started/tutorial-getting-started-with-signalr.md) , с помощью динамического объекта.

1. Установите [расширение xUnit Runner](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) для Visual Studio 2013.
2. Либо завершите работу с [руководством начало работы](../getting-started/tutorial-getting-started-with-signalr.md), либо Скачайте готовое приложение из [коллекции кода MSDN](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).
3. Если вы используете скачанную версию приложения начало работы, откройте **консоль диспетчера пакетов** и нажмите кнопку **восстановить** , чтобы добавить в проект пакет SignalR.

    ![Восстановление пакетов](unit-testing-signalr-applications/_static/image1.png)
4. Добавьте проект в решение для модульного теста. Щелкните решение правой кнопкой мыши в **Обозреватель решений** и выберите **Добавить**, **создать проект...** . В **C#** узле выберите узел **Windows** . Выберите **Библиотека классов**. Назовите новый проект **TestLibrary** и нажмите кнопку **ОК**.

    ![Создание тестовой библиотеки](unit-testing-signalr-applications/_static/image2.png)
5. Добавьте ссылку в проект библиотеки тестов в проект Сигналрчат. Щелкните правой кнопкой мыши проект **TestLibrary** и выберите **Добавить**, **ссылка...** . Выберите узел **проекты** в узле **решение** и проверьте **сигналрчат**. Нажмите кнопку **ОК**.

    ![Добавить ссылку на проект](unit-testing-signalr-applications/_static/image3.png)
6. Добавьте пакеты SignalR, MOQ и XUnit в проект **TestLibrary** . В **консоли диспетчера пакетов**задайте для раскрывающегося списка **проект по умолчанию** значение **TestLibrary**. В окне консоли выполните следующие команды:

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![Установка пакетов](unit-testing-signalr-applications/_static/image4.png)
7. Создайте файл теста. Щелкните правой кнопкой мыши проект **TestLibrary** и выберите пункт **Добавить...** , **класс**. Назовите новый класс **Tests.CS**.
8. Замените содержимое Tests.cs следующим кодом.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    В приведенном выше коде тестовый клиент создается с помощью объекта `Mock` из библиотеки [MOQ](https://github.com/Moq/moq4) типа [Ихубкаллерконнектионконтекст](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (в SignalR 2,1 назначьте `dynamic` для параметра типа.) Интерфейс `IHubCallerConnectionContext` — это прокси-объект, с помощью которого вызываются методы на клиенте. Затем функция `broadcastMessage` определяется для макета клиента, чтобы его можно было вызывать с помощью класса `ChatHub`. Затем обработчик тестов вызывает метод `Send` класса `ChatHub`, который, в свою очередь, вызывает функцию макетирования `broadcastMessage`.
9. Постройте решение, нажав клавишу **F6**.
10. Выполните модульный тест. В Visual Studio выберите **тест**, **Windows**, **Обозреватель тестов**. В окне обозревателя тестов щелкните правой кнопкой мыши **хубсаремоккаблевиадинамик** и выберите команду **Выполнить выбранные тесты**.

    ![Обозреватель тестов](unit-testing-signalr-applications/_static/image5.png)
11. Убедитесь, что тест пройден, проверив нижнюю панель в окне обозревателя тестов. В окне будет показано, что тест пройден.

    ![Тест пройден](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a>Модульное тестирование по типу

В этом разделе вы добавите тест для приложения, созданного в [Начало работы руководстве](../getting-started/tutorial-getting-started-with-signalr.md) , используя интерфейс, содержащий тестируемый метод.

1. Выполните шаги 1-7 в разделе [модульное тестирование с помощью динамического](#dynamic) учебника выше.
2. Замените содержимое Tests.cs следующим кодом.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    В приведенном выше коде создается интерфейс, определяющий сигнатуру метода `broadcastMessage`, для которого тестовый модуль будет создавать макет клиента. Затем макет клиента создается с помощью объекта `Mock` типа [ихубкаллерконнектионконтекст](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (в SignalR 2,1, назначьте `dynamic` для параметра типа.) Интерфейс `IHubCallerConnectionContext` — это прокси-объект, с помощью которого вызываются методы на клиенте.

    Затем тест создает экземпляр `ChatHub`, а затем создает макет версии метода `broadcastMessage`, который, в свою очередь, вызывается путем вызова метода `Send` в концентраторе.
3. Постройте решение, нажав клавишу **F6**.
4. Выполните модульный тест. В Visual Studio выберите **тест**, **Windows**, **Обозреватель тестов**. В окне обозревателя тестов щелкните правой кнопкой мыши **хубсаремоккаблевиадинамик** и выберите команду **Выполнить выбранные тесты**.

    ![Обозреватель тестов](unit-testing-signalr-applications/_static/image7.png)
5. Убедитесь, что тест пройден, проверив нижнюю панель в окне обозревателя тестов. В окне будет показано, что тест пройден.

    ![Тест пройден](unit-testing-signalr-applications/_static/image8.png)
