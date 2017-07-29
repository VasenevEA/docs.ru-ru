---
title: "Организация пулов соединений SQL Server (ADO.NET) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7e51d44e-7c4e-4040-9332-f0190fe36f07
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Организация пулов соединений SQL Server (ADO.NET)
Соединение с сервером базы данных обычно состоит из нескольких длительных шагов.  Необходимо установить физический канал, например сокет или именованный канал, выполнить первоначальное подтверждение установления связи с сервером, выполнить синтаксический анализ данных строки соединения, сервер должен проверить подлинность соединения, а также запустить проверку прикреплений в текущей транзакции и т. д.  
  
 На практике большинство приложений использует только одно или несколько различных конфигураций соединений.  Это означает, что во время выполнения приложения многие идентичные соединения будут повторно открываться и закрываться.  Чтобы сократить стоимость открытия соединения, [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] использует технологию оптимизации, называемую *пулом соединений*.  
  
 Пул соединений снижает количество открытий новых соединений.  *Организатор пулов* поддерживает владение физическим соединением.  Он управляет соединениями с помощью поддержания набора активных соединений для каждой конфигурации данного соединения.  Каждый раз, когда пользователь вызывает метод `Open` в соединении, организатор пулов ищет в пуле доступное соединение.  Если соединение пула доступно, вместо открытия нового соединения он возвращает его участнику.  При вызове приложением метода `Close` в соединении вместо закрытия организатор пулов возвращает его в набор активных соединений пула.  После возвращения соединения в пул оно готово к повторному использованию при следующем вызове метода `Open`.  
  
 В пул могут помещаться только соединения с одинаковой конфигурацией.  [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] поддерживает несколько пулов одновременно, по одному для каждой конфигурации.  Соединения разделяются в пулы строкой соединения, а при использовании встроенной безопасности \- удостоверением Windows.  Соединения также заносятся в пул в зависимости от того, прикреплены ли они к транзакции.  При использовании метода <xref:System.Data.SqlClient.SqlConnection.ChangePassword%2A> экземпляр <xref:System.Data.SqlClient.SqlCredential> влияет на пул соединений.  Различные экземпляры <xref:System.Data.SqlClient.SqlCredential> используют различные пулы соединений, даже если идентификатор пользователя и пароль совпадают.  
  
 Организация пулов соединений может существенно улучшить производительность и масштабируемость приложения.  По умолчанию пул соединений в [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] включен.  Пока организатор пулов не будет явно отключен, он оптимизирует соединения по мере их открытия и закрытия в приложении.  Также можно указать несколько модификаторов строки соединения для управления поведением пула соединений.  Дополнительные сведения см. в подразделе «Управление пулами соединений с помощью ключевых слов строки соединения» далее в этом разделе.  
  
> [!NOTE]
>  Если включено создание пулов соединения и происходит ошибка времени ожидания или другая ошибка входа, то выдается исключение и последующие попытки подключения завершаются ошибкой в течение следующего «интервала блокирования» \- 5 секунд.  Если приложение пытается установить подключение в течение интервала блокирования, то снова выдается первое исключение.  Последующие ошибки после завершения интервала блокирования приводят к возникновению новых интервалов блокирования, вдвое превышающих предыдущий период времени блокирования, вплоть до максимального значения в 1 минуту.  
  
## Создание и назначение пулов  
 При первом открытии соединения создается пул соединений, основанный на алгоритме точного совпадения, связанного с пулом строкой соединения.  Каждый пул соединений связывается с отдельной строкой соединения.  При открытии нового соединения, если строка соединения не соответствует в точности существующему пулу, создается новый пул.  Соединения заносятся в пул отдельно для процесса, домена приложения, строки соединения и, если используется встроенная безопасность, для удостоверения Windows.  Строки соединения должны точно совпадать. Ключевые слова, указанные в различном порядке для одного соединения, будут включены в пул по отдельности.  
  
 В следующем примере C\# создаются три новых объекта <xref:System.Data.SqlClient.SqlConnection>, но для управления ими требуется только два пула соединений.  Обратите внимание, что первая и вторая строки соединения отличаются значениями, присвоенными аргументу `Initial Catalog`.  
  
```  
using (SqlConnection connection = new SqlConnection(  
  "Integrated Security=SSPI;Initial Catalog=Northwind"))  
    {  
        connection.Open();        
        // Pool A is created.  
    }  
  
using (SqlConnection connection = new SqlConnection(  
  "Integrated Security=SSPI;Initial Catalog=pubs"))  
    {  
        connection.Open();        
        // Pool B is created because the connection strings differ.  
    }  
  
using (SqlConnection connection = new SqlConnection(  
  "Integrated Security=SSPI;Initial Catalog=Northwind"))  
    {  
        connection.Open();        
        // The connection string matches pool A.  
    }  
```  
  
 Если аргумент `MinPoolSize` не указан в строке соединения или указано значение 0, соединения в пуле будут закрыты после периода отсутствия активности.  Однако, если значение аргумента `MinPoolSize` больше 0, пул соединений не уничтожается, пока не будет выгружен домен приложения `AppDomain` и не завершится процесс.  Обслуживание неактивных или пустых пулов требует минимальных системных издержек.  
  
> [!NOTE]
>  Пул автоматически очищается при возникновении неустранимой ошибки, например переходе на другой ресурс.  
  
## Добавление соединений  
 Пул соединений создается для каждой уникальной строки соединения.  При создании пула создается множество объектов соединения, которые добавляются в пул для удовлетворения требования к минимальному размеру пула.  Соединения добавляются в пул по необходимости, вплоть до указанного максимального размера пула \(по умолчанию \- 100\).  Соединения освобождаются обратно в пул при закрытии или ликвидации.  
  
 При запросе объекта <xref:System.Data.SqlClient.SqlConnection> он получается из пула при наличии готового к использованию соединения.  Чтобы соединение можно было использовать, оно не должно использоваться, иметь совпадающий контекст транзакции либо не иметь связи с каким\-либо контекстом транзакций и иметь допустимую ссылку на сервер.  
  
 Организатор пулов соединений обрабатывает запросы соединений путем их повторного размещения после возврата в пул.  Если достигнут максимальный размер пула, а пригодные соединения недоступны, запрос помещается в очередь.  Затем организатор пулов пытается вернуть любое соединение до истечения времени ожидания \(по умолчанию \- 15 секунд\).  Если организатор пулов не может обработать запрос до истечения времени ожидания соединения, возникнет исключение.  
  
> [!CAUTION]
>  Настоятельно рекомендуется всегда закрывать соединение после его использования, чтобы оно вернулось в пул.  Это можно сделать с помощью методов `Close` или `Dispose` объекта `Connection` либо открыв все соединения внутри инструкции `using` в C\# или инструкции `Using` в [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)].  Соединения, которые явно не закрыты, нельзя добавить или вернуть в пул.  Дополнительные сведения см. в разделе [Оператор using](../Topic/using%20Statement%20\(C%23%20Reference\).md) или [Практическое руководство. Удаление системного ресурса](../Topic/How%20to:%20Dispose%20of%20a%20System%20Resource%20\(Visual%20Basic\).md) для [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)].  
  
> [!NOTE]
>  В методе `Close` вашего класса нельзя вызывать методы `Dispose` или `Connection` объектов `DataReader`, `Finalize` или любого другого управляемого объекта.  В методе завершения следует только освобождать неуправляемые ресурсы, которыми ваш класс непосредственно владеет.  Если класс не владеет какими\-либо неуправляемыми ресурсами, не включайте в его определение метод `Finalize`.  Дополнительные сведения см. в разделе [Garbage Collection](../../../../docs/standard/garbage-collection/index.md).  
  
> [!NOTE]
>  События входа в систему и выхода из системы не вызываются на сервере при выборке подключения из пула подключений и при возврате его в пул подключений.  Причина заключается в том, что при возврате в пул подключений подключение фактически не закрывается.  Дополнительные сведения см. в разделах [Класс события аудита входа в систему](http://msdn2.microsoft.com/library/ms190260.aspx) и [Класс события аудита выхода из системы](http://msdn2.microsoft.com/library/ms175827.aspx) электронной документации [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)].  
  
## Удаление соединений  
 Организатор пулов соединений удаляет соединение из пула после его простоя в течение примерно 4\-8 минут или при определении им разрыва соединения с сервером.  Обратите внимание, что разорванное соединение можно определить только после попытки связи с сервером.  При обнаружении соединения, которое больше не имеет связи с сервером, оно помечается как недействительное.  Недействительные соединения удаляются из пула соединений только после их закрытия или возврата.  
  
 Если существующее соединение с сервером исчезло, оно может быть удалено из пула, даже если организатор пулов соединений не определил разорванное соединение и не пометил его как недопустимое.  Это происходит вследствие того, что проверка соединения на допустимость уничтожит преимущества существования организатора пулов, став причиной вызова очередного цикла приема\-передачи с сервером.  В этом случае первая попытка использовать соединение определит его разрыв и вызовет исключение.  
  
## Очистка пула  
 В [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 2.0 появилось два новых метода для очистки пула: <xref:System.Data.SqlClient.SqlConnection.ClearAllPools%2A> и <xref:System.Data.SqlClient.SqlConnection.ClearPool%2A>.  Метод `ClearAllPools` очищает пулы соединений данного поставщика, а метод `ClearPool` \- пул, связанный с конкретным соединением.  Если во время вызова методов соединения использовались, они соответствующим образом помечаются.  При их закрытии вместо возвращения в пул они удаляются.  
  
## Поддержка транзакций  
 Соединения выбираются из пула и назначаются в зависимости от контекста транзакции.  Если в строке соединения не указан аргумент `Enlist=false`, пул соединений гарантирует прикрепление соединения к контексту <xref:System.Transactions.Transaction.Current%2A>.  После закрытия и возврата соединения в пул с прикрепленной транзакцией `System.Transactions` оно резервируется таким образом, что следующий запрос к пулу соединений с той же транзакцией `System.Transactions` вернет это соединение, если оно доступно.  Если при выдаче такого запроса в пуле нет доступных соединений, соединение берется и прикрепляется из части пула, не использующей транзакции.  Если доступных соединений нет во всех частях пула, создается и прикрепляется новое соединение.  
  
 При закрытии соединения оно освобождается обратно в пул и в соответствующий подраздел в зависимости от его контекста транзакции.  Поэтому можно закрыть соединение без создания ошибки, даже если распределенная транзакция все еще находится в ожидании.  Это позволит зафиксировать или отменить распределенную транзакцию позже.  
  
## Управление пулами соединений с помощью ключевых слов строки соединения  
 Свойство `ConnectionString` объекта <xref:System.Data.SqlClient.SqlConnection> поддерживает пары «ключ\-значение» из строки соединения, с помощью которых можно изменять логику организации пулов соединений.  Для получения дополнительной информации см. <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
## Фрагментация пула  
 Фрагментация пула является распространенной проблемой для многих веб\-приложений, в которых может создаваться большое количество пулов, которые не освобождаются, пока существует процесс.  Это оставляет большое количество соединений открытыми и потребляющими память, что приводит к ухудшению производительности.  
  
### Фрагментация пула из\-за встроенной безопасности  
 Соединения заносятся в пул в соответствии со строкой соединения, а также удостоверением пользователя.  Таким образом, при использовании на веб\-узле обычной проверки подлинности или проверки подлинности Windows, а также встроенной безопасности имени входа получается один пул на пользователя.  Несмотря на то, что это улучшает производительность последующих запросов пользователя к базе данных, для него недоступны преимущества соединений, установленных другими пользователями.  Это также приводит по крайней мере к одному соединению с сервером базы данных для каждого пользователя.  Это является побочным эффектом данной архитектуры веб\-приложений, который разработчики должны соизмерить с требованиями безопасности и аудита.  
  
### Фрагментация пула из\-за многочисленных баз данных  
 Многие поставщики услуг Интернет размещают несколько веб\-узлов на одиночном сервере.  Они могут использовать одну базу данных для подтверждения проверки подлинности имени входа с помощью форм и затем открывать соединение с определенной базой данных для этого пользователя или группы пользователей.  Соединение с базой данных проверки подлинности заносится в пул и используется всеми.  Однако для каждой базы данных существует отдельный пул соединений, увеличивающий количество соединений с сервером.  
  
 Это также является побочным эффектом конструкции приложений.  При соединении с [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] существует относительно простой способ устранения этого побочного эффекта без нарушения безопасности.  Вместо соединения каждого пользователя или группы с отдельной базой данных устанавливается соединение с одной базой данных на сервере, а затем выполняется инструкция [!INCLUDE[tsql](../../../../includes/tsql-md.md)] USE, чтобы переключиться на требуемую базу данных.  Следующий фрагмент кода демонстрирует создание первоначального соединения с базой данных `master` и последующее переключение на требуемую базу данных, указанную в строковой переменной `databaseName`.  
  
```vb  
' Assumes that command is a valid SqlCommand object and that  
' connectionString connects to master.  
    command.Text = "USE DatabaseName"  
Using connection As New SqlConnection(connectionString)  
    connection.Open()  
    command.ExecuteNonQuery()  
End Using  
```  
  
```csharp  
// Assumes that command is a SqlCommand object and that  
// connectionString connects to master.  
command.Text = "USE DatabaseName";  
using (SqlConnection connection = new SqlConnection(  
  connectionString))  
  {  
    connection.Open();  
    command.ExecuteNonQuery();  
  }  
```  
  
## Роли приложений и пул соединений  
 После активации роли приложения [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] с помощью вызова системной хранимой процедуры `sp_setapprole` контекст безопасности данного соединения сбросить нельзя.  Однако, если использование пула включено, соединение возвращается в пул и при повторном использовании соединения возникает ошибка.  Дополнительные сведения см. в статье базы знаний Майкрософт [Ошибки роли приложения SQL с пулами ресурсов OLE DB](http://support.microsoft.com/default.aspx?scid=KB;RU-RU;Q229564).  
  
### Альтернативы ролям приложений  
 Рекомендуется пользоваться преимуществом новых механизмов безопасности, которые пришли на смену ролям приложения.  Дополнительные сведения см. в разделе [Создание ролей приложения в SQL Server](../../../../docs/framework/data/adonet/sql/creating-application-roles-in-sql-server.md).  
  
## См. также  
 [Организация пулов соединений](../../../../docs/framework/data/adonet/connection-pooling.md)   
 [SQL Server и ADO.NET](../../../../docs/framework/data/adonet/sql/index.md)   
 [Счетчики производительности](../../../../docs/framework/data/adonet/performance-counters.md)   
 [Управляемые поставщики ADO.NET и Центр разработчиков DataSet](http://go.microsoft.com/fwlink/?LinkId=217917)