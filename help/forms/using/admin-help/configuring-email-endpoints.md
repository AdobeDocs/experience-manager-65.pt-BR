---
title: Configuração de endpoints de email
description: Saiba como configurar endpoints de email. Os endpoints de email permitem que você chame um serviço enviando um ou mais documentos para uma conta de email especificada.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 33583a12-4f20-4146-baa4-c9854e454bbf
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3796'
ht-degree: 0%

---

# Configuração de endpoints de email {#configuring-email-endpoints}

Os endpoints de email permitem que os usuários chamem um serviço enviando um ou mais documentos (como anexos de email) para uma conta de email especificada. A caixa de entrada de email atua como um ponto de coleta para os anexos. O serviço monitora a caixa de entrada e processa os anexos. Os resultados da conversão são encaminhados ao usuário definido no endpoint.

Para um endpoint de email, os usuários autorizados podem chamar um processo enviando arquivos por email para a conta apropriada. Os resultados serão retornados ao usuário remetente (por padrão) ou ao usuário definido nas configurações de endpoint.

Antes de configurar um endpoint de email, crie uma conta de email POP3 ou IMAP para ser usada pelo endpoint. Configure uma conta separada para cada tipo de conversão. Por exemplo, uma conta pode ser configurada para gerar documentos PDF padrão a partir de anexos de arquivos recebidos, e outra conta pode ser configurada para gerar documentos PDF seguros.

>[!NOTE]
>
>Cada endereço de email deve ser mapeado para apenas um endpoint de email. Não é possível configurar vários endpoints de email para um único endereço de email, mesmo que os endpoints de email adicionais estejam desabilitados.

Todos os endpoints de email são configurados com um nome de usuário autorizado e uma senha para a caixa de entrada de email, que são necessários ao invocar o serviço. A conta de e-mail está protegida pelo sistema do servidor de e-mail no qual está configurada.

Se os usuários enviarem documentos com caracteres do idioma europeu ocidental em nomes de caminho de arquivo e conversão, eles deverão usar um aplicativo de email que ofereça suporte aos tipos de codificação necessários (latino1) [ISO-8859-1], Europeu Ocidental [Windows], ou UTF-8). Para obter mais informações, consulte *Instalação e implantação de formulários AEM* para o seu servidor de aplicativos.

Antes de configurar um endpoint de email, configure o Serviço de email. (Consulte [Definir configurações padrão de ponto de extremidade de email](configuring-email-endpoints.md#configure-default-email-endpoint-settings).) Os parâmetros de configuração do serviço de email têm duas finalidades:

* Para configurar atributos comuns a todos os endpoints de email
* Para fornecer valores padrão para todos os pontos de extremidade de email

## Configurar SSL para um endpoint de email {#configure-ssl-for-an-email-endpoint}

Você pode configurar POP3, IMAP ou SMTP para usar o Secure Sockets Layer (SSL) como um endpoint de email.

1. No servidor de email, ative o SSL para POP3, IMAP ou SMTP de acordo com a documentação do fabricante.
1. Exporte um certificado de cliente do servidor de email.
1. Use o programa keytool para importar o arquivo de certificado do cliente para o armazenamento de certificados da Java Virtual Machine (JVM) do servidor de aplicativos. O procedimento para esta etapa dependerá dos caminhos de instalação da JVM e do cliente.

   Por exemplo, se estiver usando uma instalação padrão do Oracle WebLogic Server com JDK 1.5.0 no Microsoft Windows Server® 2003, digite o seguinte texto em um prompt de comando:

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. Quando solicitado, insira a senha (para Java, a senha padrão é `changeit`). Você receberá uma mensagem informando que o certificado foi importado com êxito.
1. Use o console de administração para adicionar o terminal de email ao serviço.
1. Crie o endpoint de email no console de administração. Ao definir as configurações de endpoint, selecione POP3/IMAP SSL Enabled para mensagens recebidas e SMTP SSL Enabled para mensagens enviadas e altere as propriedades da porta de acordo.

>[!NOTE]
>
>Dica: se tiver problemas ao usar SSL, use um cliente de email como o Microsoft Outlook para verificar se ele pode acessar o servidor de email usando SSL. Se o cliente de email não puder acessar o servidor de email, o problema está relacionado à configuração do certificado ou do servidor de email.

## Definir configurações padrão de ponto de extremidade de email {#configure-default-email-endpoint-settings}

Você pode usar a página Gerenciamento de serviço para configurar atributos que são comuns para todos os endpoints de email e para fornecer valores default para todos os endpoints de email.

Para que o fluxo de trabalho de formulários receba e manipule mensagens de email recebidas dos usuários, é necessário criar um terminal de email para o serviço Tarefa Completa. Esse endpoint de email requer configurações adicionais, conforme descrito em [Criar um terminal de email para o serviço de Tarefa Concluída](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service).

### Alterar os valores padrão para pontos de extremidade de email {#change-the-default-values-for-email-endpoints}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de serviços, clique em Email: 1.0 (a ID do componente é com.adobe.idp.dsc.provider.service.email.Email).
1. Na guia Configuração, especifique as configurações padrão de endpoint de email e clique em Salvar.

### Configurações padrão de ponto de extremidade de email {#default-email-endpoint-settings}

**Expressão Cron:** A expressão cron foi usada pelo quartzo para agendar a pesquisa do diretório de entrada.

**Intervalo de Repetição:** O número de vezes que a pesquisa de diretório é repetida. O intervalo de repetição padrão é em segundos se esse valor não for especificado na configuração do endpoint. O valor padrão é 10. Este valor não pode ser menor que 10.

**Contagem de repetição:** O número de vezes que o diretório de entrada é sondado. A contagem de repetição padrão a ser usada se esse valor não for especificado na configuração do endpoint. Um valor -1 indica uma varredura indefinida do diretório. O valor padrão é -1.

**Atraso no início do trabalho:** O valor padrão, em segundos, do atraso antes que o trabalho comece a verificar o endpoint. O valor padrão é 0.

**Tamanho do lote:** O número de emails que o receptor processa por verificação para obter o desempenho ideal. Um valor -1 indica todos os emails. O valor padrão é 2.

**Assíncrono:** Identifica o tipo de invocação como assíncrono ou síncrono. Processos transitórios e síncronos só podem ser chamados de forma síncrona. O valor padrão é assíncrono.

**Padrão do domínio:** O padrão do nome de domínio usado para filtrar emails de entrada. Por exemplo, se adobe.com for usado, somente o email do adobe.com será processado; o email de outros domínios será ignorado.

**Padrão do arquivo:** Os padrões de anexo de arquivo de entrada que o provedor aceita. Isso inclui arquivos que têm extensões específicas (&amp;ast;.dat, &amp;ast;.xml), nomes específicos (dados) e expressões compostas no nome e na extensão (.[dD][aA]&#39;porta&#39;). O valor padrão é &amp;ast;.&amp;ast;.

**Destinatários do Trabalho Bem-sucedido:** Um ou mais endereços de email usados para enviar emails para indicar trabalhos bem-sucedidos. Por padrão, uma mensagem de tarefa bem-sucedida é sempre enviada ao remetente da tarefa inicial. Até 100 recipients são suportados. Para desativar essa configuração, deixe esse campo em branco.

**Destinatários do trabalho com falha:** Um ou mais endereços de email usados para enviar emails para indicar tarefas com falha. Por padrão, uma mensagem de tarefa com falha é sempre enviada ao remetente que enviou a tarefa inicial. Até 100 recipients são suportados. Para desativar essa configuração, deixe esse campo em branco.

**Host da caixa de entrada:** O nome do host ou endereço IP da caixa de entrada do provedor de email a ser verificado.

**Porta da caixa de entrada:** O número da porta da caixa de entrada do provedor de email a ser verificado. Se o valor for 0, a porta IMAP ou POP3 padrão será usada.

**Protocolo da caixa de entrada:** O protocolo de email para o endpoint de email a ser usado para verificar a caixa de entrada. As opções são IMAP ou POP3. O servidor de e-mail do host da caixa de entrada deve suportar esses protocolos.

**Tempo limite da caixa de entrada:** Especifica por quanto tempo o ponto de extremidade aguardará antes de cancelar ao tentar se conectar à caixa de entrada. Se uma conexão não for adquirida antes que o valor de tempo limite seja atingido, a caixa de entrada não será sondada.

**Usuário da caixa de entrada:** O nome de usuário necessário para fazer logon na conta de email. Dependendo do servidor de email e da configuração, esse nome pode ser apenas a parte do nome de usuário do email ou pode ser o endereço de email completo.

**Senha da caixa de entrada:** A senha do Usuário da Caixa de Entrada.

**SSL POP3/IMAP Habilitado:** Quando selecionada, esta opção ativa o SSL.

**Host SMTP:** O nome de host do servidor de email que o provedor de email usa para enviar resultados e mensagens de erro. Por exemplo, mail.example.com.

**Porta SMTP:** A porta usada para conexão com o servidor de e-mail. O valor padrão é 25.

**Usuário SMTP:** A conta de usuário do provedor de email a ser usada ao enviar email para obter resultados e erros.

**Senha SMTP:** A senha da conta SMTP. Alguns servidores de email não exigem uma senha SMTP.

**Enviar de:** O endereço de email (por exemplo, user@company.com) usado para enviar notificações por email de resultados e erros. Se você não especificar um valor Enviar de, o servidor de email tentará determinar o endereço de email combinando o valor especificado na configuração Usuário SMTP com um domínio padrão configurado no servidor de email. Se o servidor de email não tiver um domínio padrão e você não especificar um valor para Enviar de, poderão ocorrer erros. Para garantir que as mensagens de email tenham o endereço &quot;de&quot; correto, especifique um valor para a configuração &quot;Enviar de&quot;.

**SMTP SSL Habilitado:** Quando selecionada, habilita SSL em SMTP.

**Incluir O Corpo Do Email Original Como Um Anexo:** Por padrão, ao enviar um email para o Forms Server, o texto original da mensagem é incluído no corpo dela. Para incluir o texto como um anexo, selecione essa opção.

**Usar A Linha De Assunto Original Para Emails De Resultado:** Por padrão, o servidor do Forms usa os valores especificados nas configurações Assunto do email de sucesso e Assunto do email de erro como a linha de assunto ao enviar as mensagens de email de resultado. Para usar a mesma linha de assunto do email original enviado ao servidor, selecione essa opção.

**Assunto do email de sucesso:** Depois de enviar um email a um endpoint de email para iniciar ou continuar um processo, você receberá uma mensagem de email de retorno do servidor do AEM Forms. Se o email for bem-sucedido, você receberá um email de sucesso. Se seu email falhar, você receberá um email de falha informando por que ele falhou. Essa configuração permite especificar a linha de assunto das mensagens de email de sucesso enviadas para esse endpoint.

**Corpo do email de sucesso:** Permite especificar o corpo de texto das mensagens de email de sucesso enviadas para esse endpoint.

**Erro no prefixo do assunto do email:** Permite especificar o texto usado no início da linha de assunto das mensagens de email de falha enviadas para esse endpoint.

**Assunto do email de erro:** Permite especificar a linha de assunto das mensagens de email de falha enviadas para este endpoint. Esse texto é exibido após o Prefixo do assunto do email de erro.

**Corpo do email de erro:** Permite especificar a primeira linha do corpo de texto das mensagens de email de falha enviadas para esse endpoint.

**Informações de resumo de email:** Cada mensagem de sucesso ou falha inclui uma seção contendo o texto original do email enviado ao Forms Server. Essa configuração especifica o texto que aparece acima dessa seção.

**Validar Caixa De Entrada Antes De Criar/Atualizar Este Ponto De Extremidade:** Quando essa opção é selecionada, o Forms Server verifica se as configurações SMTP/POP3 estão corretas antes de criar o endpoint. Quando você clica em Adicionar, é exibida uma mensagem informando se a conta da caixa de entrada é válida. Se essa opção não estiver selecionada, o AEM Forms Server criará o endpoint sem validar a caixa de entrada.

**Codificação do conjunto de caracteres:** O formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários em um ambiente japonês podem escolher ISO2022-JP.

**Pasta de emails enviados com falha:** Especifica um diretório no qual armazenar resultados se o servidor de email SMTP não estiver operacional.

## Configurações de ponto de extremidade de email {#email-endpoint-settings}

Use as configurações a seguir para configurar um endpoint de email.

**Nome:** Uma configuração obrigatória que identifica o endpoint. Não inclua um caractere &lt; porque ele trunca o nome exibido no Espaço de trabalho. Se você estiver inserindo um URL como o nome do endpoint, verifique se ele está em conformidade com as regras de sintaxe especificadas no RFC1738.

**Descrição:** Uma descrição do endpoint. Não inclua um caractere &lt; porque ele trunca a descrição exibida no Espaço de trabalho.

**Expressão Cron:** Insira uma expressão cron se o email precisar ser agendado usando uma expressão cron.

**Contagem de repetição:** Número de vezes que o endpoint de email verifica a pasta ou o diretório. Um valor de -1 indica varredura indefinida. O valor padrão é -1.

**Intervalo de Repetição:** A taxa de varredura que o destinatário usa para verificar e-mails de entrada.

**Atraso no início do trabalho:** O tempo de espera para verificação depois que o programador é iniciado.

**Tamanho do lote:** O número de emails que o receptor processa por verificação para obter o desempenho ideal. Um valor -1 indica todos os emails. O valor padrão é 2.

**Nome de usuário:** Uma configuração obrigatória, que é o nome de usuário usado ao chamar um serviço do Target por email. O valor padrão é SuperAdmin.

**Nome do domínio:** Uma configuração obrigatória, que é o domínio do usuário. O valor padrão é DefaultDom.

**Padrão do domínio:** Especifica os padrões de domínio de emails de entrada que o provedor aceita. Por exemplo, se adobe.com for usado, somente o email do adobe.com será processado; o email de outros domínios será ignorado.

**Padrão do arquivo:** Especifica os padrões de anexo de arquivo de entrada que o provedor aceita. Isso inclui arquivos que têm extensões específicas (&amp;ast;.dat, &amp;ast;.xml), nomes específicos (dados) ou expressões compostas no nome e na extensão (&amp;ast;.[dD][aA]&#39;porta&#39;).

**Destinatários do Trabalho Bem-sucedido:** Um endereço de e-mail para o qual as mensagens são enviadas para indicar tarefas bem-sucedidas. Por padrão, uma mensagem de tarefa bem-sucedida é sempre enviada ao remetente. Se você digitar remetente, os resultados do email serão enviados para ele. Até 100 recipients são suportados. Especifique recipients adicionais com endereços de email, separados por vírgulas (,).

Para desativar essa configuração, deixe a configuração em branco. Em alguns casos, você deseja acionar um processo e não deseja uma notificação por email sobre o resultado.

**Destinatários do trabalho com falha:** Um endereço de e-mail para o qual as mensagens são enviadas para indicar tarefas com falha. Por padrão, uma mensagem de tarefa com falha é sempre enviada ao remetente. Se você digitar remetente, os resultados do email serão enviados para ele. Até 100 recipients são suportados. Especifique recipients adicionais com endereços de email, separados por vírgulas (,).

Para desativar essa configuração, deixe a configuração em branco. Em alguns casos, você deseja acionar um processo e não deseja uma notificação por email sobre o resultado.

**Host da caixa de entrada:** O nome do host ou endereço IP da caixa de entrada do provedor de email a ser verificado.

**Porta da caixa de entrada:** A porta usada pelo servidor de email. O valor padrão para POP3 é 110 e o valor padrão para IMAP é 143. Se o SSL estiver ativado, o valor default para POP3 será 995 e o valor default para IMAP será 993.

**Protocolo da caixa de entrada:** O protocolo de email para o endpoint de email a ser usado para verificar a caixa de entrada. Os valores são IMAP ou POP3. O servidor de e-mail do host da caixa de entrada deve suportar esses protocolos.

**Tempo limite da caixa de entrada:** O tempo limite, em segundos, para o provedor de email aguardar as respostas da caixa de entrada.

**Usuário da caixa de entrada:** O nome de usuário necessário para fazer logon na conta de email. Dependendo do servidor de email e da configuração, esse valor pode ser apenas a parte do nome de usuário do email ou pode ser o endereço de email completo.

**Senha da caixa de entrada:** A senha do usuário da caixa de entrada.

**SSL POP3/IMAP Habilitado:** Selecione esta configuração para forçar o provedor de email a usar SSL para verificar a caixa de entrada. Certifique-se de que seu servidor de e-mail suporta SSL.

**Host SMTP:** O nome de host do servidor de email que o provedor de email usa para enviar resultados e mensagens de erro.

**Porta SMTP:** O valor padrão para a porta SMTP é 25.

**Usuário SMTP:** A conta de usuário do provedor de email a ser usada quando ele enviar notificações por email de resultados e erros.

**Senha SMTP:** A senha da conta SMTP. Alguns servidores de email não exigem uma senha SMTP.

**Enviar de:** O endereço de email (por exemplo, user@company.com) usado para enviar notificações por email de resultados e erros. Se você não especificar um valor Enviar de, o servidor de email tentará determinar o endereço de email combinando o valor especificado na configuração Usuário SMTP com um domínio padrão configurado no servidor de email. Se o servidor de email não tiver um domínio padrão e você não especificar um valor para Enviar de, poderão ocorrer erros. Para garantir que as mensagens de email tenham o endereço &quot;de&quot; correto, especifique um valor para a configuração &quot;Enviar de&quot;.

**SMTP SSL Habilitado:** Selecione esta configuração para forçar o provedor de email a usar SSL para verificar a caixa de entrada. Certifique-se de que seu servidor de e-mail suporta SSL.

**Pasta de emails enviados com falha:** Especifica um diretório no qual armazenar resultados se o servidor de email SMTP não estiver operacional.

**assíncrono:** Quando definido como síncrono, todos os documentos de entrada são processados e uma única resposta é retornada. Quando definido como assíncrono, uma resposta é enviada para cada documento processado.

Por exemplo, um terminal de email é criado para um serviço que pega um único documento do Word e retorna esse documento como um arquivo PDF. Um email pode ser enviado para a caixa de entrada do ponto de extremidade que contém vários (3) documentos do Word. Quando todos os três documentos forem processados, se o endpoint estiver configurado como síncrono, um único email de resposta será enviado com todos os três documentos anexados. Se o endpoint for assíncrono, um email de resposta será enviado depois que cada documento do Word for convertido em PDF. O resultado são três emails, cada um com um único anexo PDF.

O valor padrão é assíncrono.

**Incluir o corpo do email original como um anexo:** Por padrão, ao enviar um email para o Forms Server, o texto original da mensagem é incluído no corpo dela. Para incluir o texto como um anexo, selecione essa opção.

**Usar a linha de assunto original para emails de resultado:** Por padrão, o servidor do Forms usa os valores especificados nas configurações Assunto do email de sucesso e Assunto do email de erro como a linha de assunto ao enviar as mensagens de email de resultado. Para usar a mesma linha de assunto do email original enviado ao servidor, selecione essa opção.

**Assunto do email de sucesso:** Depois de enviar um email a um endpoint de email para iniciar ou continuar um processo, você receberá uma mensagem de email de retorno do servidor do AEM Forms. Se o email for bem-sucedido, você receberá um email de sucesso. Se seu email falhar, você receberá um email de falha informando por que ele falhou. Essa configuração permite especificar a linha de assunto das mensagens de email de sucesso enviadas para esse endpoint.

**Corpo do email de sucesso:** Permite especificar o corpo de texto das mensagens de email de sucesso enviadas para esse endpoint.

**Erro no prefixo do assunto do email:** Permite especificar o texto usado no início da linha de assunto das mensagens de email de falha enviadas para esse endpoint.

**Assunto do email de erro:** Permite especificar a linha de assunto das mensagens de email de falha enviadas para este endpoint. Esse texto é exibido após o Prefixo do assunto do email de erro.

**Corpo do email de erro:** Permite especificar a primeira linha do corpo de texto das mensagens de email de falha enviadas para esse endpoint.

**Informações de resumo de email:** Cada mensagem de sucesso ou falha inclui uma seção contendo o texto original do email enviado ao Forms Server. Essa configuração especifica o texto que aparece acima dessa seção.

**Valide a Caixa de entrada antes de criar/atualizar este endpoint:** Quando essa opção é selecionada, o Forms Server verifica se as configurações SMTP/POP3 estão corretas antes de criar o endpoint. Quando você clica em Adicionar, é exibida uma mensagem informando se a conta da caixa de entrada é válida. Se essa opção não estiver selecionada, o AEM Forms Server criará o endpoint sem validar a caixa de entrada.

**Nome da operação:** Esta configuração é obrigatória. Uma lista de operações que podem ser atribuídas ao endpoint de email. A operação selecionada aqui determina quais campos são exibidos nas seções Mapeamentos de Parâmetro de Entrada e Mapeamentos de Parâmetro de Saída.

**Mapeamentos de parâmetros de entrada:** Usado para configurar a entrada necessária para processar o serviço e a operação. Os dois tipos de entrada são literal e variável:

**Literal:** O email usa o valor inserido no campo como é exibido.

**Variável:** Você pode mapear uma string a partir do assunto, corpo, cabeçalho ou endereço de email do remetente do email. Para fazer isso, use uma das seguintes palavras-chave: %SUBJECT%, %BODY%, %HEADER% ou %SENDER%. Por exemplo, se você usar %SUBJECT%, o conteúdo do assunto do email será usado como parâmetro de entrada. Para selecionar anexos, insira um padrão de arquivo que o terminal de email possa usar para selecionar os documentos anexados. Por exemplo, inserir &amp;ast;.pdf seleciona qualquer documento anexado que tenha uma extensão de nome de arquivo .pdf. Inserir &amp;ast; seleciona qualquer documento anexado. Inserir example.pdf seleciona qualquer documento anexado chamado example.pdf.

**Mapeamentos de Parâmetros de Saída:** Usado para configurar a saída do serviço e da operação. Os seguintes caracteres nos valores de mapeamento do parâmetro de saída são expandidos no nome do arquivo de anexo:

**% F** Representa o nome de arquivo do arquivo de origem (sem incluir uma extensão).

**% E** Representa a extensão do arquivo de origem.

Qualquer ocorrência da barra invertida (\) é substituída por %%.

***observação **: se a mensagem de solicitação de serviço incluir vários anexos de arquivo, você não poderá usar os parâmetros %F e %E para a propriedade Mapeamentos de Parâmetro de Saída do ponto de extremidade. Se a resposta do serviço retornar vários anexos de arquivo, você não poderá especificar o mesmo nome de arquivo para mais de um anexo. Se você não seguir essas recomendações, o serviço chamado criará os nomes dos arquivos retornados e os nomes não serão previsíveis.*

Os seguintes valores estão disponíveis:

**Objeto único:** O provedor de email não tem o destino da pasta de origem; os resultados são retornados como anexos. O padrão é Result/%F.ps e retorna Result%%sourcefilename.ps como o anexo de nome de arquivo.

**Lista:** O padrão é Resultado/%F/ e retorna Resultado%%sourcefilename%%file1 como o anexo de nome de arquivo.

**Mapa:** O padrão é Resultado/%F/ e o destino de origem é Resultado%%sourcefilename%%file1 e Resultado%%sourcefilename%%file2. Se o mapa contiver mais de um objeto e o padrão for Result/%F.ps, os anexos do arquivo de resposta serão Result%%sourcefilename1.ps (saída 1) e Result%%sourcefilename2.ps (saída 2).

## Criar um terminal de email para o serviço de Tarefa Concluída {#create-an-email-endpoint-for-the-complete-task-service}

Para que o fluxo de trabalho de formulários receba e manipule mensagens de email recebidas dos usuários, é necessário criar um terminal de email para o serviço Tarefa Completa.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de serviço, clique no serviço Concluir tarefa.
1. Na guia Endpoints, selecione Email na lista suspensa e clique em Adicionar.
1. Na caixa Host da caixa de entrada, digite o nome do host ou o endereço IP do servidor de e-mail.
1. Na caixa Usuário da caixa de entrada, digite o nome de usuário necessário para fazer logon na conta de email criada para lidar com envios de formulários. Dependendo do servidor de email e da configuração, esse nome pode ser apenas a parte do nome de usuário do email ou pode ser o endereço de email completo.
1. Na caixa Senha da caixa de entrada, digite a senha do usuário da caixa de entrada.
1. Na caixa Host SMTP, digite o nome do host ou o endereço IP do servidor de e-mail do qual o provedor de e-mail envia resultados e mensagens de erro.
1. Na caixa Usuário SMTP, digite a conta de usuário do provedor de email a ser usada ao enviar email para obter resultados e erros. Essa conta de usuário pode ter o mesmo valor usado para o Usuário da caixa de entrada.
1. Na caixa Senha SMTP, digite a senha da conta SMTP.
1. Na lista Nome da Operação, selecione chamar.
1. Na lista attachmentMap, selecione Variable e digite `*.*` na caixa adjacente. Isso envia todos os anexos das mensagens de email de entrada para uma variável de mapa para o processo Concluir tarefa.
1. Na lista mailBody, selecione a variável e o tipo `%BODY%` na caixa adjacente.
1. Na lista mailFrom, selecione Variável e digite `%SENDER%` na caixa adjacente. Isso mapeia o endereço do remetente para os dados do processo de Tarefa Concluída.
1. Na caixa de resultados, digite `results`. Isso faz com que Concluir Tarefa ou Iniciar Processo retorne uma string de resultados.
1. Clique em Adicionar.
