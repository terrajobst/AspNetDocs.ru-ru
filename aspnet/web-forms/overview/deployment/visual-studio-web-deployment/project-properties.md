---
uid: web-forms/overview/deployment/visual-studio-web-deployment/project-properties
title: 'ASP.NET веб-развертывание с помощью Visual Studio: свойства проекта | Документация Майкрософт'
author: tdykstra
description: В этой серии руководств показано, как развернуть (опубликовать) веб-приложение ASP.NET в веб-приложениях службы приложений Azure или поставщике услуг размещения стороннего поставщика, Усин...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ec1cec4c-a75f-47af-a2ba-b1e2f971d24b
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/project-properties
msc.type: authoredcontent
ms.openlocfilehash: b2811791a897c9166f6222c23dddc6921e5267ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522942"
---
# <a name="aspnet-web-deployment-using-visual-studio-project-properties"></a>ASP.NET веб-развертывание с помощью Visual Studio: свойства проекта

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать начальный проект](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> В этой серии руководств показано, как развернуть (опубликовать) веб-приложение ASP.NET в веб-приложениях службы приложений Azure или поставщике услуг размещения стороннего поставщика с помощью Visual Studio 2012 или Visual Studio 2010. Сведения о ряде см. в [первом руководстве по ряду](introduction.md).

## <a name="overview"></a>Обзор

Некоторые параметры развертывания настраиваются в свойствах проекта, которые хранятся в файле проекта (файл *. csproj* или *. vbproj* ). В большинстве случаев значения этих параметров по умолчанию нужны, но можно использовать пользовательский интерфейс **свойств проекта** , встроенный в Visual Studio, для работы с этими параметрами, если необходимо их изменить. В этом учебнике вы просматриваете параметры развертывания в **свойствах проекта**. Также создается файл-заполнитель, который вызывает развертывание пустой папки.

## <a name="configure-deployment-settings-in-the-project-properties-window"></a>Настройка параметров развертывания в окне "Свойства проекта"

Большинство параметров, влияющих на то, что происходит во время развертывания, включаются в профиль публикации, как показано в следующих учебниках. Некоторые параметры, о которых следует помнить, находятся на вкладках **Пакет/Публикация** окна **Свойства проекта** . Эти параметры задаются для каждой конфигурации сборки, то есть могут иметь разные параметры для сборки выпуска, чем для отладочной сборки.

В **Обозреватель решений**щелкните правой кнопкой мыши проект **ContosoUniversity** , выберите пункт **Свойства**, а затем перейдите на вкладку **Пакет/Публикация веб-сайта** .

![Вкладка "Упаковка и публикация веб-проекта"](project-properties/_static/image1.png)

Когда окно отображается, оно по умолчанию отображает параметры конфигурации сборки, которая в настоящее время активна для решения. Если в поле **Конфигурация** не указано значение **активно (выпуск)** , выберите **выпуск** , чтобы отобразить параметры конфигурации сборки выпуска. Сборки выпуска развертываются как в тестовой, так и в рабочей среде.

![Выбор конфигурации сборки выпуска](project-properties/_static/image2.png)

Выбрав **Активный (выпуск)** или **выпуск** , вы увидите значения, действующие при развертывании с использованием конфигурации сборки выпуска.

- В поле **элементы для развертывания** выбраны **только файлы, необходимые для запуска приложения** . Другие параметры — **все файлы в этом проекте** или **все файлы в этой папке проекта**. При отсутствии неизменного выбора по умолчанию не следует развертывать файлы исходного кода, например. Этот параметр является причиной, по которой папки, содержащие двоичные файлы SQL Server Compact, должны быть включены в проект. Дополнительные сведения об этом параметре см. в разделе **почему не все файлы в папке проекта развертываются?** в разделе [часто задаваемые вопросы о развертывании проекта веб-приложения ASP.NET](https://msdn.microsoft.com/library/ee942158.aspx).
- Выбрано **исключение созданных отладочных символов** . При использовании этой конфигурации сборки отладка не будет выполняться.
- Выбрана **вкладка включить все базы данных, настроенные на вкладке Пакет/Публикация SQL** . Указывает, будет ли Visual Studio развертывать базы данных и файлы. Несмотря на то, что метка флажка упоминает только вкладку **Пакет/Публикация SQL** , снятие этого флажка также приведет к отключению развертывания базы данных, настроенного в профиле публикации. Это будет сделано позже, поэтому флажок должен остаться установленным. Вкладка **Пакет/Публикация SQL** используется для устаревшего метода публикации базы данных, который не используется в этих учебниках.
- Раздел **параметров пакета веб-развертывания** не применяется, так как вы используете публикацию одним щелчком в этих руководствах.

Измените раскрывающийся список **Конфигурация** на отладку, чтобы увидеть параметры по умолчанию для отладочных сборок. Значения одинаковы, за исключением случаев, когда **исключены созданные отладочные символы** , которые можно отлаживать при развертывании отладочной сборки.

## <a name="make-sure-that-the-elmah-folder-gets-deployed"></a>Убедитесь, что папка ELMAH развернута

Как было показано в предыдущем учебном курсе, [пакет NuGet для ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) предоставляет функциональные возможности для ведения журнала ошибок и создания отчетов. В приложении университета Contoso для университетов настроено хранение сведений об ошибках в папке с именем *ELMAH*:

![Папка ELMAH](project-properties/_static/image3.png)

Исключением некоторых файлов или папок из развертывания является обычное требование. Другим примером может быть папка, в которую пользователи могут отправлять файлы. Вы не хотите, чтобы файлы журнала или загруженные файлы, созданные в среде разработки, были развернуты в рабочей версии. Если вы развертываете обновление в рабочей среде, вы не хотите, чтобы процесс развертывания удалил файлы, которые существуют в рабочей среде. (В зависимости от настройки параметра развертывания, если файл существует на целевом сайте, но не на исходном сайте при развертывании, веб-развертывание удаляет его из назначения.)

Как было показано ранее в этом учебнике, для параметра **элементы для развертывания** на вкладке **Пакет/Публикация веб-сайта** задаются **только файлы, необходимые для запуска приложения**. В результате файлы журнала, созданные ELMAH в разработке, не будут развернуты, что нужно сделать. (Для развертывания они должны быть добавлены в проект, а свойство **действия построения** должно быть установлено в **содержимое**. Дополнительные сведения см. в разделе **почему не все файлы в папке проекта развертываются?** в разделе [часто задаваемые вопросы о развертывании проекта веб-приложения ASP.NET](https://msdn.microsoft.com/library/ee942158.aspx). Однако веб-развертывание не создаст папку на целевом сайте, если не существует хотя бы один файл для копирования. Таким образом, вы добавите в папку *txt* -файл, который будет использоваться в качестве заполнителя для копирования папки.

В **Обозреватель решений**щелкните правой кнопкой мыши папку *ELMAH* , выберите **Добавить новый элемент**и создайте текстовый файл с именем *PlaceHolder. txt*. Вставьте в него следующий текст: "это файл-заполнитель, который обеспечивает развертывание папки". и сохраните файл. Это все, что нужно сделать, чтобы убедиться, что Visual Studio развертывает этот файл и папку, в которой он находится, так как свойство **действия сборки** *txt* -файлов по умолчанию имеет значение **Content** .

## <a name="summary"></a>Сводка

Теперь все задачи по настройке развертывания завершены. В следующем руководстве вы развернете сайт университета Contoso в тестовой среде и протестируете его.

> [!div class="step-by-step"]
> [Назад](web-config-transformations.md)
> [Вперед](deploying-to-iis.md)
