---
title: "Прямая связь клиента микрослужбу и шаблон шлюза API"
description: "Архитектура Микрослужбами .NET для приложений .NET в контейнерах | Прямая связь клиента микрослужбу и шаблон шлюза API"
keywords: "Docker, Микрослужбами, ASP.NET, контейнера, API шлюза"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 10/18/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: c8227ec47888c7cf361f34c4c85a09c0666f886e
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2017
---
# <a name="direct-client-to-microservice-communication-versus-the-api-gateway-pattern"></a><span data-ttu-id="a18b7-104">Прямая связь клиента микрослужбу и шаблон шлюза API</span><span class="sxs-lookup"><span data-stu-id="a18b7-104">Direct client-to-microservice communication versus the API Gateway pattern</span></span>

<span data-ttu-id="a18b7-105">В архитектуре микрослужбами каждого микрослужбу предоставляет набор (обычно) fine‑grained конечных точек.</span><span class="sxs-lookup"><span data-stu-id="a18b7-105">In a microservices architecture, each microservice exposes a set of (typically) fine‑grained endpoints.</span></span> <span data-ttu-id="a18b7-106">Этот факт может повлиять на взаимодействие client‑to‑microservice, как описано в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="a18b7-106">This fact can impact the client‑to‑microservice communication, as explained in this section.</span></span>

## <a name="direct-client-to-microservice-communication"></a><span data-ttu-id="a18b7-107">Прямая связь клиента микрослужбу</span><span class="sxs-lookup"><span data-stu-id="a18b7-107">Direct client-to-microservice communication</span></span>

<span data-ttu-id="a18b7-108">Возможные подходом является использование архитектуры прямой обмен данными клиента микрослужбы.</span><span class="sxs-lookup"><span data-stu-id="a18b7-108">A possible approach is to use a direct client-to-microservice communication architecture.</span></span> <span data-ttu-id="a18b7-109">При таком подходе клиентские приложения могут выполнять запросы непосредственно к некоторым микрослужбами, как показано на рисунке 4-12.</span><span class="sxs-lookup"><span data-stu-id="a18b7-109">In this approach, a client app can make requests directly to some of the microservices, as shown in Figure 4-12.</span></span>

![](./media/image12.png)

<span data-ttu-id="a18b7-110">**Рис. 4-12**.</span><span class="sxs-lookup"><span data-stu-id="a18b7-110">**Figure 4-12**.</span></span> <span data-ttu-id="a18b7-111">С помощью прямой обмен данными клиента микрослужбу архитектуры</span><span class="sxs-lookup"><span data-stu-id="a18b7-111">Using a direct client-to-microservice communication architecture</span></span>

<span data-ttu-id="a18b7-112">При использовании этого подхода.</span><span class="sxs-lookup"><span data-stu-id="a18b7-112">In this approach.</span></span> <span data-ttu-id="a18b7-113">Каждый микрослужбу имеет общедоступную конечную точку, иногда с разных портов TCP для каждого микрослужбы.</span><span class="sxs-lookup"><span data-stu-id="a18b7-113">each microservice has a public endpoint, sometimes with a different TCP port for each microservice.</span></span> <span data-ttu-id="a18b7-114">Пример URL-адреса для конкретной службы может быть следующий URL-адрес в Azure.</span><span class="sxs-lookup"><span data-stu-id="a18b7-114">An example of a URL for a particular service could be the following URL in Azure:</span></span>

<span data-ttu-id="a18b7-115"><http://eshoponcontainers.westus.cloudapp.Azure.com:88 /></span><span class="sxs-lookup"><span data-stu-id="a18b7-115"><http://eshoponcontainers.westus.cloudapp.azure.com:88/></span></span>

<span data-ttu-id="a18b7-116">В рабочей среде, в зависимости от кластера, что URL-адреса будут сопоставлены с подсистемой балансировки нагрузки в кластере, который в свою очередь распределяет запросы по микрослужбами.</span><span class="sxs-lookup"><span data-stu-id="a18b7-116">In a production environment based on a cluster, that URL would map to the load balancer used in the cluster, which in turn distributes the requests across the microservices.</span></span> <span data-ttu-id="a18b7-117">В производственной среде, можно создать контроллер доставки приложений (ADC) как [шлюза приложения Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) между вашей микрослужбами и Интернетом.</span><span class="sxs-lookup"><span data-stu-id="a18b7-117">In production environments, you could have an Application Delivery Controller (ADC) like [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) between your microservices and the Internet.</span></span> <span data-ttu-id="a18b7-118">Это действует как прозрачный уровня, которые не только выполняет балансировку нагрузки, но также обеспечивает защиту служб, предлагая завершение запросов SSL.</span><span class="sxs-lookup"><span data-stu-id="a18b7-118">This acts as a transparent tier that not only performs load balancing, but secures your services by offering SSL termination.</span></span> <span data-ttu-id="a18b7-119">Это повышает нагрузку на узлах за счет разгрузки SSL процессор завершения других маршрутизации обязанностей и для шлюза приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="a18b7-119">This improves the load of your hosts by offloading CPU-intensive SSL termination and other routing duties to the Azure Application Gateway.</span></span> <span data-ttu-id="a18b7-120">В любом случае подсистемы балансировки нагрузки и Соединитель Active Directory являются прозрачными из приложения логической архитектуры точки зрения.</span><span class="sxs-lookup"><span data-stu-id="a18b7-120">In any case, a load balancer and ADC are transparent from a logical application architecture point of view.</span></span>

<span data-ttu-id="a18b7-121">Архитектура прямого взаимодействия клиента микрослужбу может быть достаточно для небольших микрослужбу-приложения, особенно в том случае, если клиентское приложение находится в серверном веб-приложения, как приложение ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a18b7-121">A direct client-to-microservice communication architecture could be good enough for a small microservice-based application, especially if the client app is a server-side web application like an ASP.NET MVC app.</span></span> <span data-ttu-id="a18b7-122">Однако при построении больших и сложных микрослужбу приложений на основе (например, при обработке десятки микрослужбу типов), и особенно в том случае, если клиентские приложения являются удаленного мобильных приложений или SPA веб-приложений, этот подход сталкивается несколько проблем.</span><span class="sxs-lookup"><span data-stu-id="a18b7-122">However, when you build large and complex microservice-based applications (for example, when handling dozens of microservice types), and especially when the client apps are remote mobile apps or SPA web applications, that approach faces a few issues.</span></span>

<span data-ttu-id="a18b7-123">При разработке большого приложения, основанного на микрослужбами, ответьте на следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="a18b7-123">Consider the following questions when developing a large application based on microservices:</span></span>

-   <span data-ttu-id="a18b7-124">*Как клиентские приложения свести к минимуму число запросов к серверной части и уменьшить частый обмен данными на нескольких микрослужбами?*</span><span class="sxs-lookup"><span data-stu-id="a18b7-124">*How can client apps minimize the number of requests to the backend and reduce chatty communication to multiple microservices?*</span></span>

<span data-ttu-id="a18b7-125">Взаимодействие с несколькими микрослужбами для создания одного пользовательского интерфейса экрана увеличивает количество обращений через Интернет.</span><span class="sxs-lookup"><span data-stu-id="a18b7-125">Interacting with multiple microservices to build a single UI screen increases the number of roundtrips across the Internet.</span></span> <span data-ttu-id="a18b7-126">Это увеличивает задержку и сложности на стороне пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a18b7-126">This increases latency and complexity on the UI side.</span></span> <span data-ttu-id="a18b7-127">В идеальном случае ответы эффективно рассчитано на стороне сервера — это сокращает задержки, так как несколько фрагментов данных вернитесь в параллельном режиме и пользовательский Интерфейс можно показать данные, как только будет готов к работе.</span><span class="sxs-lookup"><span data-stu-id="a18b7-127">Ideally, responses should be efficiently aggregated in the server side—this reduces latency, since multiple pieces of data come back in parallel and some UI can show data as soon as it is ready.</span></span>

-   <span data-ttu-id="a18b7-128">*Порядок обработки перекрестными проблемы, такие как авторизация, преобразования данных и диспетчеризации динамический запрос?*</span><span class="sxs-lookup"><span data-stu-id="a18b7-128">*How can you handle cross-cutting concerns such as authorization, data transformations, and dynamic request dispatching?*</span></span>

<span data-ttu-id="a18b7-129">Реализация перекрестными проблемы безопасности и как безопасности и авторизации на каждом микрослужбу может потребовать значительных разработки приложения.</span><span class="sxs-lookup"><span data-stu-id="a18b7-129">Implementing security and cross-cutting concerns like security and authorization on every microservice can require significant development effort.</span></span> <span data-ttu-id="a18b7-130">Возможный подход является эти службы в узел Docker или внутри кластера, чтобы предотвратить прямой доступ к ним извне и реализовать их беспокойство перекрестными в централизованном расположении, например шлюз API.</span><span class="sxs-lookup"><span data-stu-id="a18b7-130">A possible approach is to have those services within the Docker host or internal cluster, in order to restrict direct access to them from the outside, and to implement those cross-cutting concerns in a centralized place, like an API Gateway.</span></span>

-   <span data-ttu-id="a18b7-131">*Как клиентские приложения могут взаимодействовать со службами, которые используют протоколы Интернета понятное?*</span><span class="sxs-lookup"><span data-stu-id="a18b7-131">*How can client apps communicate with services that use non-Internet-friendly protocols?*</span></span>

<span data-ttu-id="a18b7-132">Протоколы, используемые на стороне сервера (например, AMQP или двоичные протоколы) обычно не поддерживается в клиентских приложениях.</span><span class="sxs-lookup"><span data-stu-id="a18b7-132">Protocols used on the server side (like AMQP or binary protocols) are usually not supported in client apps.</span></span> <span data-ttu-id="a18b7-133">Таким образом запросы требуется выполнить через протоколы, например HTTP или HTTPS, а затем преобразуется в другие протоколы.</span><span class="sxs-lookup"><span data-stu-id="a18b7-133">Therefore, requests must be performed through protocols like HTTP/HTTPS and translated to the other protocols afterwards.</span></span> <span data-ttu-id="a18b7-134">Объект *в середине* подход может помочь в этой ситуации.</span><span class="sxs-lookup"><span data-stu-id="a18b7-134">A *man-in-the-middle* approach can help in this situation.</span></span>

-   <span data-ttu-id="a18b7-135">*Как можно формировать оболочки, особенно сделанные для мобильных приложений*</span><span class="sxs-lookup"><span data-stu-id="a18b7-135">*How can you shape a façade especially made for mobile apps?*</span></span>

<span data-ttu-id="a18b7-136">API-Интерфейс несколько микрослужбами не следует также спроектировать для удовлетворения потребностей различных клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="a18b7-136">The API of multiple microservices might not be well designed for the needs of different client applications.</span></span> <span data-ttu-id="a18b7-137">Например потребностей мобильного приложения может отличаться от потребности веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a18b7-137">For instance, the needs of a mobile app might be different than the needs of a web app.</span></span> <span data-ttu-id="a18b7-138">Для мобильных приложений может потребоваться еще больше оптимизировать, чтобы данные ответов может быть более эффективным.</span><span class="sxs-lookup"><span data-stu-id="a18b7-138">For mobile apps, you might need to optimize even further so that data responses can be more efficient.</span></span> <span data-ttu-id="a18b7-139">Это может сделать, статистическая обработка данных из нескольких микрослужбами и возвращение одного набора данных и иногда решать любые данные в ответ, который не требуется, мобильное приложение.</span><span class="sxs-lookup"><span data-stu-id="a18b7-139">You might do this by aggregating data from multiple microservices and returning a single set of data, and sometimes eliminating any data in the response that is not needed by the mobile app.</span></span> <span data-ttu-id="a18b7-140">И, конечно, вы сжатие этих данных.</span><span class="sxs-lookup"><span data-stu-id="a18b7-140">And, of course, you might compress that data.</span></span> <span data-ttu-id="a18b7-141">Опять же оболочка или API-Интерфейс между микрослужбами и мобильные приложения может оказаться удобным для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="a18b7-141">Again, a façade or API in between the mobile app and the microservices can be convenient for this scenario.</span></span>

## <a name="using-an-api-gateway"></a><span data-ttu-id="a18b7-142">С помощью API-интерфейса шлюза</span><span class="sxs-lookup"><span data-stu-id="a18b7-142">Using an API Gateway</span></span>

<span data-ttu-id="a18b7-143">При проектировании и создание больших или сложных микрослужбу-приложениям с несколько клиентских приложений, может быть хорошим подходом, которые следует учитывать [шлюза API](http://microservices.io/patterns/apigateway.html).</span><span class="sxs-lookup"><span data-stu-id="a18b7-143">When you design and build large or complex microservice-based applications with multiple client apps, a good approach to consider can be an [API Gateway](http://microservices.io/patterns/apigateway.html).</span></span> <span data-ttu-id="a18b7-144">Это служба, предоставляющая единую точку входа для определенных групп микрослужбами.</span><span class="sxs-lookup"><span data-stu-id="a18b7-144">This is a service that provides a single entry point for certain groups of microservices.</span></span> <span data-ttu-id="a18b7-145">Это похоже на [шаблон Facade](https://en.wikipedia.org/wiki/Facade_pattern) от object‑oriented проектирования, но в этом случае он является частью распределенных систем.</span><span class="sxs-lookup"><span data-stu-id="a18b7-145">It is similar to the [Facade pattern](https://en.wikipedia.org/wiki/Facade_pattern) from object‑oriented design, but in this case, it is part of a distributed system.</span></span> <span data-ttu-id="a18b7-146">Шаблон шлюза API также иногда называют «внутренняя для внешнего интерфейса» [(BFF)](http://samnewman.io/patterns/architectural/bff/) так, как построить при думать о потребностях клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="a18b7-146">The API Gateway pattern is also sometimes known as the “backend for frontend” [(BFF)](http://samnewman.io/patterns/architectural/bff/) because you build it while thinking about the needs of the client app.</span></span>

<span data-ttu-id="a18b7-147">На рисунке 4-13 показано, как пользовательские API шлюз может быть загружено в архитектуру на основе микрослужбу.</span><span class="sxs-lookup"><span data-stu-id="a18b7-147">Figure 4-13 shows how a custom API Gateway can fit into a microservice-based architecture.</span></span>
<span data-ttu-id="a18b7-148">Важно обратить внимание, что в эту схему, используемого одну пользовательскую службу шлюза API с несколькими и различных клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="a18b7-148">It is important to highlight that in that diagram, you would be using a single custom API Gateway service facing multiple and different client apps.</span></span> <span data-ttu-id="a18b7-149">На многих различных требований из клиентских приложений, факт может быть важные риска, так как службы шлюза API будет растет и развития основе.</span><span class="sxs-lookup"><span data-stu-id="a18b7-149">That fact can be an important risk because your API Gateway service will be growing and evolving based on many different requirements from the client apps.</span></span> <span data-ttu-id="a18b7-150">Со временем будет перегруженными из-за этих различных потребностей и эффективно может быть довольно аналогично монолитные приложения или объединенный службы.</span><span class="sxs-lookup"><span data-stu-id="a18b7-150">Eventually, it will be bloated because of those different needs and effectively it could be pretty similar to a monolithic application or monolithic service.</span></span> <span data-ttu-id="a18b7-151">Именно поэтому сильно рекомендуется разбить шлюза API в несколько служб или несколько небольших API шлюзов, по одной на каждый тип форм фактор для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="a18b7-151">That is why it is very much recommended to split the API Gateway in multiple services or multiple smaller API Gateways, one per form-factor type, for instance.</span></span>

![](./media/image13.png)

<span data-ttu-id="a18b7-152">**Рис. 4-13**.</span><span class="sxs-lookup"><span data-stu-id="a18b7-152">**Figure 4-13**.</span></span> <span data-ttu-id="a18b7-153">С помощью API-интерфейса шлюза реализован как пользовательскую службу веб-API</span><span class="sxs-lookup"><span data-stu-id="a18b7-153">Using an API Gateway implemented as a custom Web API service</span></span>

<span data-ttu-id="a18b7-154">В этом примере API шлюза будет реализован в виде пользовательских веб-API службы, запущенной как контейнер.</span><span class="sxs-lookup"><span data-stu-id="a18b7-154">In this example, the API Gateway would be implemented as a custom Web API service running as a container.</span></span>

<span data-ttu-id="a18b7-155">Как уже упоминалось, необходимо реализовать несколько шлюзов API, чтобы у вас есть другой оболочкой для удовлетворения потребностей каждого клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="a18b7-155">As mentioned, you should implement several API Gateways so that you can have a different façade for the needs of each client app.</span></span> <span data-ttu-id="a18b7-156">Каждый шлюз API может предоставить другой API, предназначенная для каждого клиентского приложения, возможно даже, на основе форм-фактор клиента путем реализации какие расположенных под вызывает несколько внутренних микрослужбами кода отдельный адаптер.</span><span class="sxs-lookup"><span data-stu-id="a18b7-156">Each API Gateway can provide a different API tailored for each client app, possibly even based on the client form factor by implementing specific adapter code which underneath calls multiple internal microservices.</span></span>

<span data-ttu-id="a18b7-157">Поскольку пользовательские API шлюза обычно агрегации данных, необходимо Будьте внимательны с ним.</span><span class="sxs-lookup"><span data-stu-id="a18b7-157">Since a custom API Gateway is usually a data aggregator, you need to be careful with it.</span></span> <span data-ttu-id="a18b7-158">Обычно не рекомендуется иметь один шлюз API статистическая обработка всех внутренних микрослужбами приложения.</span><span class="sxs-lookup"><span data-stu-id="a18b7-158">Usually it isn't a good idea to have a single API Gateway aggregating all the internal microservices of your application.</span></span> <span data-ttu-id="a18b7-159">В этом случае он выступает в качестве монолитные инвентаризации программного обеспечения или orchestrator и приводит к нарушению автономность микрослужбу, связывая микрослужбами.</span><span class="sxs-lookup"><span data-stu-id="a18b7-159">If it does, it acts as a monolithic aggregator or orchestrator and violates microservice autonomy by coupling all the microservices.</span></span> <span data-ttu-id="a18b7-160">Таким образом шлюзы API должны быть выделены на основе границы и не act как инвентаризации программного обеспечения для всего приложения.</span><span class="sxs-lookup"><span data-stu-id="a18b7-160">Therefore, the API Gateways should be segregated based on business boundaries and not act as an aggregator for the whole application.</span></span>

<span data-ttu-id="a18b7-161">Иногда детальные шлюза API можно также микрослужбу сам по себе и даже настроить домен или название организации и связанные данные.</span><span class="sxs-lookup"><span data-stu-id="a18b7-161">Sometimes a granular API Gateway can also be a microservice by itself, and even have a domain or business name and related data.</span></span> <span data-ttu-id="a18b7-162">Наличие границы шлюза API для обрабатываемых бизнеса или домена поможет получить лучше.</span><span class="sxs-lookup"><span data-stu-id="a18b7-162">Having the API Gateway’s boundaries dictated by the business or domain will help you to get a better design.</span></span>

<span data-ttu-id="a18b7-163">Можно особенно полезна для более сложных составных приложений пользовательского интерфейса на основании микрослужбами, гранулярности на уровне API шлюза, поскольку концепция детально шлюза API как композиции службу пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a18b7-163">Granularity in the API Gateway tier can be especially useful for more advanced composite UI applications based on microservices, because the concept of a fine-grained API Gateway is similar to a UI composition service.</span></span> <span data-ttu-id="a18b7-164">Мы обсудим это позже в [создания составного пользовательского интерфейса, основанного на микрослужбами](#creating-composite-ui-based-on-microservices-including-visual-ui-shape-and-layout-generated-by-multiple-microservices).</span><span class="sxs-lookup"><span data-stu-id="a18b7-164">We discuss this later in the [Creating composite UI based on microservices](#creating-composite-ui-based-on-microservices-including-visual-ui-shape-and-layout-generated-by-multiple-microservices).</span></span>

<span data-ttu-id="a18b7-165">Таким образом, для многих приложений среднего и большого размера с использованием пользовательского API шлюза обычно является хорошим решением, но как один монолитные инвентаризации программного обеспечения или уникальный центра пользовательские API шлюза.</span><span class="sxs-lookup"><span data-stu-id="a18b7-165">Therefore, for many medium- and large-size applications, using a custom-built API Gateway is usually a good approach, but not as a single monolithic aggregator or unique central custom API Gateway.</span></span>

<span data-ttu-id="a18b7-166">Другой подход заключается в использовании продукта как [управления API Azure](https://azure.microsoft.com/services/api-management/) как показано на рисунке 4-14.</span><span class="sxs-lookup"><span data-stu-id="a18b7-166">Another approach is to use a product like [Azure API Management](https://azure.microsoft.com/services/api-management/) as shown in Figure 4-14.</span></span> <span data-ttu-id="a18b7-167">Такой подход не только позволяет решить потребности API шлюза, но предоставляет функции, например сбор аналитики собственные интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="a18b7-167">This approach not only solves your API Gateway needs, but provides features like gathering insights from your APIs.</span></span> <span data-ttu-id="a18b7-168">При использовании решения управления API шлюз API является только компонентом в рамках этого полному решению управления API.</span><span class="sxs-lookup"><span data-stu-id="a18b7-168">If you are using an API management solution, an API Gateway is only a component within that full API management solution.</span></span>

![](./media/image14.png)

<span data-ttu-id="a18b7-169">**Рис. 4-14**.</span><span class="sxs-lookup"><span data-stu-id="a18b7-169">**Figure 4-14**.</span></span> <span data-ttu-id="a18b7-170">С помощью управления Azure API API шлюза</span><span class="sxs-lookup"><span data-stu-id="a18b7-170">Using Azure API Management for your API Gateway</span></span>

<span data-ttu-id="a18b7-171">В этом случае при использование продукта, например управление API Azure, тот факт, что может потребоваться один шлюз API не так рискованно, поскольку такого рода шлюзы API «узкий», то есть не реализовать пользовательский код C#, который могут включать в сторону монолитные компонент.</span><span class="sxs-lookup"><span data-stu-id="a18b7-171">In this case, when using a product like Azure API Management, the fact that you might have a single API Gateway is not so risky because these kinds of API Gateways are "thinner", meaning that you don't implement custom C# code that could evolve towards a monolithic component.</span></span> 

<span data-ttu-id="a18b7-172">Этот тип продукта более действует как обратного прокси-сервера для передачи данных входящих событий, где можно также фильтровать API из внутренней микрослужбами и применять проверку подлинности для опубликованных интерфейсов API в этом одного уровня.</span><span class="sxs-lookup"><span data-stu-id="a18b7-172">This type of product acts more like a reverse proxy for ingress communication, where you can also filter the APIs from the internal microservices plus apply authorization to the published APIs in this single tier.</span></span>

<span data-ttu-id="a18b7-173">Аналитики, доступных из справочной системы управления API получить представление о том, как используются собственные интерфейсы API и как они выполняются.</span><span class="sxs-lookup"><span data-stu-id="a18b7-173">The insights available from an API Management system help you get an understanding of how your APIs are being used and how they are performing.</span></span> <span data-ttu-id="a18b7-174">Это делается, позволяя просматривать рядом с отчетами в режиме реального времени и выявления трендов, которые может повлиять на ваш бизнес.</span><span class="sxs-lookup"><span data-stu-id="a18b7-174">They do this by letting you view near real-time analytics reports and identifying trends that might impact your business.</span></span> <span data-ttu-id="a18b7-175">Кроме того может иметь журналы действий запроса и ответа для дальнейшего анализа сети и вне сети.</span><span class="sxs-lookup"><span data-stu-id="a18b7-175">Plus, you can have logs about request and response activity for further online and offline analysis.</span></span>

<span data-ttu-id="a18b7-176">Службы управления API Azure можно защитить собственные интерфейсы API, с помощью ключа, маркер и фильтрация IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a18b7-176">With Azure API Management, you can secure your APIs using a key, a token, and IP filtering.</span></span> <span data-ttu-id="a18b7-177">Эти возможности позволяют обеспечить гибкую и тонкого квоты и пределы скорости, изменять форму и поведение собственные интерфейсы API, с помощью политик и позволяют повысить производительность благодаря кэширование ответов.</span><span class="sxs-lookup"><span data-stu-id="a18b7-177">These features let you enforce flexible and fine-grained quotas and rate limits, modify the shape and behavior of your APIs using policies, and improve performance with response caching.</span></span>

<span data-ttu-id="a18b7-178">В этом руководстве и ссылка пример приложения (eShopOnContainers) архитектура проще и собственной разработки контейнерного архитектуры ограничение чтобы сосредоточить внимание на обычные контейнеры без использования продуктов PaaS как API управления Azure.</span><span class="sxs-lookup"><span data-stu-id="a18b7-178">In this guide and the reference sample application (eShopOnContainers), we are limiting the architecture to a simpler and custom-made containerized architecture in order to focus on plain containers without using PaaS products like Azure API Management.</span></span> <span data-ttu-id="a18b7-179">Однако для больших микрослужбу-приложений, развернутых в Microsoft Azure, мы рекомендуем просмотреть и адаптировать API управления Azure как основа для шлюзов API.</span><span class="sxs-lookup"><span data-stu-id="a18b7-179">But for large microservice-based applications that are deployed into Microsoft Azure, we encourage you to review and adopt Azure API Management as the base for your API Gateways.</span></span>

## <a name="drawbacks-of-the-api-gateway-pattern"></a><span data-ttu-id="a18b7-180">Недостатки шаблона API шлюза</span><span class="sxs-lookup"><span data-stu-id="a18b7-180">Drawbacks of the API Gateway pattern</span></span>

-   <span data-ttu-id="a18b7-181">Наиболее важные недостаток заключается в том, что при реализации API шлюза с внутренней микрослужбами взаимозависимость этого уровня.</span><span class="sxs-lookup"><span data-stu-id="a18b7-181">The most important drawback is that when you implement an API Gateway, you are coupling that tier with the internal microservices.</span></span> <span data-ttu-id="a18b7-182">Объединение следующим образом, может возникнуть серьезные проблемы для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a18b7-182">Coupling like this might introduce serious difficulties for your application.</span></span> <span data-ttu-id="a18b7-183">Vaster Клеменса архитектор в группе Azure Service Bus, ссылается на этой потенциальной сложности, как «новый ESB» в его «[обмена сообщениями и Микрослужбами](https://www.youtube.com/watch?v=rXi5CLjIQ9k)» в GOTO 2016 сеанс.</span><span class="sxs-lookup"><span data-stu-id="a18b7-183">Clemens Vaster, architect at the Azure Service Bus team, refers to this potential difficulty as “the new ESB” in his "[Messaging and Microservices](https://www.youtube.com/watch?v=rXi5CLjIQ9k)" session at GOTO 2016.</span></span>

-   <span data-ttu-id="a18b7-184">С помощью микрослужбами API шлюза создает дополнительные возможных узких мест.</span><span class="sxs-lookup"><span data-stu-id="a18b7-184">Using a microservices API Gateway creates an additional possible single point of failure.</span></span>

-   <span data-ttu-id="a18b7-185">Шлюз API могут вызвать увеличения времени ответа из-за дополнительных сетевых вызовов.</span><span class="sxs-lookup"><span data-stu-id="a18b7-185">An API Gateway can introduce increased response time due to the additional network call.</span></span> <span data-ttu-id="a18b7-186">Тем не менее этот дополнительный вызов обычно имеет меньше влияния, чем ошибки возникают интерфейс, который отправляет которых слишком много прямого вызова внутренней микрослужбами.</span><span class="sxs-lookup"><span data-stu-id="a18b7-186">However, this extra call usually has less impact than having a client interface that is too chatty directly calling the internal microservices.</span></span>

-   <span data-ttu-id="a18b7-187">Если не масштабировать должным образом, шлюз API может стать узким местом.</span><span class="sxs-lookup"><span data-stu-id="a18b7-187">If not scaled out properly, the API Gateway can become a bottleneck.</span></span>

-   <span data-ttu-id="a18b7-188">Шлюз API требует затраты на разработку и обслуживание будущих, если он включает пользовательской логики и статистической обработки данных.</span><span class="sxs-lookup"><span data-stu-id="a18b7-188">An API Gateway requires additional development cost and future maintenance if it includes custom logic and data aggregation.</span></span> <span data-ttu-id="a18b7-189">Разработчикам необходимо обновить шлюз API для предоставления конечных точек каждой микрослужбы.</span><span class="sxs-lookup"><span data-stu-id="a18b7-189">Developers must update the API Gateway in order to expose each microservice’s endpoints.</span></span> <span data-ttu-id="a18b7-190">Кроме того изменения реализации в внутренней микрослужбами может привести к изменения кода на уровне API шлюза.</span><span class="sxs-lookup"><span data-stu-id="a18b7-190">Moreover, implementation changes in the internal microservices might cause code changes at the API Gateway level.</span></span> <span data-ttu-id="a18b7-191">Тем не менее если шлюз API просто применяет безопасности, ведение журнала и управление версиями (как при использовании API управления Azure), эти затраты на разработку могут не действовать.</span><span class="sxs-lookup"><span data-stu-id="a18b7-191">However, if the API Gateway is just applying security, logging, and versioning (as when using Azure API Management), this additional development cost might not apply.</span></span>

-   <span data-ttu-id="a18b7-192">Если шлюз API, разработанном одну группу, может быть узким местом разработки.</span><span class="sxs-lookup"><span data-stu-id="a18b7-192">If the API Gateway is developed by a single team, there can be a development bottleneck.</span></span> <span data-ttu-id="a18b7-193">Это еще одна причина, почему лучше иметь несколько Контролируемая влечет API шлюзов, которые отвечать на разные клиентские запросы.</span><span class="sxs-lookup"><span data-stu-id="a18b7-193">This is another reason why a better approach is to have several fined-grained API Gateways that respond to different client needs.</span></span> <span data-ttu-id="a18b7-194">Может также внутренне разделять API шлюза на несколько областей или уровни, которые принадлежат другой команды, работающие на внутренние микрослужбами.</span><span class="sxs-lookup"><span data-stu-id="a18b7-194">You could also segregate the API Gateway internally into multiple areas or layers that are owned by the different teams working on the internal microservices.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a18b7-195">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a18b7-195">Additional resources</span></span>

-   <span data-ttu-id="a18b7-196">**Чарльз Ричардсон. Шаблон: API шлюза и внутреннем сервере для переднего плана**
    [*http://microservices.io/patterns/apigateway.html*](http://microservices.io/patterns/apigateway.html)</span><span class="sxs-lookup"><span data-stu-id="a18b7-196">**Charles Richardson. Pattern: API Gateway / Backend for Front-End**
[*http://microservices.io/patterns/apigateway.html*](http://microservices.io/patterns/apigateway.html)</span></span>

-   <span data-ttu-id="a18b7-197">**Управление Azure API**
    [*https://azure.microsoft.com/services/api-management/*](https://azure.microsoft.com/services/api-management/)</span><span class="sxs-lookup"><span data-stu-id="a18b7-197">**Azure API Management**
[*https://azure.microsoft.com/services/api-management/*](https://azure.microsoft.com/services/api-management/)</span></span>

-   <span data-ttu-id="a18b7-198">**UDI Dahan. Сервисноориентированные композиции**\\</span><span class="sxs-lookup"><span data-stu-id="a18b7-198">**Udi Dahan. Service Oriented Composition**\\</span></span>
    [<span data-ttu-id="a18b7-199">*http://udidahan.com/2014/07/30/Service-Oriented-Composition-WITH-Video/*</span><span class="sxs-lookup"><span data-stu-id="a18b7-199">*http://udidahan.com/2014/07/30/service-oriented-composition-with-video/*</span></span>](http://udidahan.com/2014/07/30/service-oriented-composition-with-video/)

-   <span data-ttu-id="a18b7-200">**Clemens Vasters. Обмен сообщениями и Микрослужбами на GOTO 2016** (видео) [ *https://www.youtube.com/watch?v=rXi5CLjIQ9k*](https://www.youtube.com/watch?v=rXi5CLjIQ9k)</span><span class="sxs-lookup"><span data-stu-id="a18b7-200">**Clemens Vasters. Messaging and Microservices at GOTO 2016** (video) [*https://www.youtube.com/watch?v=rXi5CLjIQ9k*](https://www.youtube.com/watch?v=rXi5CLjIQ9k)</span></span>


>[!div class="step-by-step"]
<span data-ttu-id="a18b7-201">[Предыдущие] (определить микрослужбу домена модели boundaries.md) [Далее] (связи в микрослужбу architecture.md)</span><span class="sxs-lookup"><span data-stu-id="a18b7-201">[Previous] (identify-microservice-domain-model-boundaries.md) [Next] (communication-in-microservice-architecture.md)</span></span>