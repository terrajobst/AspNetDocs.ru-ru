---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 'Практическое лабораторное занятие. One ASP.NET: Интеграция веб-форм ASP.NET, MVC и веб-API | Документация Майкрософт'
author: rick-anderson
description: ASP.NET — это платформа для разработки веб-сайтов, приложений и служб с помощью специализированных технологий, таких как MVC, веб-API и другие. С расширением ASP.NET h...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: c18911680b59448cd67190f71e951a3fcf3d0478
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044131"
---
<a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a>Практическое лабораторное занятие. One ASP.NET: интеграция веб-форм ASP.NET, MVC и веб-API
====================
по [Web Слышатся Team](https://twitter.com/webcamps)

[Скачайте комплект учебных материалов по лагеря Web](http://aka.ms/webcamps-training-kit)

> ASP.NET — это платформа для разработки веб-сайтов, приложений и служб с помощью специализированных технологий, таких как MVC, веб-API и другие. С расширением ASP.NET с момента его создания и выраженное должны эти технологии интегрированы, предпринимались последних в работе по направлению к **One ASP.NET**.
> 
> Visual Studio 2013 представлены новой системы проектов, который позволит вам создавать приложения и использовать все технологии ASP.NET в одном проекте. Эта функция устраняет необходимость для выбора одной технологии в начале проекта и палочка с ним и вместо рекомендуют использовать несколько платформ ASP.NET, в рамках одного проекта.
> 
> Все примеры кода и фрагменты кода включены в Web лагеря комплект обучающих материалов, доступных в [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit).


<a id="Overview"></a>
## <a name="overview"></a>Обзор

<a id="Objectives"></a>
### <a name="objectives"></a>Цели

В этой практической работу вы узнаете, как:

- Создание веб-сайта, на основе **One ASP.NET** тип проекта
- Использование разных **ASP.NET** платформы, такие как **MVC** и **веб-API** в одном проекте
- Определить основные компоненты **ASP.NET** приложения
- Воспользоваться преимуществами **формирование шаблонов ASP.NET** framework автоматически создавать контроллеры и представления для выполнения операций CRUD на основе вашей модели классов
- Предоставлять тот же набор сведений в форматах машины - и удобное для восприятия, с помощью подходящего средства для каждого задания

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Предварительные требования

Для завершения этой практической работу требуется следующее:

- [Visual Studio Express 2013 для Web](https://www.microsoft.com/visualstudio/) или более поздней версии
- [Visual Studio 2013 с обновлением 1](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a>Установка

Для выполнения упражнений в этой практической работу, необходимо сначала настроить среду.

1. Откройте Windows Explorer и перейдите к лаборатории **источника** папки.
2. Щелкните правой кнопкой мыши **Setup.cmd** и выберите **Запуск от имени администратора** для запуска процесса установки, будет настроить среду и установить фрагменты кода Visual Studio для этой лабораторной работы.
3. Если отображается диалоговое окно контроля учетных записей, подтвердите действие для продолжения.

> [!NOTE]
> Убедитесь, что все зависимости для этой лабораторной работы вы вернули перед запуском программы установки.


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>Фрагменты кода

В этом документе лаборатории вам будет рекомендовано вставлять блоки кода. Для удобства основная часть кода предоставляется как фрагменты кода Visual Studio, к которому можно получить из в Visual Studio 2013, чтобы избежать необходимости добавлять ее вручную.

> [!NOTE]
> Каждого упражнения сопровождается начальный решения, расположенный в **начать** папку упражнения, чему вы сможете каждого упражнения, независимо от других. Имейте в виду, что фрагменты кода, которые добавляются во время атаки, отсутствуют эти стартовые решения и могут не работать, пока не будут выполнены упражнения. В исходном коде для упражнения, вы также найдете **окончания** папку, содержащую решение Visual Studio с кодом, полученный в результате выполнения действий, описанных в соответствующий упражнении. Эти решения можно использовать в качестве руководства, если вам нужна дополнительная помощь, отвечая на это Практическое занятие.


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>Упражнения

Это Практическое занятие включает в себя следующие упражнения:

1. [Создание нового проекта Web Forms](#Exercise1)
2. [Создание с помощью формирования шаблонов контроллера MVC](#Exercise2)
3. [Создание контроллера Web API, с помощью формирования шаблонов](#Exercise3)

Предполагаемое время для выполнения этого лабораторного: **60 минут**

> [!NOTE]
> При первом запуске Visual Studio, необходимо выбрать один из предварительно определенных коллекций параметров. Каждой коллекции предопределенных соответствует конкретному стилю разработки и определяет макетов окон, поведение редактора, фрагменты кода IntelliSense и параметры диалогового окна. В этом лабораторном занятии описаны действия, необходимые для выполнения данной задачи в Visual Studio при использовании **обычные параметры разработки** коллекции. При выборе другого набора параметров для среды разработки, возможно, различия в действиях, которые следует учитывать.


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a>Упражнение 1. Создание нового проекта Web Forms

В этом упражнении вы создадите новый узел веб-форм в Visual Studio 2013 с использованием **One ASP.NET** единой опыт работы с проектами, которые позволят вам легко интегрировать компоненты веб-форм, MVC и веб-API в одном приложении. Затем изучите сгенерированное решение и определить его частей, и наконец вы увидите веб-сайта в действии.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a>Задача 1 – Создание нового сайта с помощью одного интерфейса ASP.NET

В этой задаче вы начнете создание нового веб-сайта в Visual Studio на основе **One ASP.NET** тип проекта. **One ASP.NET** объединяет все технологии ASP.NET и предоставляет вам возможность комбинировать и сопоставлять их при необходимости. Затем будет распознавать различных компонентов веб-форм, MVC и веб-API, находящиеся рядом друг с другом в вашем приложении.

1. Откройте **Visual Studio Express 2013 для Web** и выберите **файл | Создать проект...**  для запуска нового решения.

    ![Создание нового проекта](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    *Создание нового проекта*
2. В **новый проект** выберите **веб-приложение ASP.NET** под **Visual C# | Web** вкладку и убедитесь, что **.NET Framework 4.5** выбран. Назовите проект *MyHybridSite*, выберите **расположение** и нажмите кнопку **ОК**.

    ![Новый проект веб-приложения ASP.NET](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    *Создание нового проекта веб-приложения ASP.NET*
3. В **новый проект ASP.NET** выберите **веб-форм** шаблона и выберите **MVC** и **веб-API** параметры. Кроме того, убедитесь, что **проверки подлинности** параметру присваивается **учетные записи отдельных пользователей**. Нажмите кнопку **ОК** , чтобы продолжить.

    ![Создание нового проекта с помощью шаблона веб-форм, включая компоненты веб-API и MVC](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    *Создание нового проекта с помощью шаблона веб-форм, включая компоненты веб-API и MVC*
4. Теперь вы можете изучить структуру сгенерированное решение.

    ![Изучение созданного решения](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    *Изучение созданного решения*

    1. **Учетная запись:** Эта папка содержит страницы веб-формы для регистрации, вход и управление учетными записями пользователей приложения. Эта папка будет добавлена при **учетные записи отдельных пользователей** выбран параметр проверки подлинности во время настройки шаблона проекта веб-форм.
    2. **Модели:** Эта папка будет содержать классы, представляющие данные приложения.
    3. **Контроллеры** и **представления**: Эти папки являются обязательными для **ASP.NET MVC** и **веб-API ASP.NET** компонентов. Рассмотрим в следующих упражнениях технологии MVC и веб-API.
    4. **Default.aspx**, **Contact.aspx** и **About.aspx** файлы, предварительно определенные страницы веб-форм, которые можно использовать в качестве отправных точек для создания страниц, относящиеся к вашей приложение. Программная логика этих файлов находится в отдельном файле, который называется &quot;кода&quot; файл, который имеет &quot;. aspx.vb&quot; или &quot;. aspx.cs&quot; расширения (в зависимости от язык, используемый). Логику кода выполняется на сервере и динамически создает выходные данные HTML для страницы.
    5. **Site.Master** и **Site.Mobile.Master** страницы определяют внешний вид и стандартное поведение всех страниц в приложении.
5. Дважды щелкните **Default.aspx** файл для просмотра содержимого страницы.

    ![Просмотр страницы Default.aspx](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    *Просмотр страницы Default.aspx*

    > [!NOTE]
    > **Страницы** директивы в верхней части файла определяет атрибуты страницы веб-форм. К примеру **MasterPageFile** атрибут указывает путь к главной странице — в этом случае *Site.Master* страницы - и **Inherits** атрибут определяет Класс фонового кода для страницы, чтобы наследовать. Этот класс находится в файле определяется **фонового кода** атрибута.
    > 
    > **Asp: Content** управления содержит фактическое содержимое страницы (текст, разметку и элементы управления) и сопоставляется с **asp: ContentPlaceHolder** управления на главной странице. В этом случае будет отображено содержимое страницы внутри *MainContent* управления, определенных в *Site.Master* страницы.
6. Разверните **приложения\_запустить** папку и обратите внимание, что **WebApiConfig.cs** файла. Visual Studio включены этот файл в сгенерированное решение, так как вы включили веб-API, при настройке проекта с помощью шаблона One ASP.NET.
7. Откройте **WebApiConfig.cs** файла. В *WebApiConfig* направляет класса, вы найдете конфигурации, связанные с веб-API, которая сопоставляет HTTP **контроллеров веб-API**.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. Откройте **RouteConfig.cs** файла. Внутри *RegisterRoutes* вы найдете конфигурации, связанной с моделью MVC, которая сопоставляет маршруты HTTP, чтобы метод **контроллеров MVC**.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a>Задача 2 – при запуске решения

В этой задаче будет запустите сгенерированное решение и изучение приложения и некоторые его функции, такие как переписывание URL-адресов и встроенная проверка подлинности.

1. Чтобы запустить решение, нажмите клавишу **F5** или нажмите кнопку **запустить** расположенную на панели инструментов. На домашней странице приложения откроется в браузере.

    ![При запуске решения](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. Убедитесь, что вызываются на страницах веб-форм. Чтобы сделать это, добавьте **/contact.aspx** на URL-адрес в адресной строке и нажмите клавишу **ввод**.

    ![Понятные URL-адреса](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    *Понятные URL-адреса*

    > [!NOTE]
    > Как вы видите, URL-адрес примет **/обратитесь в службу**. Начиная с **ASP.NET 4**, были добавлены возможности маршрутизации URL-адрес для веб-форм, поэтому вы можете писать URL-адреса, например *[ http://www.mysite.com/products/software ](http://www.mysite.com/products/software)* вместо  *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*. Дополнительные сведения см. [маршрутизации URL-адресов](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).
3. Теперь вы изучить процесс проверки подлинности, интегрировать в приложение. Чтобы сделать это, нажмите кнопку **зарегистрировать** в правом верхнем углу страницы.

    ![Регистрация нового пользователя](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    *Регистрация нового пользователя*
4. В **зарегистрировать** введите **имя пользователя** и **пароль**, а затем нажмите кнопку **зарегистрировать**.

    ![Страница «Регистрация»](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    *Страница «Регистрация»*
5. Приложение регистрирует новую учетную запись, и пользователь проходит проверку подлинности.

    ![Пользователь прошел проверку подлинности](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    *Пользователь прошел проверку подлинности*
6. Вернитесь к Visual Studio и нажать клавишу **SHIFT + F5** остановить отладку.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a>Упражнение 2. Создание с помощью формирования шаблонов контроллера MVC

В этом упражнении будет воспользоваться преимуществами платформы формирование шаблонов ASP.NET в Visual Studio для создания контроллера ASP.NET MVC 5 с действиями и представлениями Razor для выполнения операций CRUD, не написав ни строчки кода. Процесс формирования шаблонов использует Entity Framework Code First для создания контекста данных и схемы базы данных в базе данных SQL.

**О платформе Entity Framework Code First**

Entity Framework (EF) — это объектно реляционного сопоставления (ORM), которая позволяет создавать приложения для доступа к данным, работающие с концептуальной моделью приложения вместо программирования, напрямую с помощью реляционной схемой хранения.

Entity Framework Code First рабочий процесс моделирования можно использовать собственные классы домена для представления модели, который использует EF при выполнении запроса, функции отслеживания изменений и обновления. С помощью Code First рабочий процесс разработки, вы не обязательно должны начинаться приложения путем создания базы данных или указание схемы. Вместо этого можно написать стандартных классов .NET, которые определяют наиболее подходящий объектов модели предметной области для вашего приложения, и платформа Entity Framework автоматически создаст базу данных.

> [!NOTE]
> Дополнительные сведения о платформе Entity Framework [здесь](../../../entity-framework.md).


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a>Задача 1 – Создание новой модели

Теперь мы определим **Person** класс, который будет модели, использованный во время формирования шаблонов для создания контроллера MVC и представлений. Сначала нужно создать **Person** класс модели и операции CRUD в контроллере будут автоматически созданы с помощью функции формирования шаблонов.

1. Откройте **Visual Studio Express 2013 для Web** и **MyHybridSite.sln** решение находится в **источника/Ex2-MvcScaffolding/начало** папки. Кроме того можно продолжить с решением, полученный в предыдущем упражнении.
2. В **обозревателе решений**, щелкните правой кнопкой мыши **моделей** папке **MyHybridSite** проекта и выберите **Add | Класс...** .

    ![Добавление класса модели Person](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    *Добавление класса модели Person*
3. В **Добавление нового элемента** диалоговом окне имя файла *Person.cs* и нажмите кнопку **добавить**.

    ![Создание класса модели Person](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    *Создание класса модели Person*
4. Замените содержимое **Person.cs** файла следующим кодом. Нажмите клавишу **CTRL + S** для сохранения изменений.

    (Code Snippet - *PersonClass BringingTogetherOneAspNet - Ex2 -*)

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. В **обозревателе решений**, щелкните правой кнопкой мыши **MyHybridSite** проекта и выберите **построения**, или нажмите клавишу **CTRL + SHIFT + B** для сборки проекта.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a>Задача 2 – Создание контроллера MVC

Теперь, когда **Person** создания модели, вы будете использовать формирование шаблонов ASP.NET MVC с Entity Framework для создания действия CRUD контроллера и представлений для **Person**.

1. В **обозревателе решений**, щелкните правой кнопкой мыши **контроллеров** папке **MyHybridSite** проекта и выберите **Add | Создать шаблонный элемент...** .

    ![Создание нового формирования шаблонов контроллера](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    *Создание нового контроллера Скаффолдинга*
2. В **Добавление шаблона** выберите **контроллер MVC 5 с представлениями, использующий Entity Framework** и нажмите кнопку **Add.**

    ![Выбрав контроллер MVC 5 с представлениями и Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    *Выбрав контроллер MVC 5 с представлениями и Entity Framework*
3. Задайте *MvcPersonController* как **имя контроллера**выберите **использовать асинхронные действия контроллера** и выберите **Person (MyHybridSite.Models)**  как **класс модели**.

    ![Добавление контроллера MVC с помощью формирования шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    *Добавление контроллера MVC с помощью формирования шаблонов*
4. В разделе **класс контекста данных**, нажмите кнопку **новый контекст данных...** .

    ![Создать новый контекст данных](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    *Создать новый контекст данных*
5. В **новый контекст данных** диалоговом окне имя новый контекст данных *PersonContext* и нажмите кнопку **добавить**.

    ![Создание нового PersonContext](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    *Создание нового типа PersonContext*
6. Нажмите кнопку **добавить** для создания нового контроллера для **Person** с помощью формирования шаблонов. Visual Studio создаст действий контроллера, контекст данных Person и представлениями Razor.

    ![После создания контроллер MVC с помощью формирования шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    *После создания контроллер MVC с помощью формирования шаблонов*
7. Откройте **MvcPersonController.cs** файл **контроллеров** папки. Обратите внимание на то, что методы действия CRUD были созданы автоматически.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > Выбрав **использовать асинхронные действия контроллера** смарт-теге формирование шаблонов параметров в предыдущих шагах, Visual Studio создает асинхронные методы действия для всех действий, которые включают в себя доступ к контексту данных пользователя. Рекомендуется использовать асинхронные методы действия для выполняющейся длительное время, не связаны с ЦП запросы для предотвращения блокировки веб-сервера от выполнения операций во время обработки запроса.

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a>Задача 3 – при запуске решения

В этой задаче будет выполняться представлений для решения еще раз, чтобы убедиться, что **Person** работают надлежащим образом. Вы добавите новый пользователь, чтобы проверить, успешно сохранены в базе данных.

1. Нажмите клавишу **F5** для запуска решения.
2. Перейдите к **/MvcPerson**. Должна появиться шаблонный представление, отображающее список пользователей.
3. Нажмите кнопку **Create New** для добавления нового пользователя.

    ![Переход к сформированные представления MVC](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    *Переход к сформированные представления MVC*
4. В **создать** просмотреть, укажите **имя** и **возраст** человека, и нажмите кнопку **создать**.

    ![Добавление нового пользователя](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    *Добавление нового пользователя*
5. Новый пользователь добавляется в список. В списке элементов выберите **сведения** для отображения представления сведений пользователя. Затем в **сведения** , щелкните **обратно к списку** чтобы вернуться к представлению списка.

    ![Представление сведений пользователя](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    *Представление сведений пользователя*
6. Нажмите кнопку **удалить** ссылка для удаления пользователя. В **удалить** , щелкните **удалить** для подтверждения операции.

    ![Удаление пользователя](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    *Удаление пользователя*
7. Вернитесь к Visual Studio и нажать клавишу **SHIFT + F5** остановить отладку.

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a>Упражнение 3. Создание контроллера Web API, с помощью формирования шаблонов

Платформа веб-API является частью стека ASP.NET и предназначенных для упрощения реализации службы HTTP, как правило, отправки и получения данных в формате JSON или XML через API-интерфейсов RESTful.

В этом упражнении будет использовать формирование шаблонов ASP.NET снова создать контроллер Web API. Применяются те же **Person** и **PersonContext** классов из предыдущего упражнения для предоставляют одинаковые данные пользователя в формате JSON. Вы увидите, как можно предоставить те же ресурсы по-разному внутри одного приложения ASP.NET.

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a>Задача 1 – Создание контроллер веб-API

В этой задаче вы создадите новый **контроллер Web API** , будет представлять данные пользователя в машинные команды компьютера в формате JSON.

1. Если еще не открыт, откройте **Visual Studio Express 2013 для Web** и откройте **MyHybridSite.sln** решение находится в **источника/Ex3-веб-API/начало** папки. Кроме того можно продолжить с решением, полученный в предыдущем упражнении.

    > [!NOTE]
    > При запуске с помощью решения Begin из Упражнение 3, нажмите клавишу **CTRL + SHIFT + B** для сборки решения.
2. В **обозревателе решений**, щелкните правой кнопкой мыши **контроллеров** папке **MyHybridSite** проекта и выберите **Add | Создать шаблонный элемент...** .

    ![Создание нового формирования шаблонов контроллера](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    *Создание нового формирования шаблонов контроллера*
3. В **Добавление шаблона** выберите **веб-API** в области слева, затем **контроллер Web API 2 с действиями, использующий Entity Framework** в средней области и нажмите кнопку  **Добавите.**

    ![Выбрав контроллер Web API 2 с действиями и Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "выбрав контроллер Web API 2 с действиями и Entity Framework")

    *Выбрав контроллер Web API 2 с действиями и Entity Framework*
4. Задайте *ApiPersonController* как **имя контроллера**выберите **использовать асинхронные действия контроллера** и выберите **Person (MyHybridSite.Models)**  и **PersonContext (MyHybridSite.Models)** как **модели** и **контекст данных** классы соответственно. Затем нажмите кнопку **Добавить**.

    ![Добавление контроллер веб-API с помощью формирования шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Добавление контроллера в веб-API с помощью формирования шаблонов")

    *Добавление контроллера в веб-API с помощью формирования шаблонов*
5. Visual Studio создаст **ApiPersonController** класс с четырьмя действиями CRUD для работы с данными.

    ![После создания контроллера веб-API с помощью формирования шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "после создания контроллера веб-API с помощью формирования шаблонов")

    *После создания контроллера веб-API с помощью формирования шаблонов*
6. Откройте **ApiPersonController.cs** файл и проверьте *GetPeople* метода действия. Этот метод отправляет запрос в поле db **PersonContext** типа для получения данных пользователей.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. Теперь обратите внимание, что с комментарием над определение метода. Он предоставляет URI, который представляет это действие, который будет использоваться в следующей задаче.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > По умолчанию веб-API настроен для перехвата запросов к */API* путь, чтобы избежать конфликтов с помощью контроллеров MVC. Если вам нужно изменить этот параметр, см. раздел [маршрутизации в ASP.NET Web API](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a>Задача 2 – при запуске решения

В этой задаче будет использоваться в Internet Explorer **средства разработчика F12** проверяемый полный ответ от контроллера веб-API. Вы увидите, как можно записывать сетевой трафик, чтобы получить дополнительные сведения о данных приложения.

> [!NOTE]
> Убедитесь, что **Internet Explorer** выбран в **запустить** расположенную на панели инструментов Visual Studio.
> 
> ![Параметр Internet Explorer](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> **Средства разработчика F12** имеют широкий набор функциональных возможностей, не охваченных этого практического занятия. Если вы хотите узнать больше об этом, см. раздел [с помощью средств разработчика F12](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).


1. Нажмите клавишу **F5** для запуска решения.

    > [!NOTE]
    > Чтобы правильно выполнить эту задачу, приложение должно иметь данные. Если пустой базы данных, можно вернуться к задаче 3 в упражнении 2 и выполните действия по созданию нового пользователя, с помощью представлений MVC.
2. В браузере, нажмите клавишу **F12** открыть **средств разработчика** панели. Нажмите клавишу **CTRL** + **4** или нажмите кнопку **сети** значок, а затем щелкните кнопку с зеленой стрелкой, чтобы начать отслеживать сетевой трафик.

    ![Запуск записи сетевых данных веб-API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "записи сетевых данных инициирует веб-API")

    *Запуск записи сетевых данных веб-API*
3. Добавление **api/ApiPerson** на URL-адрес в адресной строке браузера. Теперь проверьте сведения об ответе от **ApiPersonController**.

    ![Извлечение данных пользователя через веб-API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "извлечение данных пользователя через веб-API")

    *Извлечение данных пользователя через веб-API*

    > [!NOTE]
    > После завершения загрузки, вам будет предложено задать действие с помощью загруженного файла. Не закрывайте диалоговое окно, чтобы иметь возможность смотреть содержимое ответа через окно инструментов для разработчиков.
4. Теперь будет проверять текст ответа. Чтобы сделать это, нажмите кнопку **сведения** вкладке и нажмите кнопку **текст ответа**. Вы можете проверить, что загруженные данные — это список объектов со свойствами **идентификатор**, **имя** и **возраст** , которые соответствуют **Person** класс.

    ![Просмотр веб-текст ответа API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "просмотра веб-текст ответа API")

    *Текст ответа API Web просмотра*

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a>Задача 3 – добавление справки API веб-страниц

При создании веб-API, полезно создать страницу справки, чтобы другие разработчики будете знать, как вызвать API. Можно создать и обновлять страницы документации вручную, но лучше автоматически создавать их, чтобы не пришлось выполнять работу обслуживания. В этой задаче будет использовать пакет Nuget для автоматического создания страниц справки веб-API в решение.

1. Из **средства** меню в Visual Studio, выберите пункт **диспетчер пакетов NuGet**, а затем нажмите кнопку **консоль диспетчера пакетов**.
2. В **консоль диспетчера пакетов** окно, выполните следующую команду:

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > **Microsoft.AspNet.WebApi.HelpPage** пакет устанавливает необходимые сборки и добавляет представлений MVC для страницы справки, в разделе **области/HelpPage** папки.

    ![Область HelpPage](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage область")

    *Область HelpPage*
3. По умолчанию с помощью страницы имеют заполнитель строки для документации. Комментарии XML-документации можно использовать для создания документации. Чтобы включить эту функцию, откройте **HelpPageConfig.cs** файл, расположенный в **областей, приложения или HelpPage\_запустить** папки и раскомментируйте следующую строку:

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. В **обозревателе решений**, щелкните правой кнопкой мыши проект **MyHybridSite**выберите **свойства** и нажмите кнопку **построения** вкладки.

    ![Вкладка "сборка"](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Создание раздела")

    *Вкладка "сборка"*
5. В разделе **вывода**выберите **XML-файл документации**. В поле ввода введите **приложения\_Data/XmlDocument.xml**.

    ![Выходные данные раздела на вкладке "Построение"](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "вывода раздела на вкладке \"Построение\"")

    *Раздел выходных данных на вкладке "Построение"*
6. Нажмите клавишу **CTRL** + **S** для сохранения изменений.
7. Откройте **ApiPersonController.cs** файла из **контроллеров** папки.
8. Введите новую строку между *GetPeople* сигнатуру метода и */ / GET api/ApiPerson* комментарий, а затем введите три косые черты.

    > [!NOTE]
    > Visual Studio автоматически добавляет XML-элементы, которые определяют документацию по методу.
9. Добавьте текст сводки и возвращаемое значение для *GetPeople* метод. Он должен выглядеть следующим образом.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. Нажмите клавишу **F5** для запуска решения.
11. Добавление **/help** URL-адрес в адресной строке, чтобы перейти на страницу справки.

    ![Страница справки веб-API ASP.NET](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "страница справки веб-API ASP.NET")

    *Страница справки веб-API ASP.NET*

    > [!NOTE]
    > Основное содержимое страницы — это таблица, API-интерфейсов, сгруппированные по контроллера. Записи таблицы создаются динамически, с помощью **IApiExplorer** интерфейс. Если добавить или обновить контроллер API таблицы будут обновляться автоматически в следующий раз вы создадите приложение.
    > 
    > **API** столбце перечислены метод HTTP и относительного URI. **Описание** столбец содержит сведения, которые были извлечены из документации по методу.
12. Обратите внимание, что описание, добавляемого перед определением метода отображается в столбце «Описание».

    ![Описание метода API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "описание метода API")

    *Описание метода API*
13. Выберите один из методов API, чтобы перейти на страницу с более подробными сведениями, включая примеры текстов ответа.

    ![Странице подробной информации](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "страницу подробных сведений")

    *Подробные сведения страницы*

* * *

<a id="Summary"></a>
## <a name="summary"></a>Сводка

Выполнив этой практической работу вы узнали, как:

- Создание нового веб-приложения, используя один интерфейс ASP.NET в Visual Studio 2013
- Интегрировать несколько технологий ASP.NET в один единый проект
- Создание контроллеров и представлений MVC из классах модели с помощью формирования шаблонов ASP.NET
- Создание контроллеров веб-API, которые используют функции, такие как асинхронного программирования и доступа к данным через Entity Framework
- Автоматически создавать веб-страницы справки API контроллеров