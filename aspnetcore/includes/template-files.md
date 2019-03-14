---
ms.openlocfilehash: eb2f83504129ae2b19ff5d85a2bc7d90293b43d6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043401"
---
* Startup.cs: [Класс Startup](xref:fundamentals/startup) -класс настраивает конвейер запросов, который обрабатывает все запросы, сделанные в приложение.
* Program.cs: [Программа класс](xref:fundamentals/index) , содержащий это точка входа Main приложения.
* firstapp.csproj: [Файл проекта](/dotnet/articles/core/preview3/tools/csproj) формат файла проекта MSBuild для приложений ASP.NET Core. Содержит ссылки между проектами, ссылки на пакеты NuGet и другие связанные элементы проекта.
* appSettings.JSON / appsettings. Development.JSON: Файл конфигурации параметры базового приложения среды. [См. в разделе конфигурации](xref:fundamentals/configuration/index).
* bower.JSON: Зависимости пакетов bower для проекта.
* .bowerrc: Файл конфигурации bower, который определяет местоположение для установки компонентов, когда Bower загружает ресурсы.
* bundleconfig.JSON: файлы конфигурации для объединения и уменьшения внешние ресурсы JavaScript и CSS.
* Представления: Содержит представления Razor. компоненты, которые формируют пользовательский интерфейс приложения. Как правило, в пользовательском интерфейсе отображаются данные модели.
* Контроллеры: Изначально содержит контроллеры MVC *HomeController.cs*. Контроллеры являются классами, которые обрабатывают запросы браузера.
* wwwroot: Корневой папке веб-приложения.

Дополнительные сведения см. в разделе [шаблон MVC](xref:mvc/overview).
