---
title: Configuração de pontos de extremidade de email
seo-title: Configuração de pontos de extremidade de email
description: Saiba como configurar pontos de extremidade de email.
seo-description: Saiba como configurar pontos de extremidade de email.
uuid: d47bb45b-0e0e-43ca-9e25-e347d0e60206
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dcf15c42-9ec6-4d1c-ad41-083aa0b8c7ae
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configuração de pontos de extremidade de email {#configuring-email-endpoints}

Os pontos de extremidade de e-mail permitem que os usuários chamem um serviço enviando um ou mais documentos (como anexos de e-mail) para uma conta de e-mail especificada. A caixa de entrada de email atua como um ponto de coleta para os anexos. O serviço monitora a caixa de entrada e processa os anexos. Os resultados da conversão são encaminhados ao usuário definido no ponto final.

Para um terminal de email, os usuários autorizados podem invocar um processo enviando arquivos por email para a conta apropriada. Os resultados serão retornados para o usuário que envia (por padrão) ou para o usuário definido nas configurações de ponto de extremidade.

Antes de configurar um terminal de email, crie uma conta de email POP3 ou IMAP para uso pelo terminal. Configure uma conta separada para cada tipo de conversão. Por exemplo, uma conta pode ser configurada para gerar documentos PDF padrão a partir de anexos de arquivos recebidos e outra conta pode ser configurada para gerar documentos PDF seguros.

>[!NOTE]
>
>Cada endereço de email deve mapear somente para um terminal de email. Não é possível configurar vários pontos de extremidade de email para um único endereço de email, mesmo que os pontos de extremidade de email adicionais estejam desativados.

Todos os pontos de extremidade de e-mail são configurados com um nome de usuário e senha autorizados para a caixa de entrada de e-mail, que são necessários ao chamar o serviço. A conta de email é protegida pelo sistema do servidor de email no qual está configurada.

Se os usuários enviarem documentos com caracteres de idioma da Europa Ocidental em nomes de arquivos e caminhos de conversão, eles deverão usar um aplicativo de email que suporte os tipos de codificação necessários (Latin1 [ISO-8859-1], Western European [Windows]ou UTF-8). Para obter mais informações, consulte o documento *Instalar e implantar formulários* AEM para seu servidor de aplicativos.

Antes de configurar um terminal de e-mail, configure o serviço de e-mail. (Consulte [Definir configurações](configuring-email-endpoints.md#configure-default-email-endpoint-settings)padrão de ponto de extremidade de email.) Os parâmetros de configuração do serviço de email têm dois objetivos:

* Para configurar atributos comuns a todos os pontos de extremidade de email
* Para fornecer valores padrão para todos os pontos finais de email

## Configurar o SSL para um terminal de email {#configure-ssl-for-an-email-endpoint}

Você pode configurar POP3, IMAP ou SMTP para usar SSL (Secure Sockets Layer) para um terminal de email.

1. No servidor de email, ative SSL para POP3, IMAP ou SMTP de acordo com a documentação do fabricante.
1. Exporte um certificado de cliente do servidor de email.
1. Use o programa keytool para importar o arquivo de certificado do cliente para o repositório de certificados Java Virtual Machine (JVM) do servidor de aplicativos. O procedimento para esta etapa dependerá dos caminhos de instalação do JVM e do cliente.

   Por exemplo, se você estiver usando uma instalação padrão do Oracle WebLogic Server com JDK 1.5.0 no Microsoft Windows Server® 2003, digite o seguinte texto em um prompt de comando:

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. Quando solicitado, digite a senha (para Java, a senha padrão é `changeit`). Você receberá uma mensagem informando que o certificado foi importado com êxito.
1. Use o console de administração para adicionar o terminal de email ao serviço.
1. Crie o terminal de email no console de administração. Ao definir as configurações do ponto de extremidade, selecione SSL POP3/IMAP Ativado para mensagens de entrada e SSL SMTP Ativado para mensagens de saída e altere as propriedades da porta de acordo.

>[!NOTE]
>
>Dica: Se tiver problemas ao usar SSL, use um cliente de email como o Microsoft Outlook para verificar se ele pode acessar o servidor de email usando SSL. Se o cliente de e-mail não puder acessar o servidor de e-mail, o problema está relacionado à configuração do seu certificado ou do seu servidor de e-mail.

## Definir configurações padrão de ponto de extremidade de email {#configure-default-email-endpoint-settings}

Você pode usar a página Gerenciamento de serviços para configurar atributos comuns a todos os pontos de extremidade de email e fornecer valores padrão para todos os pontos de extremidade de email.

Para que o fluxo de trabalho de formulários receba e manipule mensagens de email recebidas de usuários, é necessário criar um terminal de email para o serviço de Tarefa completa. Esse terminal de email requer configurações adicionais, conforme descrito em [Criar um terminal de email para o serviço](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)de Tarefa completa.

### Alterar os valores padrão para pontos de extremidade de email {#change-the-default-values-for-email-endpoints}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de serviços, clique em Email: 1.0 (a ID do componente é com.adobe.idp.dsc.provider.service.email.Email).
1. Na guia Configuração, especifique as configurações padrão de ponto de extremidade de email e clique em Salvar.

### Configurações de ponto de extremidade de email padrão {#default-email-endpoint-settings}

**Expressão do cron:** A expressão cron como usada pelo quartzo para agendar a pesquisa do diretório de entrada.

**Intervalo de repetição:** O número de vezes que a pesquisa de diretório é repetida. O intervalo de repetição padrão é em segundos se esse valor não for especificado na configuração do ponto de extremidade. O valor padrão é 10. Este valor não pode ser inferior a 10.

**Contagem de repetição:** O número de vezes que o diretório de entrada é pesquisado. A contagem de repetição padrão a ser usada se esse valor não for especificado na configuração do ponto de extremidade. Um valor de -1 indica uma varredura indefinida do diretório. O valor padrão é -1.

**Atraso quando o trabalho for start:** O valor padrão, em segundos, para o atraso antes dos start do trabalho para digitalizar o terminal. O valor padrão é 0.

**Tamanho do lote:** O número de emails que o receptor processa por varredura para obter um desempenho ótimo. O valor -1 indica todos os emails. O valor padrão é 2.

**Assíncrono:** Identifica o tipo de invocação como assíncrono ou síncrono. Processos transitórios e síncronos só podem ser chamados de forma síncrona. O valor padrão é assíncrono.

**Padrão de domínio:** O padrão de nome de domínio usado para filtrar emails recebidos. Por exemplo, se adobe.com for usado, somente o email do adobe.com será processado; o email de outros domínios é ignorado.

**Padrão de arquivo:** Os padrões de anexo de arquivo de entrada aceitos pelo provedor. Isso inclui arquivos com extensões específicas (&amp;ast;.dat, &amp;ast;.xml), nomes específicos (dados) e expressões compostas no nome e na extensão (.[dD][aA]&#39;port&#39;). O valor padrão é &amp;ast;.&amp;ast;.

**Recipient de trabalho bem-sucedidos:** Um ou mais endereços de email usados para enviar emails para indicar trabalhos bem-sucedidos. Por padrão, uma mensagem de trabalho bem-sucedida é sempre enviada ao remetente do trabalho inicial. Há suporte para até 100 recipient. Para desativar esta configuração, deixe este campo em branco.

**Recipient de trabalho com falha:** Um ou mais endereços de email usados para enviar emails para indicar trabalhos com falha. Por padrão, uma mensagem de falha de trabalho é sempre enviada ao remetente que enviou o trabalho inicial. Há suporte para até 100 recipient. Para desativar esta configuração, deixe este campo em branco.

**Host da Caixa de Entrada:** O nome do host da caixa de entrada ou o endereço IP do provedor de email a ser verificado.

**Porta da caixa de entrada:** O número da porta da caixa de entrada para que o provedor de email possa digitalizar. Se o valor for 0, a porta padrão IMAP ou POP3 será usada.

**Protocolo da caixa de entrada:** O protocolo de email do terminal de email a ser usado para digitalizar a caixa de entrada. As opções são IMAP ou POP3. O servidor de correio do host da caixa de entrada deve suportar esses protocolos.

**Tempo limite da caixa de entrada:** Especifica o tempo que o ponto de extremidade aguardará antes de cancelar ao tentar se conectar à caixa de entrada. Se uma conexão não for adquirida antes de o valor de tempo limite ser atingido, a caixa de entrada não será sondada.

**Usuário da Caixa de Entrada:** O nome de usuário necessário para fazer logon na conta de email. Dependendo do servidor de e-mail e da configuração, esse nome pode ser apenas a parte do nome do usuário do e-mail ou pode ser o endereço de e-mail completo.

**Senha da caixa de entrada:** A senha para o usuário da Caixa de entrada.

**SSL POP3/IMAP ativado:** Quando selecionada, ativa SSL.

**Host SMTP:** O nome de host do servidor de email que o provedor usa para enviar resultados e mensagens de erro. Por exemplo, mail.corp.example.com.

**Porta SMTP:** A porta usada para conectar-se ao servidor de email. O valor padrão é 25.

**Usuário SMTP:** A conta de usuário que o provedor de email deve usar ao enviar emails para obter resultados e erros.

**Senha SMTP:** A senha da conta SMTP. Alguns servidores de email não exigem uma senha SMTP.

**Enviar de:** O endereço de email (por exemplo, user@company.com) usado para enviar notificações por email de resultados e erros. Se você não especificar um valor Enviar de, o servidor de email tentará determinar o endereço de email combinando o valor especificado na configuração Usuário SMTP com um domínio padrão configurado no servidor de email. Se o servidor de e-mail não tiver um domínio padrão e você não especificar um valor para Enviar de, podem ocorrer erros. Para garantir que as mensagens de e-mail tenham o endereço de origem correto, especifique um valor para a configuração Enviar de.

**SSL SMTP Habilitado:** Quando selecionada, ativa SSL sobre SMTP.

**Inclua O Corpo De Email Original Como Um Anexo:** Por padrão, quando você envia um email para o servidor de formulários, o texto original da mensagem é incluído no corpo da mensagem. Para incluir o texto como anexo, selecione essa opção.

**Use A Linha De Assunto Original Para Emails De Resultado:** Por padrão, o servidor do Forms usa os valores especificados nas configurações Assunto do email de sucesso e Assunto do email de erro como a linha de assunto ao enviar mensagens de email de resultado. Para, em vez disso, usar a mesma linha de assunto que o email original enviado para o servidor, selecione essa opção.

**Assunto do email de sucesso:** Depois de enviar um email para um terminal de email para o start ou continuar um processo, você receberá uma mensagem de email de retorno do servidor de formulários do AEM. Se seu email for bem-sucedido, você receberá um email de sucesso. Se seu email falhar, você receberá um email com falha informando por que ele falhou. Essa configuração permite especificar a linha de assunto das mensagens de email de sucesso enviadas para esse terminal.

**Corpo de email de sucesso:** Permite que você especifique o texto do corpo das mensagens de email de sucesso enviadas para este terminal.

**Prefixo de assunto do email de erro:** Permite que você especifique o texto usado no início da linha de assunto das mensagens de e-mail de falha enviadas para este terminal.

**Assunto do email de erro:** Permite que você especifique a linha de assunto das mensagens de e-mail de falha enviadas para este terminal. Esse texto é exibido após o Prefixo de assunto do email de erro.

**Corpo do email de erro:** Permite que você especifique a primeira linha no texto do corpo das mensagens de e-mail de falha enviadas para esse terminal.

**Informações de resumo do email:** Cada mensagem de sucesso ou falha inclui uma seção que contém o texto original do email enviado para o servidor de formulários. Essa configuração especifica o texto que aparece acima dessa seção.

**Validar Caixa De Entrada Antes De Criar/Atualizar Este Ponto Final:** Quando essa opção é selecionada, o servidor de formulários verifica se as configurações de SMTP/POP3 estão corretas antes da criação do terminal. Quando você clica em Adicionar, uma mensagem é exibida informando se a conta da caixa de entrada é válida. Se essa opção não estiver selecionada, o servidor de formulários AEM criará o terminal sem validar a caixa de entrada.

**Codificação do conjunto de caracteres:** O formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários em um ambiente japonês podem escolher ISO2022-JP.

**Pasta Enviada por Email com Falha:** Especifica um diretório no qual armazenar resultados se o servidor de correio SMTP não estiver operacional.

## Configurações de ponto de extremidade de email {#email-endpoint-settings}

Use as seguintes configurações para configurar um ponto de extremidade de email.

**Nome:** Uma configuração obrigatória que identifica o ponto final. Não inclua um caractere &lt; porque ele trava o nome exibido no Workspace. Se você estiver inserindo um URL como o nome do ponto de extremidade, verifique se ele está em conformidade com as regras de sintaxe especificadas em RFC1738.

**Descrição:** Uma descrição do terminal. Não inclua um caractere &lt; porque ele trava a descrição exibida no Workspace.

**Expressão do cron:** Digite uma expressão cron se o email precisar ser programado usando uma expressão cron.

**Contagem de repetição:** Número de vezes que o ponto de extremidade de email verifica a pasta ou o diretório. Um valor de -1 indica uma varredura indefinida. O valor padrão é -1.

**Intervalo de repetição:** A taxa de varredura que o receptor usa para verificar a entrada de emails.

**Atraso quando o trabalho for start:** O tempo de espera para digitalizar após os start do scheduler.

**Tamanho do lote:** O número de emails que o receptor processa por varredura para obter um desempenho ótimo. O valor -1 indica todos os emails. O valor padrão é 2.

**Nome do usuário:** Uma configuração obrigatória, que é o nome de usuário usado ao chamar um serviço de público alvo do email. O valor padrão é SuperAdmin.

**Nome do domínio:** Uma configuração obrigatória, que é o domínio do usuário. O valor padrão é DefaultDom.

**Padrão de domínio:** Especifica os padrões de domínio do email recebido que o provedor aceita. Por exemplo, se adobe.com for usado, somente o email do adobe.com será processado; o email de outros domínios é ignorado.

**Padrão de arquivo:** Especifica os padrões de anexo de arquivo de entrada aceitos pelo provedor. Isso inclui arquivos com extensões específicas (&amp;ast;.dat, &amp;ast;.xml), nomes específicos (dados) ou expressões compostas no nome e extensão (&amp;ast;.[dD][aA]&#39;port&#39;).

**Recipient de trabalho bem-sucedidos:** Um endereço de email para o qual as mensagens são enviadas para indicar trabalhos bem-sucedidos. Por padrão, uma mensagem de trabalho bem-sucedida é sempre enviada ao remetente. Se você digitar remetente, os resultados do email serão enviados para o remetente. Há suporte para até 100 recipient. Especifique recipient adicionais com endereços de email separados por vírgulas (,).

Para desativar essa configuração, deixe a configuração em branco. Em alguns casos, você deseja acionar um processo e não desejar uma notificação por email do resultado.

**Recipient de trabalho com falha:** Um endereço de email para o qual são enviadas mensagens para indicar trabalhos com falha. Por padrão, uma mensagem de falha é sempre enviada ao remetente. Se você digitar remetente, os resultados do email serão enviados para o remetente. Há suporte para até 100 recipient. Especifique recipient adicionais com endereços de email separados por vírgulas (,).

Para desativar essa configuração, deixe a configuração em branco. Em alguns casos, você deseja acionar um processo e não desejar uma notificação por email do resultado.

**Host da Caixa de Entrada:** O nome do host da caixa de entrada ou o endereço IP do provedor de email a ser verificado.

**Porta da caixa de entrada:** A porta que o servidor de email usa. O valor padrão para POP3 é 110 e o valor padrão para IMAP é 143. Se SSL estiver ativado, o valor padrão para POP3 é 995 e o valor padrão para IMAP é 993.

**Protocolo da caixa de entrada:** O protocolo de email do terminal de email a ser usado para digitalizar a caixa de entrada. Os valores são IMAP ou POP3. O servidor de correio do host da caixa de entrada deve suportar esses protocolos.

**Tempo limite da caixa de entrada:** O tempo limite, em segundos, para que o provedor de email aguarde as respostas da caixa de entrada.

**Usuário da Caixa de Entrada:** O nome de usuário necessário para fazer logon na conta de email. Dependendo do servidor de e-mail e da configuração, esse valor pode ser apenas a parte do nome do usuário do e-mail ou pode ser o endereço de e-mail completo.

**Senha da caixa de entrada:** A senha do usuário da caixa de entrada.

**SSL POP3/IMAP ativado:** Selecione esta configuração para forçar o provedor de email a usar SSL para digitalizar a caixa de entrada. Certifique-se de que o servidor de correio suporta SSL.

**Host SMTP:** O nome de host do servidor de email que o provedor usa para enviar resultados e mensagens de erro.

**Porta SMTP:** O valor padrão para a porta SMTP é 25.

**Usuário SMTP:** A conta de usuário que o provedor de email deve usar ao enviar notificações por email de resultados e erros.

**Senha SMTP:** A senha da conta SMTP. Alguns servidores de email não exigem uma senha SMTP.

**Enviar de:** O endereço de email (por exemplo, user@company.com) usado para enviar notificações por email de resultados e erros. Se você não especificar um valor Enviar de, o servidor de email tentará determinar o endereço de email combinando o valor especificado na configuração Usuário SMTP com um domínio padrão configurado no servidor de email. Se o servidor de e-mail não tiver um domínio padrão e você não especificar um valor para Enviar de, podem ocorrer erros. Para garantir que as mensagens de e-mail tenham o endereço de origem correto, especifique um valor para a configuração Enviar de.

**SSL SMTP Habilitado:** Selecione esta configuração para forçar o provedor de email a usar SSL para digitalizar a caixa de entrada. Certifique-se de que o servidor de correio suporta SSL.

**Pasta Enviada por Email com Falha:** Especifica um diretório no qual armazenar resultados se o servidor de correio SMTP não estiver operacional.

**assíncrono:** Quando definido como síncrono, todos os documentos de entrada são processados e uma única resposta é retornada. Quando definido como assíncrono, uma resposta é enviada para cada documento processado.

Por exemplo, um terminal de email é criado para um serviço que utiliza um único documento do Word e retorna esse documento como um arquivo PDF. Um email pode ser enviado para a caixa de entrada do ponto final que contém vários (3) documentos do Word. Quando todos os três documentos são processados, se o terminal estiver configurado como síncrono, um único email de resposta será enviado com os três documentos anexados. Se o ponto de extremidade for assíncrono, um email de resposta será enviado depois que cada documento do Word for convertido em PDF. O resultado são três emails, cada um com um único anexo PDF.

O valor padrão é assíncrono.

**Inclua o corpo original do email como um anexo:** Por padrão, quando você envia um email para o servidor de formulários, o texto original da mensagem é incluído no corpo da mensagem. Para incluir o texto como anexo, selecione essa opção.

**Use a linha de assunto original para emails de resultado:** Por padrão, o servidor do Forms usa os valores especificados nas configurações Assunto do email de sucesso e Assunto do email de erro como a linha de assunto ao enviar mensagens de email de resultado. Para, em vez disso, usar a mesma linha de assunto que o email original enviado para o servidor, selecione essa opção.

**Assunto do email de sucesso:** Depois de enviar um email para um terminal de email para o start ou continuar um processo, você receberá uma mensagem de email de retorno do servidor de formulários do AEM. Se seu email for bem-sucedido, você receberá um email de sucesso. Se seu email falhar, você receberá um email com falha informando por que ele falhou. Essa configuração permite especificar a linha de assunto das mensagens de email de sucesso enviadas para esse terminal.

**Corpo de email de sucesso:** Permite que você especifique o texto do corpo das mensagens de email de sucesso enviadas para este terminal.

**Prefixo de assunto do email de erro:** Permite que você especifique o texto usado no início da linha de assunto das mensagens de e-mail de falha enviadas para este terminal.

**Assunto do email de erro:** Permite que você especifique a linha de assunto das mensagens de e-mail de falha enviadas para este terminal. Esse texto é exibido após o Prefixo de assunto do email de erro.

**Corpo do email de erro:** Permite que você especifique a primeira linha no texto do corpo das mensagens de e-mail de falha enviadas para esse terminal.

**Informações de resumo do email:** Cada mensagem de sucesso ou falha inclui uma seção que contém o texto original do email enviado para o servidor de formulários. Essa configuração especifica o texto que aparece acima dessa seção.

**Valide a Caixa de entrada antes de criar/atualizar este ponto de extremidade:** Quando essa opção é selecionada, o servidor de formulários verifica se as configurações de SMTP/POP3 estão corretas antes da criação do terminal. Quando você clica em Adicionar, uma mensagem é exibida informando se a conta da caixa de entrada é válida. Se essa opção não estiver selecionada, o servidor de formulários AEM criará o terminal sem validar a caixa de entrada.

**Nome da Operação:** Esta configuração é obrigatória. Uma lista de operações que podem ser atribuídas ao ponto de extremidade de email. A operação selecionada aqui determina quais campos são exibidos nas seções Mapeamentos de parâmetro de entrada e Mapeamentos de parâmetro de saída.

**Mapeamentos de parâmetros de entrada:** Usado para configurar a entrada necessária para processar o serviço e a operação. Os dois tipos de entrada são literal e variável:

**Literal:** O email usa o valor inserido no campo conforme é exibido.

**Variável:** Você pode mapear uma string do assunto do email, corpo, cabeçalho ou endereço de email do remetente. Para fazer isso, use uma das seguintes palavras-chave: %SUBJECT%, %BODY%, %HEADER% ou %SENDER%. Por exemplo, se você usar %SUBJECT%, o conteúdo do assunto do email será usado como parâmetro de entrada. Para coletar anexos, insira um padrão de arquivo que o ponto de extremidade de email pode usar para selecionar os documentos anexados. Por exemplo, inserir &amp;ast;.pdf seleciona qualquer documento anexado que tenha uma extensão de nome de arquivo .pdf. Inserir &amp;ast; seleciona qualquer documento anexado. Digitar example.pdf seleciona qualquer documento anexado chamado example.pdf.

**Mapeamentos de parâmetros de saída:** Usado para configurar a saída do serviço e da operação. Os seguintes caracteres nos valores de mapeamento do parâmetro de saída são expandidos no nome do arquivo anexo:

**%F** Representa o nome de arquivo do arquivo de origem (não inclui uma extensão).

**%E** Representa a extensão do arquivo de origem.

Qualquer ocorrência da barra invertida (\) é substituída por %%.

***observação **: Se a mensagem de solicitação de serviço incluir vários anexos de arquivo, você não poderá usar os parâmetros %F e %E para a propriedade Mapeamentos de Parâmetro de Saída do ponto final. Se a resposta dos serviços retornar vários anexos de arquivo, não será possível especificar o mesmo nome para mais de um anexo. Se você não seguir essas recomendações, o serviço chamado criará os nomes dos arquivos retornados e os nomes não serão previsíveis.*

Os seguintes valores estão disponíveis:

**Objeto único:** O provedor de e-mail não tem o destino da pasta de origem; os resultados são retornados como anexos. O padrão é Result/%F.ps e retorna Result%%sourcefilename.ps como o anexo de nome de arquivo.

**Lista:** O padrão é Result/%F/ e retorna Result%%sourcefilename%%file1 como o anexo de nome de arquivo.

**Mapa:** O padrão é Result/%F/ e o destino de origem é Result%%sourcefilename%%file1 e Result%%sourcefilename%%file2. Se o mapa contiver mais de um objeto e o padrão for Result/%F.ps, os anexos do arquivo de resposta serão Result%%sourcefilename1.ps (saída 1) e Result%%sourcefilename2.ps (saída 2).

## Criar um ponto de extremidade de email para o serviço de Tarefa completa {#create-an-email-endpoint-for-the-complete-task-service}

Para que o fluxo de trabalho de formulários receba e manipule mensagens de email recebidas de usuários, é necessário criar um terminal de email para o serviço de Tarefa completa.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de serviços, clique no serviço Tarefa completa.
1. Na guia Pontos de extremidade, selecione Email na lista suspensa e clique em Adicionar.
1. Na caixa Host da caixa de entrada, digite o nome do host ou o endereço IP do servidor de email.
1. Na caixa Usuário da caixa de entrada, digite o nome de usuário necessário para fazer logon na conta de email que você criou para lidar com os envios de formulário. Dependendo do servidor de e-mail e da configuração, esse nome pode ser apenas a parte do nome do usuário do e-mail ou pode ser o endereço de e-mail completo.
1. Na caixa Senha da caixa de entrada, digite a senha para o Usuário da caixa de entrada.
1. Na caixa Host SMTP, digite o nome do host ou endereço IP do servidor de email do qual o provedor de email envia resultados e mensagens de erro.
1. Na caixa Usuário SMTP, digite a conta de usuário que o provedor de email deve usar ao enviar emails para obter resultados e erros. Essa conta de usuário pode ser o mesmo valor que você usou para o Usuário da Caixa de entrada.
1. Na caixa Senha SMTP, digite a senha para a conta SMTP.
1. Na lista Nome da Operação, selecione invocar.
1. Na lista attachmentMap, selecione Variável e digite `*.*` na caixa adjacente. Isso envia todos os anexos das mensagens de entrada para uma variável de mapa para o processo de Tarefa Concluída.
1. Na lista mailBody, selecione a variável e digite `%BODY%` na caixa adjacente.
1. Na lista mailFrom, selecione Variable e digite `%SENDER%` na caixa adjacente. Isso mapeia o endereço do remetente para os dados do processo de Tarefa completa.
1. Na caixa de resultados, digite `results`. Isso faz com que o processo Concluir Tarefa ou Start retorne uma string de resultado.
1. Clique em Adicionar.

