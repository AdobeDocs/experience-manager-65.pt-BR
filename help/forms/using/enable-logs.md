---
title: Habilitar registro para formulários HTML5
seo-title: Habilitar registro para formulários HTML5
description: O utilitário logger ativa o registro em log de um formulário e ajuda a depurar os problemas relacionados ao formulário.
seo-description: O utilitário logger ativa o registro em log de um formulário e ajuda a depurar os problemas relacionados ao formulário.
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 6%

---


# Habilitar registro para formulários HTML5{#enable-logging-for-html-forms}

Você pode configurar o utilitário logger para começar a criar logs para formulários HTML5. O utilitário logger tem vários níveis. Você pode definir um nível de acordo com seus requisitos. Os formulários HTML5 têm componentes de servidor e cliente. Você pode configurar logs para ambos os componentes.

## Configurando o registro do lado do servidor {#configuring-server-side-logging}

Execute as seguintes etapas para configurar os logs do lado do servidor:

1. Ir para `https://'[server]:[port]'/system/console/configMgr`. Localize e abra a opção *Apace Sling logging logger configuration* . Uma caixa de diálogo é exibida:

   ![ Caixa de diálogo da opção de configuração do logger de registro do Apache Sling](assets/logconfig.png)

   Opção de configuração do logger de registro do Apache Sling

1. Altere o **Nível de Log** para **Depuração**.

1. Especifique o nome e o caminho do **Arquivo de Log**.

   >[!NOTE]
   >
   >Para gerar logs no diretório de log de formulários HTML5, adicione ../logs/ antes do nome do arquivo.

1. Altere **Logger** para **HTMLFormsPerfLogger**. Clique em **Salvar**.

## Configurando o registro de cliente {#configuring-client-logging}

Você pode usar os seguintes métodos para ativar o logon no lado do cliente em formulários HTML5:

* Uso do parâmetro de solicitação chamado `log`
* Uso do Gerenciador de configuração do CQ

### Ativar o registro usando o parâmetro de solicitação {#enabling-logging-using-request-parameter}

Usando este método, você pode gerar logs para uma solicitação específica. O nome do parâmetro da solicitação é &quot;log&quot;. O URL de log é o seguinte:

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

A configuração do log é composta pelo nível do log e pela categoria do logger.

#### Destino do Log {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>Destino do log</strong></th>
   <th><strong>Descrição</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>Os registros são direcionados para o navegador <strong>Console</strong></td>
  </tr>
  <tr>
   <td>2</td>
   <td>Os logs são coletados em um objeto JavaScript no lado do cliente e podem ser publicados em <strong>Server</strong> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>Ambas as opções acima<br /> </td>
  </tr>
 </tbody>
</table>

#### Níveis de Log {#log-levels}

<table>
 <tbody>
  <tr>
   <th>Nível de registro</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>0</td>
   <td>DESLIGADO<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>1</td>
   <td>FATAL<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>2</td>
   <td>ERRO<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>AVISO<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>4</td>
   <td>INFO<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>5</td>
   <td>DEPURAR<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>6</td>
   <td>TRACE<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>7</td>
   <td>TODAS<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Categorias de logger {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>Categoria de Log</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>uma sessão gerenciada no quadro branco</td>
   <td>xfa (registros relacionados ao mecanismo de scripts)</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView (registros relacionados ao mecanismo de layout)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf (registros relacionados ao desempenho)<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Configuração de Log {#log-configuration}

No URL de log, o parâmetro da string de consulta de configuração de log é definido da seguinte maneira:

`{destination}-{a level}-{b level}-{c level}`

Por exemplo:

<table>
 <tbody>
  <tr>
   <th>Configuração de registro</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>Destino: Servidor<br /> nível xfa: INFO<br /> nível xfaView: Nível DEBUG<br /> xfaPerf: TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O nível de log padrão para cada categoria de log a (xfa), b (xfaView) e c (xfaPerf) é 2 (ERRO). Assim, para configuração de log: 2-b6, os níveis de log para categorias diferentes são:
>a xfa: 2 (ERRO de nível padrão)
>b (xfaView): 6 (TRACE especificado pelo usuário)
>a (xfaPerf): 2 (ERRO de nível padrão)

### Ativar o registro utilizando o Configuration Manager {#enabling-logging-using-configuration-manager}

Se você usar o Configuration Manager para ativar o registro, os registros serão gerados para cada solicitação de renderização até que o registro seja desativado novamente.

1. Faça logon no CQ Configuration Manager em `https://'[server]:[port]'/system/console/configMgr` e faça logon com credenciais de administrador.
1. Procure por e clique em **Configurações de Forms Móvel**.
1. Na caixa de texto Opções de depuração , digite as configurações de log conforme descrito na seção anterior, por exemplo, **2-a4-b5-c6**

   ![Configuração de formulários](assets/forms_configuration.png)

   Configuração de formulários

## Upload de logs {#uploading-logs}

Se o destino for definido como 1, todas as mensagens de log do script do cliente serão direcionadas para o console. Se um administrador exigir esses logs, juntamente com os logs do servidor, defina o nível de destino como 2. Nesse nível, todos os logs são coletados em um objeto JS no lado do cliente e, se o formulário for renderizado com o Perfil padrão, um botão **Enviar logs** será exibido à esquerda do botão **Realçar campos existentes** na barra de ferramentas. Quando o usuário clica no link, todos os logs coletados são publicados no servidor e são registrados no arquivo de log de erros configurado no servidor.

Por padrão, todas as informações são adicionadas ao arquivo error.log no diretório /crx-repository/logs/ .

Para alterar o local e o nome do arquivo de log:

1. Faça logon no Configuration Manager como administrador. O URL padrão do Configuration Manager é `https://'[server]:[port]'/system/console/configMgr`.
1. Clique em **Apache Sling Logging Logger Configuration**. Uma caixa de diálogo é exibida.

   ![logconfig-1](assets/logconfig-1.png)

1. Altere o **Nível de Log** para Depurar.

1. Especifique o caminho e o nome do **Arquivo de Log**.

   >[!NOTE]
   >
   >Para criar logs no mesmo diretório em que outros arquivos de log são mantidos, especifique ../logs/&lt;filename> na propriedade Arquivos de Log.

1. Altere o **Agente de log** para **HTMLFormsPerfLogger** e clique em **Salvar**.
