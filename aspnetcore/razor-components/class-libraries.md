---
title: Библиотеки классов Razor компонентов
author: guardrex
description: Узнайте, как компоненты могут быть включены в приложениях Razor компоненты из библиотеки внешнего компонента.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/09/2019
uid: razor-components/class-libraries
ms.openlocfilehash: 0e644627178bae2b8880760335860b3e0ebef156
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037411"
---
# <a name="razor-components-class-libraries"></a>Библиотеки классов Razor компонентов

По [Тиммса Simon](https://github.com/stimms)

> [!NOTE]
> SDK для .NET Core 3.0 Предварительная версия 2 не содержит шаблон проекта для библиотеки классов Razor компонента, но мы планируем добавить шаблон в следующей предварительной версии. В пока можно использовать шаблон библиотеки классов компонентов Blazor, описанных в этом разделе.

Компоненты в библиотек компонентов могут совместно использоваться проектами. Компоненты можно включить из:

* Другой проект в решении.
* Пакет NuGet.
* Библиотека .NET, на которую указывает ссылка.

Так же, как компоненты регулярные типы .NET, компонент библиотеки — обычный сборок .NET.

Чтобы создать новую библиотеку компонента, используйте `blazorlib` шаблон с [команды dotnet new](/dotnet/core/tools/dotnet-new) команды. Шаблон является частью шаблоны, установленные при [Настройка компонентов Razor](xref:razor-components/get-started).

```console
dotnet new blazorlib -o MyComponentLib1
```

Чтобы добавить в библиотеку в существующий проект, используйте [dotnet sln](/dotnet/core/tools/dotnet-sln) команды:

```console
dotnet sln add .\MyComponentLib1
```

Библиотеки компонентов может содержать статические файлы, такие как изображения, JavaScript и таблицы стилей. Во время сборки, статические файлы внедряются в сборку файл (*.dll*), позволяющий потребления компонентов не нужно беспокоиться о том, как включить их ресурсы. Все файлы, включенные в `content` directory помечаются как внедренный ресурс. 

## <a name="consume-a-library-component"></a>Использует компонент библиотеки

Чтобы использовать компоненты, определенные в библиотеке в другом проекте [ @addTagHelper ](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label) необходимо использовать директиву. Отдельные компоненты могут быть добавлены по имени. Например, следующая директива добавляет `Component1` из `MyComponentLib1`:

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1
```

Директивы общие выглядит следующим образом:

```cshtml
@addTagHelper <namespaced component name>, <assembly name>
```

Тем не менее он являются общими для включения всех компонентов из сборки с помощью подстановочного знака.

```cshtml
@addTagHelper *, MyComponentLib1
```

`@addTagHelper` Директивы может быть включено в *_ViewImport.cshtml* для этих компонентов доступны для всего проекта или примененные к одной странице или набору страниц в папке. С помощью `@addTagHelper` директив на месте, компоненты библиотеки компонентов могут быть использованы как если бы они были в той же сборке, что и приложение. 

## <a name="build-pack-and-ship-to-nuget"></a>Сборки, пакет и поставки для NuGet

Так как компонент библиотеки — стандартные библиотеки .NET, упаковки и их отправки в NuGet в качестве примеров, ничем не отличается от упаковки и доставки любую библиотеку в NuGet. Упаковка выполняется с помощью [dotnet pack](/dotnet/core/tools/dotnet-pack) команды:

```console
dotnet pack
```

Отправка пакета NuGet с помощью [публикации dotnet nuget](/dotnet/core/tools/dotnet-nuget-push) команды:

```console
dotnet nuget publish
```

Все включенные статические ресурсы включаются в пакет NuGet. Потребители библиотеки автоматически получать скриптов и таблиц стилей, чтобы потребители не требуется вручную установить ресурсы.
