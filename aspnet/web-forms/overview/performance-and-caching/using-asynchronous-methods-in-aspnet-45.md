---
uid: web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
title: Использование асинхронных методов в ASP.NET 4.5 | Документация Майкрософт
author: Rick-Anderson
description: Этом учебнике описываются основы создания асинхронных приложений веб-форм ASP.NET с помощью Visual Studio Express 2012 для Web, где — это бесплатный...
ms.author: riande
ms.date: 01/02/2019
ms.assetid: a585c9a2-7c8e-478b-9706-90f3739c50d1
msc.legacyurl: /web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: c36749f82051ee8965035eca9c2e4e57a5dbd616
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028291"
---
<a name="using-asynchronous-methods-in-aspnet-45"></a>Использование асинхронных методов в ASP.NET 4.5
====================
по [Рик Андерсон]((https://twitter.com/RickAndMSFT))

> Этот учебник поможет основы создания асинхронных приложений веб-форм ASP.NET с использованием [Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/11), который является бесплатной версии Microsoft Visual Studio. Можно также использовать [Visual Studio 2012](https://www.microsoft.com/visualstudio/11). В этом учебнике включены следующие разделы.
> 
> - [Порядок обработки запросов пулом потоков](#HowRequestsProcessedByTP)
> - [Выбор синхронные или асинхронные методы](#ChoosingSyncVasync)
> - [Пример приложения](#SampleApp)
> - [На странице синхронной элементы](#GizmosSynch)
> - [Создание асинхронных элементы страницы](#CreatingAsynchGizmos)
> - [Параллельное выполнение нескольких операций](#Parallel)
> - [Использование токена отмены](#CancelToken)
> - [Конфигурация сервера для вызовов веб-службы высокого уровня параллелизма и высокий уровень задержки](#ServerConfig)
> 
> Полный пример предоставляется для выполнения инструкций этого руководства  
>  [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/) на [GitHub](https://github.com/) сайта.


ASP.NET 4.5 веб-страницы в сочетании [.NET 4.5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx) позволяет зарегистрировать асинхронные методы, которые возвращают объект типа [задачи](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx). .NET Framework 4 появилась асинхронного программирования концепция, называемая [задачи](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) и ASP.NET 4.5 поддерживает [задачи](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx). Задачи представляются **задачи** типа и связанных типов в [System.Threading.Tasks](https://msdn.microsoft.com/library/system.threading.tasks.aspx) пространства имен. .NET Framework 4.5 основан на этой асинхронной поддержки за счет [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) и [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) ключевые слова, которые делают работу с [задачи](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) гораздо проще, чем предыдущие объектов асинхронные подходы. [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ключевое слово является синтаксическое сокращение, которое указывает, которого фрагмент кода асинхронно ожидает на другие части кода. [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) ключевое слово представляет подсказку, которая позволяет пометить методы как асинхронные методы на основе задач. Сочетание **await**, **async**и **задачи** объекта значительно упрощает написание асинхронного кода в .NET 4.5. Новая модель для асинхронных методов называется *асинхронную модель на основе задач* (**КОСНИТЕСЬ**). Предполагается, что у вас есть некоторый опыт работы с асинхронного программирования при помощи [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) и [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) ключевые слова и [задачи](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) пространства имен.

Дополнительные сведения об использовании [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) и [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) ключевые слова и [задачи](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) пространства имен, см. в следующих ресурсах.

- [Технический документ. Асинхронность в .NET](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Часто задаваемые вопросы о Async/Await](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Асинхронное программирование в Visual Studio](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>  Порядок обработки запросов пулом потоков

На веб-сервере в .NET Framework поддерживается пул потоков, которые используются для обслуживания запросов ASP.NET. Когда запрос прибывает, поток из пула отправляется для обработки этого запроса. Если запрос обрабатывается синхронно, поток, который обрабатывает запрос является занятости во время запрос обрабатывается, и что поток не может обслуживать другой запрос.   
  
Это может оказаться проблемой, так как пул потоков можно сделать достаточно велик для хранения множества занятых потоков. Однако количество потоков в пуле потоков ограничено (максимум для .NET 4.5 по умолчанию — 5000). В больших приложениях с высокой степенью параллелизма длительных запросов может препятствовать все доступные потоки. Это состояние называется нехватка потоков. При наступлении такой ситуации веб-сервер помещает запросы в очередь. При переполнении очереди запросов веб-сервер отклоняет запросы с состоянием HTTP 503 (сервер перегружен). Пул потоков CLR имеет ограничения на новый поток вставки. Если параллелизм множественными (то есть веб-сайт может неожиданно получить большое количество запросов) и все доступные потоки запросов заняты из-за вызовов серверной части с высокой задержкой, скорость внедрения ограниченной потока могут сделать очень плохо отвечать приложение. Кроме того каждый новый поток, добавляемые в пул потоков имеет издержки (например, 1 МБ памяти). Веб-приложения с помощью синхронных методов вызовы между службами высокой задержкой, где пул потоков возрастает до .NET 4.5 по умолчанию более 5, 000 потоков займут около 5 ГБ больше памяти, чем приложение с такой же запросов на обслуживание с помощью асинхронные методы и 50 потоков. При выполнении асинхронной работы, не всегда используется поток. Например, при выполнении запроса асинхронной веб-службы ASP.NET не будет использовать все потоки между **async** вызова метода и **await**. Используя пул потоков для обслуживания запросов с высокой задержкой может привести к большой объем памяти и неэффективного использования серверного оборудования.

## <a name="processing-asynchronous-requests"></a>Обработка асинхронных запросов

В веб-приложений, см. в разделе большое количество одновременных запросов при запуске или имеет множественными нагрузки (где степень параллелизма можно повысить внезапно) делая асинхронных вызовов веб-службы увеличит скорость реагирования приложения. Асинхронный запрос обрабатывается тем же количество времени для обработки как синхронный запрос. Например если запрос выполняет вызов веб-службы требует две секунды, принимает запрос на две секунды ли она выполняется синхронно или асинхронно. Однако при асинхронном вызове, поток не заблокирован отвечать на другие запросы во время ожидания выполнения первого запроса. Поэтому асинхронные запросы предупреждают роста пула очереди и поток запроса при наличии множества параллельных запросов, которые вызывают длительные операции.

## <a id="ChoosingSyncVasync"></a>  Выбор синхронные или асинхронные методы

В этом разделе перечислены рекомендации, когда использовать синхронные или асинхронные методы. Это только рекомендации; Проверьте каждое приложение, чтобы определить, является ли асинхронные методы повышения производительности.

В общем случае используйте синхронные методы для следующих условий:

- Операции являются простыми или коротким циклом выполнения.
- Простота является более важным, чем эффективность.
- Операции основном являются операциями ЦП вместо операции, включающие широко используется диск или сетевые ресурсы. Использование асинхронных методов для операций ЦП не дает преимущества и приводит к дополнительной нагрузки.

В общем случае используйте асинхронные методы для следующих условий:

- Вы вызываете служб, которые могут быть использованы через асинхронных методов, и вы используете .NET 4.5 или более поздней.
- Операции являются сети или ввода вывода вместо ЦП.
- Параллелизм имеет большее, чем простота кода.
- Вы хотите предоставить механизм, который позволяет пользователям отменить длительные запрос.
- При переключении потоков преимущество перевешивает стоимость переключения контекста. В общем случае следует метод асинхронной Если синхронный метод блокирует поток запроса ASP.NET при не выполняют никакой работы. Путем вызова асинхронного потока запросов ASP.NET не блокируется во время ожидания запроса веб-службы завершить не выполняют никакой работы.
- Тестирование показало, что блокировка операций приводит к ухудшению производительности сайта и что IIS может обслуживать большее количество запросов с помощью асинхронных методов для этих заблокированных вызовов.

  Загружаемый пример показано, как эффективно использовать асинхронные методы. Предоставленный образец была разработана для представлена простая демонстрация асинхронного программирования в ASP.NET 4.5. Образец не является эталонную архитектуру для асинхронного программирования в ASP.NET. Программа-пример вызывает [веб-API ASP.NET](../../../web-api/index.md) методы, которые в свою очередь вызывают [Task.Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) для имитации вызовов длительных веб-службы. Большинство приложений не продемонстрируют такие очевидные преимущества для использования асинхронных методов.   
  
Несколько приложений требуют все методы, чтобы быть асинхронным. Часто преобразование нескольких синхронных методов в асинхронных методов обеспечивает наилучший прирост эффективности для требуемого объема работ.

## <a id="SampleApp"></a>  Пример приложения

Можно загрузить пример приложения из [ https://github.com/RickAndMSFT/Async-ASP.NET ](https://github.com/RickAndMSFT/Async-ASP.NET) на [GitHub](https://github.com/) сайта. Хранилище состоит из трех проектов:

- *WebAppAsync*: Проект веб-форм ASP.NET, в котором веб-API **WebAPIpwg** службы. Большая часть кода, для нашего руководства это из этого проекта.
- *WebAPIpgw*: Проект веб-API ASP.NET MVC 4, который реализует `Products, Gizmos and Widgets` контроллеров. Он предоставляет данные для *WebAppAsync* проекта и *Mvc4Async* проекта.
- *Mvc4Async*: Проект ASP.NET MVC 4, который содержит код, используемый в другом руководстве. Он выполняет вызовы веб-API **WebAPIpwg** службы.

## <a id="GizmosSynch"></a>  На странице синхронной элементы

 В следующем коде показан `Page_Load` синхронный метод, который используется для отображения списка элементы. (В этой статье gizmo — это вымышленная механические устройство). 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample1.cs)]

В следующем коде показан `GetGizmos` метода gizmo службы.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample2.cs)]

`GizmoService GetGizmos` Метод передает URI в службе ASP.NET Web API HTTP, который возвращает список элементы данных. *WebAPIpgw* проект содержит реализацию веб-API `gizmos, widget` и `product` контроллеров.  
Ниже показана страница элементы из образца проекта.

![Элементы](using-asynchronous-methods-in-aspnet-45/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>  Создание асинхронных элементы страницы

В образце используется новый [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) и [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ключевые слова (доступный в .NET 4.5 и Visual Studio 2012) позволяет вести сложных преобразований, необходимых для компилятора Асинхронное программирование. Компилятор позволяет писать код, используя конструкции потока синхронной управления C#, и компилятор автоматически применяет преобразования, необходимые для использования обратных вызовов, чтобы избежать блокировки потоков.

Асинхронные страницы ASP.NET необходимо включить [страницы](https://msdn.microsoft.com/library/ydy4x04a.aspx) директиву `Async` набором атрибутов «true». В следующем коде показан [страницы](https://msdn.microsoft.com/library/ydy4x04a.aspx) директиву `Async` атрибут «true» для *GizmosAsync.aspx* страницы.

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample3.aspx?highlight=1)]

В следующем коде показан `Gizmos` синхронной `Page_Load` метод и `GizmosAsync` асинхронной страницы. Если браузер поддерживает [HTML 5 &lt;пометить&gt; элемент](http://www.w3.org/wiki/HTML/Elements/mark), вы сможете увидеть изменения в `GizmosAsync` в выделение желтым цветом.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample4.cs)]

Асинхронная версия:

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample5.cs?highlight=3,6-7,9,11)]

 Следующие изменения были применены к Разрешить `GizmosAsync` страница выполняться асинхронно.

- [Страницы](https://msdn.microsoft.com/library/ydy4x04a.aspx) директива должна иметь `Async` набором атрибутов «true».
- `RegisterAsyncTask` Метод используется для регистрации асинхронная задача, содержащий код, который выполняется асинхронно.
- Новый `GetGizmosSvcAsync` метод помечен атрибутом [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) ключевое слово, которое указывает компилятору создавать обратные вызовы для частей тела и автоматически создавать `Task` возвращаемый.
- &quot;Async&quot; был добавлен к имени асинхронного метода. Добавление «Async» не является обязательным, но является соглашением, при написании асинхронных методов.
- Тип возвращаемого значения нового `GetGizmosSvcAsync` метод `Task`. Тип возвращаемого значения `Task` представляет текущую операцию и предоставляет этот метод с дескриптором, через который ожидает завершения асинхронной операции.
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ключевое слово была применена для вызова веб-службы.
- Был вызван асинхронный веб-API службы (`GetGizmosAsync`).

Внутри элемента `GetGizmosSvcAsync` другого асинхронного метода, основной метод `GetGizmosAsync` вызывается. `GetGizmosAsync` немедленно возвращает `Task<List<Gizmo>>` со временем, завершается, если данные недоступны. Так как не нужно ничего делать, пока не получится gizmo данные, код ожидает завершения задачи (с помощью **await** ключевое слово). Можно использовать **await** ключевое слово только в методы, помеченные **async** ключевое слово.

**Await** ключевое слово не блокирует поток до завершения задачи. Он регистрирует остальную метода как обратный вызов в задаче и немедленно возвращает. После завершения выполнения ожидающей задачи в конечном счете, он этот обратный вызов и таким образом возобновить выполнение метод справа, где она была остановлена. Дополнительные сведения об использовании [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) и [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) ключевые слова и [задачи](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) пространства имен, см. в разделе [ссылки async](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async).

В следующем коде показан `GetGizmos` и `GetGizmosAsync` методы.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample6.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample7.cs?highlight=1,4-8)]

 Асинхронные изменения аналогичны внесенные **GizmosAsync** выше. 

- Подпись метода, аннотированных в [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) ключевое слово, возвращаемый тип был изменен на `Task<List<Gizmo>>`, и *Async* добавленный к имени метода.
- Асинхронный [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) класс используется вместо синхронного [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx) класса.
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) ключевое слово была применена к [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)[GetAsync](https://msdn.microsoft.com/library/hh158944(VS.110).aspx) асинхронного метода.

На следующем рисунке представление асинхронных gizmo.

![async](using-asynchronous-methods-in-aspnet-45/_static/image2.png)

Браузеры представлением данных элементы идентична представлениям, созданным синхронный вызов. Единственное различие — это асинхронная версия может быть более высокую производительность при больших нагрузках.

## <a name="registerasynctask-notes"></a>Метод RegisterAsyncTask заметки

Подключить методы с `RegisterAsyncTask` будет выполняться сразу после [PreRender](https://msdn.microsoft.com/library/ms178472.aspx). Также можно асинхронных событий void страницу напрямую, как показано в следующем коде:

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample8.cs)]

Недостаток асинхронных событий void состоит, что разработчикам больше не имеет полный контроль над при выполнения события. Например если оба .aspx и. Определение главного `Page_Load` события и один или оба значения являются асинхронными, порядок выполнения не гарантируется. Том же порядке indeterminiate для обработчиков событий, отличных от (такие как `async void Button_Click` ) применяется. Для большинства разработчиков это приемлемо, но те, которым требуется полный контроль над порядком выполнения следует использовать только API, например `RegisterAsyncTask` , использовать методы, которые возвращают объект задачи.

## <a id="Parallel"></a>  Параллельное выполнение нескольких операций

Асинхронные методы имеют значительное преимущество синхронных методов, когда действие должно выполнить несколько независимых операций. В приведенном примере модуль синхронной страницы *PWG.aspx*(для продуктов, мини-приложения и элементы) отображаются результаты трех вызовов веб-служб для получения списка продуктов, мини-приложения и элементы. [Веб-API ASP.NET](../../../web-api/index.md) проект, который предоставляет эти службы использует [Task.Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) чтобы имитировать задержки или медленные вызовы методов. Когда для задержки задано значение 500 миллисекунд, асинхронный *PWGasync.aspx* страница занимает немного более чем 500 мс до завершения во время синхронного `PWG` имеет версию, чем 1 500 миллисекунд. Синхронный *PWG.aspx* страница показана в следующем коде.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample9.cs)]

Асинхронный `PWGasync` ниже приведен код программной части.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample10.cs?highlight=5,11,21)]

На следующем рисунке показаны представления, возвращаемого из асинхронной *PWGasync.aspx* страницы.

![](using-asynchronous-methods-in-aspnet-45/_static/image3.png)

## <a id="CancelToken"></a>  Использование токена отмены

Асинхронные методы, возвращающие `Task`являются можно отменить; они принимают [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) параметр, если оно предоставлено с `AsyncTimeout` атрибут [страницы](https://msdn.microsoft.com/library/ydy4x04a.aspx) директива. В следующем коде показан *GizmosCancelAsync.aspx* страницы с временем ожидания в секунду.

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample11.aspx?highlight=1)]

В следующем коде показан *GizmosCancelAsync.aspx.cs* файла.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample12.cs?highlight=6,9)]

В примере приложения, выбрав *GizmosCancelAsync* связать вызовы *GizmosCancelAsync.aspx* странице и демонстрирует Отмена (по времени ожидания) асинхронного вызова. Так как время задержки входит в диапазон случайных, может потребоваться для обновления страницы несколько раз, чтобы получить сообщение об ошибке времени ожидания.

## <a id="ServerConfig"></a>  Конфигурация сервера для вызовов веб-службы высокого уровня параллелизма и высокий уровень задержки

Чтобы воспользоваться преимуществами асинхронных веб-приложения, может потребоваться внести некоторые изменения в конфигурации сервера по умолчанию. Имейте в виду при настройке и нагрузочное тестирование асинхронных веб-приложения следующее.

- Windows 7, Windows Vista, Windows 8 и все клиентские операционные системы Windows иметь не более 10 одновременных запросов. Вам потребуется операционной системы Windows Server, чтобы ознакомиться с преимуществами асинхронных методов в условиях высокой нагрузки.
- Зарегистрируйте .NET 4.5 с IIS с повышенными привилегиями команду, используя следующую команду:  
  %windir%\Microsoft.NET\Framework64 \v4.0.30319\aspnet\_regiis -i  
  См. в разделе [средство регистрации ASP.NET IIS (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h.aspx)
- Может потребоваться увеличить [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) предел очереди из значения по умолчанию 1000 до 5000. Если для параметра установлено слишком низкое, может появиться [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) отклонять запросы с состоянием HTTP 503. Изменение предел очереди HTTP.sys.

    - Откройте диспетчер IIS и перейдите в область пулов приложений.
    - Щелкните правой кнопкой целевой пул приложений и выберите **Дополнительные параметры**.  
        ![Дополнительно](using-asynchronous-methods-in-aspnet-45/_static/image4.png)
    - В **Дополнительные параметры** » диалогового окна «Изменение *длина очереди* от 1000 до 5 000.  
        ![Длина очереди](using-asynchronous-methods-in-aspnet-45/_static/image5.png)  
  
  Обратите внимание, на рисунках выше, .NET framework указана как v4.0, несмотря на то, что пул приложений используется .NET 4.5. Чтобы понять это несоответствие, см. в следующих:

- [Управление версиями .NET и многоплатформенного нацеливания - .NET 4.5 является обновлением на месте для .NET 4.0](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
- [Настройка приложения IIS или пул приложений для использования ASP.NET 3.5, а не 2.0](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
- [Версии и зависимости платформы .NET Framework](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)

- Если приложение использует веб-служб или System.NET для взаимодействия с серверной части по протоколу HTTP вам может потребоваться увеличить [connectionManagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx) элемент. Для приложений ASP.NET это ограничено с помощью функции автоматической настройки в 12 раз число ЦП. Это означает, что в quad-proc, можно иметь не более 12 \* 4 = 48 одновременных подключений к IP-адрес конечной точки. Так как это привязывается к [autoConfig](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx), самый простой способ увеличить `maxconnection` в ASP.NET является установка приложения [System.Net.ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) в обработчике из `Application_Start` метод в *global.asax* файл. Ознакомьтесь с примером загрузить пример.
- В .NET 4.5, по умолчанию 5000 для [MaxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx) будет прекрасно работать.

## <a name="contributors"></a>Авторы

- [Levi Broderick](http://stackoverflow.com/users/59641/levi)
- [Том Дайкстра](http://www.bing.com/search?q=site%3Aasp.net+%22Tom+Dykstra%22+-forums.asp.net&amp;qs=n&amp;form=QBRE&amp;pq=site%3Aasp.net+%22tom+dykstra%22+-forums.asp.net&amp;sc=8-42&amp;sp=-1&amp;sk=)
- [Брэд Вилсон](http://bradwilson.typepad.com/)
- [HongMei Ge](https://blogs.msdn.com/b/hongmeig/)