---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET отклонил доступ к каталогам IIS | Документация Майкрософт
author: rick-anderson
description: В этом техническом документе описывается, что необходимо сделать, если запрос к приложению ASP.NET возвращает ошибку "отказано в доступе к каталогу Директоринаме. Не удалось выполнить...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: a3a53aa88abbe1bcaaea7d691406800c8f9b988b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518574"
---
# <a name="aspnet-denied-access-to-iis-directories"></a><span data-ttu-id="c9b04-104">Платформа ASP.NET отказала в доступе к каталогам IIS ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c9b04-104">ASP.NET Denied Access to IIS Directories</span></span>

> <span data-ttu-id="c9b04-105">В этом техническом документе описывается, что необходимо сделать, если запрос к приложению ASP.NET возвращает ошибку "отказано в доступе к каталогу *директоринаме* .</span><span class="sxs-lookup"><span data-stu-id="c9b04-105">This whitepaper describes what you must do if a request to your ASP.NET application returns the error, "Denied Access to *DirectoryName* directory.</span></span> <span data-ttu-id="c9b04-106">Не удалось начать наблюдение за изменениями каталога. "</span><span class="sxs-lookup"><span data-stu-id="c9b04-106">Failed to start monitoring directory changes."</span></span>
> 
> <span data-ttu-id="c9b04-107">Применяется к ASP.NET 1,0 и ASP.NET 1,1.</span><span class="sxs-lookup"><span data-stu-id="c9b04-107">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="c9b04-108">ASP.NET v1 RTM теперь запускается с использованием учетной записи Windows с меньшим уровнем привилегий, зарегистрированной как учетная запись ASPNET на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c9b04-108">ASP.NET V1 RTM now runs using a less privileged windows account - registered as the "ASPNET" account on a local machine.</span></span>

<span data-ttu-id="c9b04-109">В некоторых заблокированных системах эта учетная запись по умолчанию может не иметь права на чтение каталогов содержимого веб-сайта, корневого каталога приложения или корневого каталога веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="c9b04-109">On some locked down systems, this account may not by default have read security access to a website's content directories, the application root directory, or the web site root directory.</span></span> <span data-ttu-id="c9b04-110">В этом случае при запросе страниц из заданного веб-приложения будет получена следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="c9b04-110">In this case you will receive the following error when requesting pages from a given web application:</span></span>

![](denied-access-to-iis-directories/_static/image1.jpg)

<span data-ttu-id="c9b04-111">Чтобы устранить эту проблему, необходимо изменить разрешения безопасности для соответствующих каталогов.</span><span class="sxs-lookup"><span data-stu-id="c9b04-111">To fix this you will need to change the security permissions on the appropriate directories.</span></span>

<span data-ttu-id="c9b04-112">В частности, для ASP.NET требуется доступ на чтение, выполнение и перечисление учетной записи ASPNET для корневого узла веб-сайта (например, c:\Inetpub\wwwroot или любого альтернативного каталога сайтов, который мог быть настроен в службах IIS), каталога содержимого и корневого каталога приложения. для отслеживания изменений в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c9b04-112">Specifically, ASP.NET requires read, execute, and list access for the ASPNET account for the web site root (for example: c:\inetpub\wwwroot or any alternative site directory you may have configured in IIS), the content directory and the application root directory in order to monitor for configuration file changes.</span></span> <span data-ttu-id="c9b04-113">Корень приложения соответствует пути к папке, связанному с виртуальным каталогом приложения, в средстве администрирования IIS (inetmgr).</span><span class="sxs-lookup"><span data-stu-id="c9b04-113">The application root corresponds to the folder path associated with the application virtual directory in the IIS Administration tool (inetmgr).</span></span>

<span data-ttu-id="c9b04-114">Например, рассмотрим следующую иерархию приложений в папке wwwroot.</span><span class="sxs-lookup"><span data-stu-id="c9b04-114">For example, consider the following application hierarchy under the wwwroot folder.</span></span>

`C:\inetpub\wwwroot\myapp\default.aspx`

<span data-ttu-id="c9b04-115">В этом примере учетной записи ASPNET требуются разрешения на чтение, определенные выше, для содержимого в каталоге MyApp и wwwroot.</span><span class="sxs-lookup"><span data-stu-id="c9b04-115">For this example, the ASPNET account needs the read permissions defined above for content in both the myapp and the wwwroot directory.</span></span> <span data-ttu-id="c9b04-116">Один наследуемый список ACL для корневой папки можно также использовать для обоих каталогов, если они являются вложенными.</span><span class="sxs-lookup"><span data-stu-id="c9b04-116">A single inherited ACL on the root folder can also be optionally used for both directories if they're nested.</span></span>

<span data-ttu-id="c9b04-117">Чтобы добавить разрешения в каталог, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c9b04-117">To add permissions to a directory, perform the following steps:</span></span>

- <span data-ttu-id="c9b04-118">С помощью проводника Windows перейдите в каталог.</span><span class="sxs-lookup"><span data-stu-id="c9b04-118">Using the Windows explorer, navigate to the directory</span></span>
- <span data-ttu-id="c9b04-119">Щелкните правой кнопкой мыши папку каталога и выберите пункт "Свойства".</span><span class="sxs-lookup"><span data-stu-id="c9b04-119">Right click on the directory folder and choose "Properties"</span></span>
- <span data-ttu-id="c9b04-120">Перейдите на вкладку "безопасность" в диалоговом окне свойств.</span><span class="sxs-lookup"><span data-stu-id="c9b04-120">Navigate to the "Security" tab on the property dialog</span></span>
- <span data-ttu-id="c9b04-121">Нажмите кнопку "Добавить" и введите имя компьютера, а затем имя учетной записи ASPNET.</span><span class="sxs-lookup"><span data-stu-id="c9b04-121">Click the "Add" button and enter the machine name followed by the ASPNET account name.</span></span> <span data-ttu-id="c9b04-122">Например, на компьютере с именем "WebDev" необходимо ввести Вебдев\аспнет и нажать кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="c9b04-122">For example, on a machine named "webdev", you would enter webdev\ASPNET and hit "OK".</span></span>
- <span data-ttu-id="c9b04-123">Убедитесь, что в учетной записи ASPNET установлены флажки "чтение &amp; выполнение", "список содержимого папки" и "чтение".</span><span class="sxs-lookup"><span data-stu-id="c9b04-123">Ensure that the ASPNET account has the "Read &amp; Execute", "List Folder Contents", and "Read" checkboxes checked.</span></span>
- <span data-ttu-id="c9b04-124">Нажмите кнопку ОК, чтобы закрыть диалоговое окно и сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="c9b04-124">Hit OK to dismiss the dialog and save the changes.</span></span>

![](denied-access-to-iis-directories/_static/image2.jpg)

<span data-ttu-id="c9b04-125">При необходимости эти изменения можно автоматизировать с помощью сценариев или средства "cacls. exe", поставляемого с Windows.</span><span class="sxs-lookup"><span data-stu-id="c9b04-125">If desired, these changes can be automated using scripts or the "cacls.exe" tool that ships with Windows.</span></span> <span data-ttu-id="c9b04-126">Дополнительные сведения об учетной записи ASPNET см. в [документе с вопросами и](https://go.microsoft.com/fwlink/?LinkId=5828)ответами.</span><span class="sxs-lookup"><span data-stu-id="c9b04-126">For more information on the ASPNET account, please see the [FAQ document](https://go.microsoft.com/fwlink/?LinkId=5828).</span></span>

<span data-ttu-id="c9b04-127">Если конкретное веб-приложение использует разрешения на запись или изменение для конкретной папки или файла, это можно сделать, выполнив ту же процедуру и установив флажки "Write" и (или) "Modify" (изменить).</span><span class="sxs-lookup"><span data-stu-id="c9b04-127">If a given web application relies on having write or modify permissions to a particular folder or file, this can be granted by following the same procedure and checking the "Write" and/or "Modify" checkboxes.</span></span>

<span data-ttu-id="c9b04-128">На компьютерах, разрешающих всем пользователям или группам пользователей доступ на чтение к этим каталогам (что является конфигурацией по умолчанию), проблемы не будут обнаружены, и указанные выше действия не потребуются.</span><span class="sxs-lookup"><span data-stu-id="c9b04-128">On machines that allow Everyone or the Users group read access to these directories (which is the default configuration), no issues will be encountered and the above steps will not be required.</span></span>
