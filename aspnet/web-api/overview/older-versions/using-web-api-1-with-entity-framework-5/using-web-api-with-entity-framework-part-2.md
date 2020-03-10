---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: Часть 2. Создание моделей предметной области | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c5ed1bdb4b390c94907b14e208231f16ad42d96
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504276"
---
# <a name="part-2-creating-the-domain-models"></a><span data-ttu-id="a91ac-102">Часть 2. Создание моделей предметной области</span><span class="sxs-lookup"><span data-stu-id="a91ac-102">Part 2: Creating the Domain Models</span></span>

<span data-ttu-id="a91ac-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a91ac-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a91ac-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="a91ac-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a><span data-ttu-id="a91ac-105">Добавление моделей</span><span class="sxs-lookup"><span data-stu-id="a91ac-105">Add Models</span></span>

<span data-ttu-id="a91ac-106">Существует три способа подхода Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="a91ac-106">There are three ways to approach Entity Framework:</span></span>

- <span data-ttu-id="a91ac-107">База данных. сначала вы начинаете с базы данных, а Entity Framework создаете код.</span><span class="sxs-lookup"><span data-stu-id="a91ac-107">Database-first: You start with a database, and Entity Framework generates the code.</span></span>
- <span data-ttu-id="a91ac-108">Модель — сначала: начинается с визуальной модели, а Entity Framework создает и базу данных, и код.</span><span class="sxs-lookup"><span data-stu-id="a91ac-108">Model-first: You start with a visual model, and Entity Framework generates both the database and code.</span></span>
- <span data-ttu-id="a91ac-109">Код — сначала: начинается с кода, а Entity Framework создает базу данных.</span><span class="sxs-lookup"><span data-stu-id="a91ac-109">Code-first: You start with code, and Entity Framework generates the database.</span></span>

<span data-ttu-id="a91ac-110">Мы используем подход с использованием кода, поэтому начнем с определения наших объектов домена как POCO (обычные объекты CLR).</span><span class="sxs-lookup"><span data-stu-id="a91ac-110">We are using the code-first approach, so we start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="a91ac-111">При использовании подхода "код — первый" объекты предметной области не требуют дополнительного кода для поддержки уровня базы данных, например транзакций или сохраняемости.</span><span class="sxs-lookup"><span data-stu-id="a91ac-111">With the code-first approach, domain objects don't need any extra code to support the database layer, such as transactions or persistence.</span></span> <span data-ttu-id="a91ac-112">(В частности, им не нужно наследовать от класса [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) .) Заметки к данным по-прежнему можно использовать для управления Entity Framework создания схемы базы данных.</span><span class="sxs-lookup"><span data-stu-id="a91ac-112">(Specifically, they do not need to inherit from the [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) class.) You can still use data annotations to control how Entity Framework creates the database schema.</span></span>

<span data-ttu-id="a91ac-113">Поскольку POCO не содержит дополнительных свойств, описывающих [состояние базы данных](https://msdn.microsoft.com/library/system.data.entitystate.aspx), их можно легко сериализовать в формат JSON или XML.</span><span class="sxs-lookup"><span data-stu-id="a91ac-113">Because POCOs do not carry any extra properties that describe [database state](https://msdn.microsoft.com/library/system.data.entitystate.aspx), they can easily be serialized to JSON or XML.</span></span> <span data-ttu-id="a91ac-114">Однако это не означает, что всегда следует предоставлять модели Entity Framework непосредственно клиентам, как будет показано далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="a91ac-114">However, that does not mean you should always expose your Entity Framework models directly to clients, as we'll see later in the tutorial.</span></span>

<span data-ttu-id="a91ac-115">Мы создадим следующие POCO:</span><span class="sxs-lookup"><span data-stu-id="a91ac-115">We will create the following POCOs:</span></span>

- <span data-ttu-id="a91ac-116">Продукт</span><span class="sxs-lookup"><span data-stu-id="a91ac-116">Product</span></span>
- <span data-ttu-id="a91ac-117">Порядок</span><span class="sxs-lookup"><span data-stu-id="a91ac-117">Order</span></span>
- <span data-ttu-id="a91ac-118">OrderDetail</span><span class="sxs-lookup"><span data-stu-id="a91ac-118">OrderDetail</span></span>

<span data-ttu-id="a91ac-119">Чтобы создать каждый класс, щелкните правой кнопкой мыши папку Models в обозреватель решений.</span><span class="sxs-lookup"><span data-stu-id="a91ac-119">To create each class, right-click the Models folder in Solution Explorer.</span></span> <span data-ttu-id="a91ac-120">В контекстном меню выберите **Добавить** , а затем выберите **класс.**</span><span class="sxs-lookup"><span data-stu-id="a91ac-120">From the context menu, select **Add** and then select **Class.**</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

<span data-ttu-id="a91ac-121">Добавьте класс `Product` со следующей реализацией:</span><span class="sxs-lookup"><span data-stu-id="a91ac-121">Add a `Product` class with the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

<span data-ttu-id="a91ac-122">По соглашению Entity Framework использует свойство `Id` в качестве первичного ключа и сопоставляет его со столбцом идентификаторов в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="a91ac-122">By convention, Entity Framework uses the `Id` property as the primary key and maps it to an identity column in the database table.</span></span> <span data-ttu-id="a91ac-123">При создании нового экземпляра `Product` не устанавливается значение для `Id`, так как база данных создает значение.</span><span class="sxs-lookup"><span data-stu-id="a91ac-123">When you create a new `Product` instance, you won't set a value for `Id`, because the database generates the value.</span></span>

<span data-ttu-id="a91ac-124">Атрибут **скаффолдколумн** указывает ASP.NET MVC пропустить свойство `Id` при создании формы редактора.</span><span class="sxs-lookup"><span data-stu-id="a91ac-124">The **ScaffoldColumn** attribute tells ASP.NET MVC to skip the `Id` property when generating an editor form.</span></span> <span data-ttu-id="a91ac-125">Для проверки модели используется **обязательный** атрибут.</span><span class="sxs-lookup"><span data-stu-id="a91ac-125">The **Required** attribute is used to validate the model.</span></span> <span data-ttu-id="a91ac-126">Он указывает, что свойство `Name` должно быть непустой строкой.</span><span class="sxs-lookup"><span data-stu-id="a91ac-126">It specifies that the `Name` property must be a non-empty string.</span></span>

<span data-ttu-id="a91ac-127">Добавьте класс `Order`:</span><span class="sxs-lookup"><span data-stu-id="a91ac-127">Add the `Order` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

<span data-ttu-id="a91ac-128">Добавьте класс `OrderDetail`:</span><span class="sxs-lookup"><span data-stu-id="a91ac-128">Add the `OrderDetail` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a><span data-ttu-id="a91ac-129">Связи по внешнему ключу</span><span class="sxs-lookup"><span data-stu-id="a91ac-129">Foreign Key Relations</span></span>

<span data-ttu-id="a91ac-130">Заказ содержит много подробных сведений о заказах, и каждая информация о заказе относится к одному продукту.</span><span class="sxs-lookup"><span data-stu-id="a91ac-130">An order contains many order details, and each order detail refers to a single product.</span></span> <span data-ttu-id="a91ac-131">Для представления этих отношений класс `OrderDetail` определяет свойства с именами `OrderId` и `ProductId`.</span><span class="sxs-lookup"><span data-stu-id="a91ac-131">To represent these relations, the `OrderDetail` class defines properties named `OrderId` and `ProductId`.</span></span> <span data-ttu-id="a91ac-132">Entity Framework определит, что эти свойства представляют внешние ключи, и добавит ограничения внешнего ключа в базу данных.</span><span class="sxs-lookup"><span data-stu-id="a91ac-132">Entity Framework will infer that these properties represent foreign keys, and will add foreign-key constraints to the database.</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

<span data-ttu-id="a91ac-133">Классы `Order` и `OrderDetail` также включают свойства навигации, которые содержат ссылки на связанные объекты.</span><span class="sxs-lookup"><span data-stu-id="a91ac-133">The `Order` and `OrderDetail` classes also include "navigation" properties, which contain references to the related objects.</span></span> <span data-ttu-id="a91ac-134">При наличии заказа можно перейти к продуктам в порядке, следуя свойствам навигации.</span><span class="sxs-lookup"><span data-stu-id="a91ac-134">Given an order, you can navigate to the products in the order by following the navigation properties.</span></span>

<span data-ttu-id="a91ac-135">Скомпилируйте проект прямо сейчас.</span><span class="sxs-lookup"><span data-stu-id="a91ac-135">Compile the project now.</span></span> <span data-ttu-id="a91ac-136">Entity Framework использует отражение для обнаружения свойств моделей, поэтому для создания схемы базы данных требуется скомпилированная сборка.</span><span class="sxs-lookup"><span data-stu-id="a91ac-136">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

## <a name="configure-the-media-type-formatters"></a><span data-ttu-id="a91ac-137">Настройка модулей форматирования типа мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a91ac-137">Configure the Media-Type Formatters</span></span>

<span data-ttu-id="a91ac-138">[Модуль форматирования типа мультимедиа](../../formats-and-model-binding/media-formatters.md) — это объект, который сериализует данные при записи веб-API в текст ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="a91ac-138">A [media-type formatter](../../formats-and-model-binding/media-formatters.md) is an object that serializes your data when Web API writes the HTTP response body.</span></span> <span data-ttu-id="a91ac-139">Встроенные модули форматирования поддерживают выходные данные JSON и XML.</span><span class="sxs-lookup"><span data-stu-id="a91ac-139">The built-in formatters support JSON and XML output.</span></span> <span data-ttu-id="a91ac-140">По умолчанию оба этих модуля форматирования сериализуются все объекты по значению.</span><span class="sxs-lookup"><span data-stu-id="a91ac-140">By default, both of these formatters serialize all objects by value.</span></span>

<span data-ttu-id="a91ac-141">Сериализация по значению создает проблему, если граф объекта содержит циклические ссылки.</span><span class="sxs-lookup"><span data-stu-id="a91ac-141">Serialization by value creates a problem if an object graph contains circular references.</span></span> <span data-ttu-id="a91ac-142">Именно в этом случае классы `Order` и `OrderDetail`, так как каждый из них содержит ссылку на другой.</span><span class="sxs-lookup"><span data-stu-id="a91ac-142">That's exactly the case with the `Order` and `OrderDetail` classes, because each holds a reference to the other.</span></span> <span data-ttu-id="a91ac-143">Модуль форматирования будет следовать ссылкам, записывать каждый объект по значению и идти по кругам.</span><span class="sxs-lookup"><span data-stu-id="a91ac-143">The formatter will follow the references, writing each object by value, and go in circles.</span></span> <span data-ttu-id="a91ac-144">Поэтому необходимо изменить поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a91ac-144">Therefore, we need to change the default behavior.</span></span>

<span data-ttu-id="a91ac-145">В обозреватель решений разверните папку приложение\_запуск и откройте файл с именем WebApiConfig.cs.</span><span class="sxs-lookup"><span data-stu-id="a91ac-145">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="a91ac-146">Добавьте в класс `WebApiConfig` приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="a91ac-146">Add the following code to the `WebApiConfig` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

<span data-ttu-id="a91ac-147">Этот код задает модуль форматирования JSON для сохранения ссылок на объекты и полностью удаляет модуль форматирования XML из конвейера.</span><span class="sxs-lookup"><span data-stu-id="a91ac-147">This code sets the JSON formatter to preserve object references, and removes the XML formatter from the pipeline entirely.</span></span> <span data-ttu-id="a91ac-148">(Можно настроить модуль форматирования XML для сохранения ссылок на объекты, но это немного дополнительная работа, и для этого приложения требуется только JSON.</span><span class="sxs-lookup"><span data-stu-id="a91ac-148">(You can configure the XML formatter to preserve object references, but it's a little more work, and we only need JSON for this application.</span></span> <span data-ttu-id="a91ac-149">Дополнительные сведения см. в разделе [Обработка циклических ссылок на объекты](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span><span class="sxs-lookup"><span data-stu-id="a91ac-149">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a91ac-150">[Назад](using-web-api-with-entity-framework-part-1.md)
> [Вперед](using-web-api-with-entity-framework-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="a91ac-150">[Previous](using-web-api-with-entity-framework-part-1.md)
[Next](using-web-api-with-entity-framework-part-3.md)</span></span>
