---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: Развертывание паролей и других конфиденциальных данных в ASP.NET и службе приложений Azure — ASP.NET 4. x
author: Rick-Anderson
description: В этом руководстве показано, как код может безопасно хранить и получать доступ к защищенным сведениям. Самый важный момент — не хранить пароли или другие нда...
ms.author: riande
ms.date: 05/21/2015
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 8356a90611f791779cc4ff4730038d82cd76242f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457054"
---
# <a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a>Рекомендации по развертыванию паролей и других конфиденциальных данных в ASP.NET и службу приложений Azure

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом руководстве показано, как код может безопасно хранить и получать доступ к защищенным сведениям. Самый важный момент — не хранить пароли или другие конфиденциальные данные в исходном коде, и не следует использовать рабочие секреты в режиме разработки и тестирования.
> 
> Пример кода — это простое консольное приложение веб-задания и приложение ASP.NET MVC, которым требуется доступ к паролю строки подключения к базе данных, защищенным ключам Twilio, Google и SendGrid.
> 
> Также упомянуты локальные параметры и PHP.

- [Работа с паролями в среде разработки](#pwd)
- [Работа со строками подключения в среде разработки](#con)
- [Консольные приложения веб-заданий](#wj)
- [Развертывание секретов в Azure](#da)
- [Примечания для локальных и PHP](#not)
- [Дополнительные ресурсы](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a>Работа с паролями в среде разработки

Учебники часто демонстрируют конфиденциальные данные в исходном коде, надеюсь, что не следует хранить конфиденциальные данные в исходном коде. Например, в руководстве мое [приложение ASP.NET MVC 5 с SMS и электронной почтой 2FA](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) показано следующее в файле *Web. config* :

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

Файл *Web. config* является исходным кодом, поэтому эти секреты никогда не должны храниться в этом файле. К счастью, элемент `<appSettings>` имеет атрибут `file`, который позволяет указать внешний файл, содержащий конфиденциальные параметры конфигурации приложения. Все секреты можно переместить во внешний файл, если внешний файл не возвращен в исходное дерево. Например, в следующей разметке файл *аппсеттингссекретс. config* содержит все секреты приложения:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

Разметка во внешнем файле (*аппсеттингссекретс. config* в этом примере) — это та же разметка, которая находится в файле *Web. config* :

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

Среда выполнения ASP.NET объединяет содержимое внешнего файла с разметкой в &lt;appSettings&gt; element. Если указанный файл не удается найти, среда выполнения игнорирует атрибут файла.

> [!WARNING]
> Безопасность — не добавляйте файл *секреты. config* в проект или верните его в систему управления версиями. По умолчанию Visual Studio устанавливает для `Build Action` значение `Content`, что означает, что файл развертывается. Дополнительные сведения см. в разделе [почему не все файлы в папке проекта развертываются?](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment) Хотя можно использовать любое расширение для файла *секреты. config* , лучше не выполнять файл конфигурации, так как *он не*обслуживается службами IIS. Кроме того, обратите внимание, что файл *аппсеттингссекретс. config* — это два уровня каталога выше, чем в файле *Web. config* , поэтому он полностью выходит за пределы каталога решения. Перемещая файл из каталога решения, &quot;Git Add \*&quot; не добавит его в репозиторий.

<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a>Работа со строками подключения в среде разработки

Visual Studio создает новые проекты ASP.NET, использующие [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx). LocalDB был создан специально для среды разработки. Он не требует пароля, поэтому вам не нужно ничего делать, чтобы предотвратить возврат секретов в исходный код. Некоторые группы разработчиков используют полные версии SQL Server (или другой СУБД), для которых требуется пароль.

Можно использовать атрибут `configSource`, чтобы заменить всю разметку `<connectionStrings>`. В отличие от атрибута `<appSettings>` `file`, который выполняет слияние разметки, атрибут `configSource` заменяет разметку. В следующей разметке показан атрибут `configSource` в файле *Web. config* :

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> Если вы используете атрибут `configSource`, как показано выше, чтобы переместить строки подключения во внешний файл и создать новый веб-сайт с помощью Visual Studio, он не сможет обнаружить, что вы используете базу данных, и вы не сможете настроить базу данных при публикации в Azure из Visual Studio. Если вы используете атрибут `configSource`, для создания и развертывания веб-сайта и базы данных можно использовать PowerShell. также можно создать веб-сайт и базу данных на портале перед публикацией. Сценарий [Нев-азуревебситевисдб. ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) создаст новый веб-сайт и базу данных.

> [!WARNING]
> Безопасность. в отличие от файла *аппсеттингссекретс. config* , файл строк внешнего подключения должен находиться в том же каталоге, что и корневой файл *Web. config* , поэтому необходимо принять меры предосторожности, чтобы не выполнять возврат в исходном репозитории.

> [!NOTE]
> **Предупреждение безопасности для секретного файла:** Рекомендуется не использовать рабочие секреты в тестировании и разработке. Использование рабочих паролей в ходе тестирования или разработки приводит к утечке этих секретов.

<a id="wj"></a>
## <a name="webjobs-console-apps"></a>Консольные приложения веб-заданий

Файл *app. config* , используемый консольным приложением, не поддерживает относительные пути, но поддерживает абсолютные пути. Можно использовать абсолютный путь для перемещения секретов из каталога проекта. В следующей разметке показаны секреты в файле *к:\секретс\аппсеттингссекретс.конфиг* , а не конфиденциальные данные в файле *app. config* .

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a>Развертывание секретов в Azure

При развертывании веб-приложения в Azure файл *аппсеттингссекретс. config* не будет развернут (именно то, что вам нужно). Вы можете открыть [портал управления Azure](https://azure.microsoft.com/services/management-portal/) и настроить их вручную. для этого выполните следующие действия.

1. Перейдите в [https://portal.azure.com](https://portal.azure.com)и выполните вход с использованием учетных данных Azure.
2. Щелкните **обзор &gt; веб-приложения**, а затем щелкните имя своего веб-приложения.
3. Щелкните **все параметры &gt; параметры приложения**.

**Параметры приложения** и значения **строки подключения** переопределяют те же параметры в файле *Web. config* . В нашем примере мы не развернули эти параметры в Azure, но если эти ключи были в файле *Web. config* , то параметры, показанные на портале, будут иметь приоритет.

Рекомендуется следовать [рабочему процессу DevOps](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md) и использовать [Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (или другую платформу, например [Chef](http://www.opscode.com/chef/) или [Puppet](http://puppetlabs.com/puppet/what-is-puppet)) для автоматизации установки этих значений в Azure. Следующий сценарий PowerShell использует [Export-CliXml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk) для экспорта зашифрованных секретов на диск:

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

В приведенном выше сценарии "имя" — это имя секретного ключа, например "&quot;FB\_AppSecret&quot; или" Твиттерсекрет ". Файл с учетными данными, созданный скриптом, можно просмотреть в браузере. Приведенный ниже фрагмент кода проверяет каждый из файлов учетных данных и задает секреты для именованного веб-приложения.

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> Безопасность — не включайте пароли или другие секреты в сценарий PowerShell. это не позволит использовать сценарий PowerShell для развертывания конфиденциальных данных. Командлет [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) предоставляет безопасный механизм для получения пароля. Использование запроса пользовательского интерфейса может препятствовать утечке пароля.

### <a name="deploying-db-connection-strings"></a>Развертывание строк подключения к базе данных

Строки подключения к базе данных обрабатываются аналогично параметрам приложения. При развертывании веб-приложения из Visual Studio строка подключения будет настроена для вас. Это можно проверить на портале. Для задания строки подключения рекомендуется использовать PowerShell. Пример сценария PowerShell, который создает веб-сайт и базу данных и задает строку подключения на веб-сайте, скачайте [Нев-азуревебситевисдб. ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) из [библиотеки скриптов Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure).

<a id="not"></a>
## <a name="notes-for-php"></a>Примечания для PHP

Так как пары "ключ-значение" для **параметров приложения** и **строк подключения** хранятся в переменных среды в службе приложений Azure, разработчики, использующие любые платформы веб-приложений (например, PHP), могут легко извлекать эти значения. См. раздел Стефан Шаков (Web Sites ( [веб-сайты Windows Azure): как строки приложения и строки подключения работают](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) с записью блога, в которой ПОКАЗАН фрагмент PHP для чтения параметров приложения и строк подключения.

## <a name="notes-for-on-premises-servers"></a>Примечания для локальных серверов

При развертывании на локальных веб-серверах можно защитить секреты путем [шифрования разделов конфигурации файлов конфигурации](https://msdn.microsoft.com/library/ff647398.aspx). В качестве альтернативы можно использовать тот же подход, который рекомендуется для веб-сайтов Azure: не заключить параметры разработки в файлах конфигурации и использовать значения переменных среды для рабочих параметров. Однако в этом случае необходимо написать код приложения для функций, автоматически выполняемых на веб-сайтах Azure: извлечь параметры из переменных среды и использовать эти значения вместо параметров файла конфигурации или использовать параметры файла конфигурации, если переменные среды не найдены.

<a id="addRes"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

Пример сценария PowerShell, который создает веб-приложение и базу данных, задает строку подключения + параметры приложения, скачайте [Нев-азуревебситевисдб. ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) из [библиотеки скриптов Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure). 

См. раздел Стефан Шаков (Web Sites ( [веб-сайты Windows Azure): как работают строки приложения и строки подключения.](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)

Для ознакомления — Барри Доррансом ( [@blowdart](https://twitter.com/blowdart) ) и Карлос Фарре.
