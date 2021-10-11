---
title: Configuração de pontos de extremidade de email
seo-title: Configuring email endpoints
description: Saiba como configurar pontos de extremidade de email.
seo-description: Learn how to configure email endpoints.
uuid: d47bb45b-0e0e-43ca-9e25-e347d0e60206
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dcf15c42-9ec6-4d1c-ad41-083aa0b8c7ae
exl-id: 33583a12-4f20-4146-baa4-c9854e454bbf
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '3757'
ht-degree: 0%

---

# Configuração de pontos de extremidade de email {#configuring-email-endpoints}

Os pontos de extremidade de email permitem que os usuários invoquem um serviço ao enviar um ou mais documentos (como anexos de email) para uma conta de email específica. A caixa de entrada do email atua como um ponto de coleta para os anexos. O serviço monitora a caixa de entrada e processa os anexos. Os resultados da conversão são encaminhados ao usuário definido no endpoint .

Para um endpoint de email, usuários autorizados podem invocar um processo ao enviar arquivos por email para a conta apropriada. Os resultados serão retornados ao usuário que enviou (por padrão) ou ao usuário definido nas configurações do ponto de extremidade.

Antes de configurar um ponto de extremidade de email, crie uma conta de email POP3 ou IMAP para uso pelo ponto de extremidade. Configure uma conta separada para cada tipo de conversão. Por exemplo, uma conta pode ser configurada para gerar documentos PDF padrão a partir de anexos de arquivos recebidos e outra conta pode ser configurada para gerar documentos PDF seguros.

>[!NOTE]
>
>Cada endereço de email deve mapear para apenas um ponto de extremidade de email. Não é possível configurar vários pontos de extremidade de email para um único endereço de email, mesmo que os pontos de extremidade de email adicionais estejam desativados.

Todos os pontos de extremidade de email são configurados com um nome de usuário autorizado e senha para a caixa de entrada de email, que são necessários ao chamar o serviço. A conta de email é protegida pelo sistema de servidor de email em que está configurada.

Se os usuários enviarem documentos com caracteres de idioma da Europa Ocidental em nomes de arquivo e caminho de conversão, eles deverão usar um aplicativo de email que ofereça suporte aos tipos de codificação necessários (Latin1 [ISO-8859-1], Western European [Windows] ou UTF-8). Para obter mais informações, consulte o documento *Instalando e Implantando formulários AEM* para seu servidor de aplicativos.

Antes de configurar um terminal de email, configure o serviço de Email . (Consulte [Definir configurações padrão de ponto de extremidade de email](configuring-email-endpoints.md#configure-default-email-endpoint-settings).) Os parâmetros de configuração do serviço de email têm dois objetivos:

* Para configurar atributos comuns a todos os pontos de extremidade de email
* Para fornecer valores padrão para todos os pontos de extremidade de email

## Configurar SSL para um endpoint de email {#configure-ssl-for-an-email-endpoint}

Você pode configurar POP3, IMAP ou SMTP para usar o SSL (Secure Sockets Layer) para um terminal de email.

1. No servidor de email, ative o SSL para POP3, IMAP ou SMTP de acordo com a documentação do fabricante.
1. Exportar um certificado de cliente do servidor de email.
1. Use o programa keytool para importar o arquivo de certificado do cliente para o armazenamento de certificado Java Virtual Machine (JVM) do servidor de aplicativos. O procedimento para esta etapa dependerá dos caminhos de instalação da JVM e do cliente.

   Por exemplo, se estiver usando uma instalação padrão do Oracle WebLogic Server com JDK 1.5.0 no Microsoft Windows Server® 2003, digite o seguinte texto em um prompt de comando:

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. Quando solicitado, insira a senha (para Java, a senha padrão é `changeit`). Você receberá uma mensagem informando que o certificado foi importado com êxito.
1. Use o console de administração para adicionar o terminal de email ao serviço.
1. Crie o endpoint de email no console de administração. Ao definir as configurações do ponto de extremidade, selecione POP3/IMAP SSL Enabled for incoming messages e SMTP SSL Enabled for outgoing messages, e altere as propriedades da porta de acordo.

>[!NOTE]
>
>Dica: Em caso de problemas ao usar o SSL, use um cliente de email, como o Microsoft Outlook, para verificar se ele pode acessar o servidor de email usando SSL. Se o cliente de email não conseguir acessar o servidor de email, o problema estará relacionado à configuração do seu certificado ou do seu servidor de email.

## Definir configurações padrão de ponto de extremidade de email {#configure-default-email-endpoint-settings}

Você pode usar a página Gerenciamento de serviço para configurar atributos comuns a todos os pontos de extremidade de email e fornecer valores padrão para todos os pontos de extremidade de email.

Para que o fluxo de trabalho de formulários receba e manipule mensagens de email recebidas dos usuários, é necessário criar um terminal de email para o serviço Tarefa completa. Este ponto de extremidade de email requer configurações adicionais, conforme descrito em [Criar um ponto de extremidade de email para o serviço de Tarefa completa](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service).

### Alterar os valores padrão de pontos de extremidade de email {#change-the-default-values-for-email-endpoints}

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Serviços.
1. Na página Gerenciamento de serviços , clique em Email: 1.0 (a ID do componente é com.adobe.idp.dsc.provider.service.email.Email).
1. Na guia Configuração, especifique as configurações padrão de ponto de extremidade de email e clique em Salvar.

### Configurações padrão de ponto de extremidade de email {#default-email-endpoint-settings}

**Expressão Cron:** A expressão cron usada pelo quartzo para agendar a pesquisa do diretório de entrada.

**Intervalo de repetição:** o número de vezes que a pesquisa de diretório é repetida. O intervalo de repetição padrão é em segundos, se esse valor não for especificado na configuração do ponto de extremidade. O valor padrão é 10. Este valor não pode ser inferior a 10.

**Contagem de repetição:** o número de vezes em que o diretório de entrada é pesquisado. A contagem de repetição padrão a ser usada se esse valor não for especificado na configuração de ponto de extremidade. Um valor de -1 indica a verificação indefinida do diretório. O valor padrão é -1.

**Delay when job starts:** O valor padrão, em segundos, do atraso antes que o job comece a verificar o terminal. O valor padrão é 0.

**Tamanho do lote:** O número de emails que o receptor processa por varredura para obter desempenho ideal. Um valor de -1 indica todos os emails. O valor padrão é 2.

**Assíncrono:** identifica o tipo de invocação como assíncrona ou síncrona. Processos transitórios e síncronos só podem ser invocados de forma síncrona. O valor padrão é assíncrono.

**Padrão de domínio:** o padrão de nome de domínio usado para filtrar emails de entrada. Por exemplo, se adobe.com for usado, somente o email de adobe.com será processado; o email de outros domínios é ignorado.

**Padrão de arquivo:** os padrões de anexo de arquivo de entrada aceitos pelo provedor. Isso inclui arquivos com extensões específicas (&amp;ast;.dat, &amp;ast;.xml), nomes específicos (dados) e expressões compostas no nome e na extensão (.[dD][aA]&#39;port&#39;). O valor padrão é &amp;ast;.&amp;ast;.

**Recipients do trabalho bem-sucedido:** um ou mais endereços de email usados para enviar emails para indicar trabalhos bem-sucedidos. Por padrão, uma mensagem de trabalho bem-sucedida é sempre enviada ao remetente do trabalho inicial. Há suporte para até 100 recipients. Para desativar essa configuração, deixe este campo em branco.

**Recipients do trabalho com falha:** um ou mais endereços de email usados para enviar emails para indicar trabalhos com falha. Por padrão, uma mensagem de trabalho com falha é sempre enviada ao remetente que enviou o trabalho inicial. Há suporte para até 100 recipients. Para desativar essa configuração, deixe este campo em branco.

**Host da caixa de entrada:** o nome do host da caixa de entrada ou o endereço IP do provedor de email a ser verificado.

**Porta da Caixa de entrada:** o número da porta da caixa de entrada do provedor de email a ser verificado. Se o valor for 0, a porta IMAP ou POP3 padrão será usada.

**Protocolo da caixa de entrada:** o protocolo de email do ponto de extremidade do email a ser usado para digitalizar a caixa de entrada. As opções são IMAP ou POP3. O servidor de correio do host da caixa de entrada deve oferecer suporte a esses protocolos.

**Tempo limite da caixa de entrada:** especifica o tempo que o ponto de extremidade aguardará antes de ser cancelado ao tentar se conectar à caixa de entrada. Se uma conexão não for adquirida antes do valor de tempo limite ser atingido, a caixa de entrada não será sondada.

**Usuário da caixa de entrada:** o nome de usuário necessário para fazer logon na conta de email. Dependendo do servidor de email e da configuração, esse nome pode ser apenas a parte do nome de usuário do email ou pode ser o endereço de email completo.

**Senha da Caixa de Entrada:** A senha do usuário da Caixa de Entrada.

**SSL POP3/IMAP Habilitado:** Quando selecionado, habilita o SSL.

**Host SMTP:** o nome do host do servidor de email que o provedor de email usa para enviar resultados e mensagens de erro. Por exemplo, mail.example.com

**Porta SMTP:** A porta usada para se conectar ao servidor de email. O valor padrão é 25.

**Usuário SMTP:** A conta de usuário para o provedor de email usar quando enviar email para resultados e erros.

**Senha SMTP:** A senha da conta SMTP. Alguns servidores de email não exigem uma senha SMTP.

**Enviar de:** o endereço de email (por exemplo, user@company.com) usado para enviar notificações por email de resultados e erros. Se você não especificar um valor Enviar de , o servidor de email tentará determinar o endereço de email combinando o valor especificado na configuração Usuário SMTP com um domínio padrão configurado no servidor de email. Se o servidor de email não tiver um domínio padrão e você não especificar um valor para Enviar de, poderão ocorrer erros. Para garantir que as mensagens de email tenham o endereço de origem correto, especifique um valor para a configuração Enviar de .

**SSL SMTP ativado:** quando selecionado, ativa o SSL sobre SMTP.

**Incluir o corpo do email original como um anexo:** por padrão, ao enviar um email para o servidor de formulários, o texto original da mensagem é incluído no corpo da mensagem. Para incluir o texto como anexo, selecione essa opção.

**Usar a linha de assunto original para emails de resultado:** por padrão, o servidor do Forms usa os valores especificados nas configurações Assunto do email de sucesso e Assunto do email de erro como a linha de assunto ao enviar mensagens de email de resultado. Para usar a mesma linha de assunto do email original enviado ao servidor, selecione essa opção.

**Assunto do email de sucesso:** depois de enviar um email para um terminal de email para iniciar ou continuar um processo, você recebe uma mensagem de email de retorno do servidor de formulários de AEM. Se o email for bem-sucedido, você receberá um email bem-sucedido. Se o email falhar, você receberá um email de falha informando por que ele falhou. Essa configuração permite especificar a linha de assunto das mensagens de email de sucesso enviadas para esse terminal.

**Corpo do email de sucesso:** permite especificar o texto do corpo das mensagens de email de sucesso enviadas para esse ponto de extremidade.

**Prefixo de assunto do email de erro:** permite especificar o texto usado no início da linha de assunto das mensagens de email de falha enviadas para esse ponto de extremidade.

**Assunto do email de erro:** permite especificar a linha de assunto das mensagens de email de falha enviadas para esse terminal. Este texto é exibido após o Prefixo de assunto do email de erro.

**Corpo do email de erro:** permite especificar a primeira linha no texto do corpo das mensagens de email de falha enviadas para esse terminal.

**Informações de resumo de email:** cada mensagem de sucesso ou falha inclui uma seção que contém o texto original do email enviado ao servidor de formulários. Essa configuração especifica o texto que aparece acima dessa seção.

**Validar Caixa de Entrada Antes de Criar/Atualizar Esse Ponto de Extremidade:**  Quando essa opção é selecionada, o servidor de formulários verifica se as configurações de SMTP/POP3 estão corretas antes de criar o ponto de extremidade. Ao clicar em Adicionar, uma mensagem é exibida informando se a conta da caixa de entrada é válida. Se essa opção não estiver selecionada, o servidor do AEM forms criará o ponto de extremidade sem validar a caixa de entrada.

**Codificação do conjunto de caracteres:** o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários em um ambiente japonês podem escolher ISO2022-JP.

**Pasta Enviada por Email com Falha:** Especifica um diretório no qual armazenar resultados se o servidor de email SMTP não estiver operacional.

## Configurações do ponto de extremidade de email {#email-endpoint-settings}

Use as configurações a seguir para configurar um ponto de extremidade de email.

**Nome:** uma configuração obrigatória que identifica o ponto de extremidade. Não inclua um caractere &lt; porque ele trunca o nome exibido no Workspace. Se estiver inserindo um URL como o nome do ponto de extremidade, verifique se ele está em conformidade com as regras de sintaxe especificadas na RFC1738.

**Descrição:** Uma descrição do ponto de extremidade. Não inclua um caractere &lt; porque ele trunca a descrição exibida no Workspace.

**Expressão de Cron:** insira uma expressão de cron se o email precisar ser agendado com o uso de uma expressão de cron.

**Contagem de repetição:** Número de vezes que o ponto de extremidade do email verifica a pasta ou o diretório. Um valor de -1 indica varredura indefinida. O valor padrão é -1.

**Intervalo de repetição:** a taxa de varredura que o receptor usa para verificar emails recebidos.

**Atraso no início do trabalho:** o tempo de espera para a verificação após o agendador começar.

**Tamanho do lote:** O número de emails que o receptor processa por varredura para obter desempenho ideal. Um valor de -1 indica todos os emails. O valor padrão é 2.

**Nome do usuário:** uma configuração obrigatória, que é o nome de usuário usado ao chamar um serviço de direcionamento do email. O valor padrão é SuperAdmin.

**Nome do domínio:** uma configuração obrigatória, que é o domínio do usuário. O valor padrão é DefaultDom.

**Padrão de domínio:** Especifica os padrões de domínio do email de entrada que o provedor aceita. Por exemplo, se adobe.com for usado, somente o email de adobe.com será processado; o email de outros domínios é ignorado.

**Padrão de arquivo:** Especifica os padrões de anexo de arquivo de entrada aceitos pelo provedor. Isso inclui arquivos com extensões específicas (&amp;ast;.dat, &amp;ast;.xml), nomes específicos (dados) ou expressões compostas no nome e na extensão (&amp;ast;.[dD][aA]&#39;port&#39;).

**Recipients do trabalho bem-sucedido:** um endereço de email para o qual são enviadas mensagens para indicar trabalhos bem-sucedidos. Por padrão, uma mensagem de trabalho bem-sucedida é sempre enviada ao remetente. Se você digitar o remetente, os resultados do email serão enviados ao remetente. Há suporte para até 100 recipients. Especifique recipients adicionais com endereços de email, separados por vírgulas (,).

Para desativar esta configuração, deixe a configuração em branco. Em alguns casos, você deseja acionar um processo e não desejar uma notificação por email do resultado.

**Recipients do trabalho com falha:** um endereço de email para o qual são enviadas mensagens para indicar trabalhos com falha. Por padrão, uma mensagem de trabalho com falha é sempre enviada ao remetente. Se você digitar o remetente, os resultados do email serão enviados ao remetente. Há suporte para até 100 recipients. Especifique recipients adicionais com endereços de email, separados por vírgulas (,).

Para desativar esta configuração, deixe a configuração em branco. Em alguns casos, você deseja acionar um processo e não desejar uma notificação por email do resultado.

**Host da caixa de entrada:** o nome do host da caixa de entrada ou o endereço IP do provedor de email a ser verificado.

**Porta da caixa de entrada:** a porta que o servidor de email usa. O valor padrão para POP3 é 110 e o valor padrão para IMAP é 143. Se SSL estiver ativado, o valor padrão para POP3 é 995 e o valor padrão para IMAP é 993.

**Protocolo da caixa de entrada:** o protocolo de email do ponto de extremidade do email a ser usado para digitalizar a caixa de entrada. Os valores são IMAP ou POP3. O servidor de correio do host da caixa de entrada deve oferecer suporte a esses protocolos.

**Tempo limite da caixa de entrada:** o tempo limite, em segundos, para o provedor de email aguardar as respostas da caixa de entrada.

**Usuário da caixa de entrada:** o nome de usuário necessário para fazer logon na conta de email. Dependendo do servidor de email e da configuração, esse valor pode ser apenas a parte do nome do usuário do email ou pode ser o endereço de email completo.

**Senha da caixa de entrada:** a senha do usuário da caixa de entrada.

**POP3/IMAP SSL ativado:** selecione essa configuração para forçar o provedor de email a usar SSL para digitalizar a caixa de entrada. Certifique-se de que o seu servidor de correio suporta SSL.

**Host SMTP:** o nome do host do servidor de email que o provedor de email usa para enviar resultados e mensagens de erro.

**Porta SMTP:** O valor padrão para a porta SMTP é 25.

**Usuário SMTP:** A conta de usuário para o provedor de email usar ao enviar notificações por email de resultados e erros.

**Senha SMTP:** A senha da conta SMTP. Alguns servidores de email não exigem uma senha SMTP.

**Enviar de:** o endereço de email (por exemplo, user@company.com) usado para enviar notificações por email de resultados e erros. Se você não especificar um valor Enviar de , o servidor de email tentará determinar o endereço de email combinando o valor especificado na configuração Usuário SMTP com um domínio padrão configurado no servidor de email. Se o servidor de email não tiver um domínio padrão e você não especificar um valor para Enviar de, poderão ocorrer erros. Para garantir que as mensagens de email tenham o endereço de origem correto, especifique um valor para a configuração Enviar de .

**SSL SMTP habilitado:** selecione essa configuração para forçar o provedor de email a usar SSL para digitalizar a caixa de entrada. Certifique-se de que o seu servidor de correio suporta SSL.

**Pasta Enviada por Email com Falha:** Especifica um diretório no qual armazenar resultados se o servidor de email SMTP não estiver operacional.

**assíncrono:** quando definido como síncrono, todos os documentos de entrada são processados e uma única resposta é retornada. Quando definido como assíncrono, uma resposta será enviada para cada documento processado.

Por exemplo, um ponto de extremidade de email é criado para um serviço que utiliza um único documento do Word e retorna esse documento como um arquivo PDF. Um email pode ser enviado para a caixa de entrada do ponto de extremidade que contém vários (3) documentos do Word. Quando todos os três documentos são processados, se o endpoint estiver configurado como síncrono, um único email de resposta é enviado com todos os três documentos anexados. Se o endpoint for assíncrono, um email de resposta será enviado depois que cada documento do Word for convertido em PDF. O resultado são três emails, cada um com um único anexo de PDF.

O valor padrão é assíncrono.

**Inclua o corpo do email original como um anexo:** por padrão, ao enviar um email para o servidor de formulários, o texto original da mensagem é incluído no corpo da mensagem. Para incluir o texto como anexo, selecione essa opção.

**Use a linha de assunto original para emails de resultado:** Por padrão, o servidor do Forms usa os valores especificados nas configurações Assunto do email de sucesso e Assunto do email de erro como a linha de assunto ao enviar mensagens de email de resultado. Para usar a mesma linha de assunto do email original enviado ao servidor, selecione essa opção.

**Assunto do email de sucesso:** depois de enviar um email para um terminal de email para iniciar ou continuar um processo, você recebe uma mensagem de email de retorno do servidor de formulários de AEM. Se o email for bem-sucedido, você receberá um email bem-sucedido. Se o email falhar, você receberá um email de falha informando por que ele falhou. Essa configuração permite especificar a linha de assunto das mensagens de email de sucesso enviadas para esse terminal.

**Corpo do email de sucesso:** permite especificar o texto do corpo das mensagens de email de sucesso enviadas para esse ponto de extremidade.

**Prefixo de assunto do email de erro:** permite especificar o texto usado no início da linha de assunto das mensagens de email de falha enviadas para esse ponto de extremidade.

**Assunto do email de erro:** permite especificar a linha de assunto das mensagens de email de falha enviadas para esse terminal. Este texto é exibido após o Prefixo de assunto do email de erro.

**Corpo do email de erro:** permite especificar a primeira linha no texto do corpo das mensagens de email de falha enviadas para esse terminal.

**Informações de resumo de email:** cada mensagem de sucesso ou falha inclui uma seção que contém o texto original do email enviado ao servidor de formulários. Essa configuração especifica o texto que aparece acima dessa seção.

**Validar a Caixa de entrada antes de criar/atualizar esse ponto de extremidade:**  quando essa opção é selecionada, o servidor de formulários verifica se as configurações de SMTP/POP3 estão corretas antes de criar o ponto de extremidade. Ao clicar em Adicionar, uma mensagem é exibida informando se a conta da caixa de entrada é válida. Se essa opção não estiver selecionada, o servidor do AEM forms criará o ponto de extremidade sem validar a caixa de entrada.

**Nome da operação:** essa configuração é obrigatória. Uma lista de operações que podem ser atribuídas ao ponto de extremidade do email. A operação selecionada aqui determina quais campos são exibidos nas seções Mapeamentos do parâmetro de entrada e Mapeamentos do parâmetro de saída .

**Mapeamentos do parâmetro de entrada:** usados para configurar a entrada necessária para processar o serviço e a operação. Os dois tipos de entrada são literal e variável:

**Literal:** o email usa o valor inserido no campo, conforme ele é exibido.

**Variável:** é possível mapear uma sequência de caracteres do assunto do email, do corpo, do cabeçalho ou do endereço de email do remetente. Para fazer isso, use uma das seguintes palavras-chave: %SUBJECT%, %BODY%, %HEADER% ou %SENDER%. Por exemplo, se você usar %SUBJECT%, o conteúdo do assunto do email será usado como parâmetro de entrada. Para selecionar anexos, insira um padrão de arquivo que o ponto de extremidade de email possa usar para selecionar os documentos anexados. Por exemplo, inserir &amp;ast;.pdf seleciona qualquer documento anexado que tenha uma extensão de nome de arquivo .pdf. Entrando no &amp;ast; seleciona qualquer documento anexado. Inserir example.pdf seleciona qualquer documento anexado chamado example.pdf.

**Mapeamentos de parâmetros de saída:** usados para configurar a saída do serviço e da operação. Os seguintes caracteres nos valores de mapeamento do parâmetro de saída são expandidos no nome do arquivo do anexo:

**%** FRrepresenta o nome de arquivo do arquivo de origem (sem incluir uma extensão).

**%** EReforma a extensão do arquivo de origem.

Qualquer ocorrência da barra invertida (\) é substituída por %%.

***observação **: Se a mensagem de solicitação de serviço incluir vários anexos de arquivo, você não poderá usar os parâmetros %F e %E para a propriedade Mapeamentos de Parâmetro de Saída do ponto de extremidade. Se a resposta dos serviços retornar vários anexos de arquivo, não será possível especificar o mesmo nome de arquivo para mais de um anexo. Se você não seguir essas recomendações, o serviço chamado criará os nomes para os arquivos retornados e os nomes não serão previsíveis.*

Os seguintes valores estão disponíveis:

**Objeto único:** O provedor de email não tem o destino da pasta de origem; os resultados são retornados como anexos. O padrão é Result/%F.ps e retorna Result%%sourcefilename.ps como o anexo do nome de arquivo.

**Lista:** o padrão é Result/%F/ e retorna Result%%sourcefilename%%file1 como o anexo do nome de arquivo.

**Mapa:** O padrão é Resultado/%F/ e o destino de origem é Resultado%%sourcefilename%%file1 e Resultado%%sourcefilename%%file2. Se o mapa contiver mais de um objeto e o padrão for Result/%F.ps, os anexos do arquivo de resposta serão Result%%sourcefilename1.ps (output 1) e Result%%sourcefilename2.ps (output 2).

## Criar um terminal de email para o serviço Concluir tarefa {#create-an-email-endpoint-for-the-complete-task-service}

Para que o fluxo de trabalho de formulários receba e manipule mensagens de email recebidas dos usuários, é necessário criar um terminal de email para o serviço Tarefa completa.

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Serviços.
1. Na página Gerenciamento de Serviço, clique no serviço Concluir Tarefa.
1. Na guia Endpoints , selecione Email na lista suspensa e clique em Adicionar.
1. Na caixa Host da caixa de entrada, digite o nome do host ou endereço IP do servidor de email.
1. Na caixa Usuário da caixa de entrada, digite o nome de usuário necessário para fazer logon na conta de email criada para lidar com envios de formulários. Dependendo do servidor de email e da configuração, esse nome pode ser apenas a parte do nome do usuário do email ou pode ser o endereço de email completo.
1. Na caixa Senha da Caixa de Entrada, digite a senha do Usuário da Caixa de Entrada.
1. Na caixa Host SMTP, digite o nome do host ou endereço IP do servidor de email do qual o provedor de email envia resultados e mensagens de erro.
1. Na caixa Usuário SMTP, digite a conta de usuário para o provedor de email usar quando enviar email para resultados e erros. Essa conta de usuário pode ser o mesmo valor usado para o Usuário da Caixa de Entrada.
1. Na caixa Senha SMTP, digite a senha da conta SMTP.
1. Na lista Nome da Operação, selecione invocar.
1. Na lista attachmentMap , selecione Variável e digite `*.*` na caixa adjacente. Isso envia todos os anexos das mensagens de email de entrada para uma variável de mapa do processo Concluir tarefa.
1. Na lista mailBody, selecione a variável e digite `%BODY%` na caixa adjacente.
1. Na lista mailFrom, selecione Variable e digite `%SENDER%` na caixa adjacente. Isso mapeia o endereço do remetente para os dados do processo Concluir tarefa.
1. Na caixa de resultados, digite `results`. Isso faz com que a tarefa Concluir ou Iniciar processo retorne uma string de resultado.
1. Clique em Adicionar.
