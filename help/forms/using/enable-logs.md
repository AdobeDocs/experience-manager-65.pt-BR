---
title: Habilitar registro para formulários HTML5
description: O utilitário logger habilita o registro em log de um formulário e ajuda a depurar problemas relacionados ao formulário.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 2f574c98-550c-4b84-be1e-46a2700e7277
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 4%

---

# Habilitar registro para formulários HTML5{#enable-logging-for-html-forms}

Você pode configurar o utilitário logger para começar a criar registros para formulários HTML5. O utilitário logger tem vários níveis, você pode definir um nível de acordo com seus requisitos. os formulários HTML5 têm componentes de servidor e cliente. Você pode configurar logs para ambos os componentes.

## Configurar o registro do lado do servidor {#configuring-server-side-logging}

Execute as seguintes etapas para configurar registros do lado do servidor:

1. Ir para `https://'[server]:[port]'/system/console/configMgr`. Localize e abra a opção *Configuração do log do Apace Sling*. Uma caixa de diálogo é exibida:

   ![&#x200B; Caixa de diálogo de opção de configuração do agente de log do Apace Sling &#x200B;](assets/logconfig.png)

   Opção de configuração do logger de log do Apace Sling

1. Altere o **Nível de Log** para **Depuração**.

1. Especifique o nome e o caminho do **Arquivo de Log**.

   >[!NOTE]
   >
   >Para gerar logs no diretório de log dos formulários HTML5, adicione ../logs/ antes do nome do arquivo.

1. Altere **Logger** para **HTMLFormsPerfLogger**. Clique em **Salvar**.

## Configurando o registro do cliente {#configuring-client-logging}

Você pode usar os seguintes métodos para ativar o registro do lado do cliente em formulários HTML5:

* Usando o parâmetro de solicitação chamado `log`
* Utilização do CQ Configuration Manager

### Ativando o registro usando o parâmetro de solicitação {#enabling-logging-using-request-parameter}

Usando esse método, você pode gerar logs para uma solicitação específica. O nome do parâmetro de solicitação é `log`. O URL de log é o seguinte:

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

A configuração de log é composta do nível de log e da categoria do log.

#### Destino do log {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>Destino do log</strong></th>
   <th><strong>Descrição</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>Os logs são direcionados ao <strong>Console</strong> do navegador</td>
  </tr>
  <tr>
   <td>2</td>
   <td>Os logs são coletados em um objeto JavaScript no lado do cliente e podem ser postados no <strong>Servidor</strong> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>Ambas as opções acima<br /> </td>
  </tr>
 </tbody>
</table>

#### Níveis de log {#log-levels}

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
   <td>INFORMAÇÕES<br type="_moz" /> </td>
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
   <td>TUDO<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Categorias de logger {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>Categoria de log</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>a</td>
   <td>xfa (registros relacionados ao mecanismo de script)</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView (Logs relacionados ao mecanismo de layout)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf (logs relacionados ao desempenho)<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Configuração de log {#log-configuration}

No URL de log, o parâmetro da string de consulta de configuração do log é definido da seguinte maneira:

`{destination}-{a level}-{b level}-{c level}`

Por exemplo:

<table>
 <tbody>
  <tr>
   <th>Configuração de log</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>Destino: Servidor<br /> nível xfa: INFO<br /> nível xfaView: DEBUG<br /> nível xfaPerf: TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O nível de log padrão para cada categoria de log a (xfa), b (xfaView) e c (xfaPerf) é 2 (ERROR). Da mesma forma, para a configuração de log: 2-b6, os níveis de log para categorias diferentes são:
>a (xfa): 2 (erro de nível padrão)
>b (xfaView): 6 (TRACE especificado pelo usuário)
>a (xfaPerf): 2 (ERRO de nível padrão)

### Habilitando o registro usando o Configuration Manager {#enabling-logging-using-configuration-manager}

Se você usar o Configuration Manager para ativar o registro em log, serão gerados logs para cada solicitação de renderização até que o registro em log seja desativado novamente.

1. Faça logon no Gerenciador de configurações do CQ em `https://'[server]:[port]'/system/console/configMgr` e faça logon com credenciais de administrador.
1. Procure por e clique em **Configurações de Forms Móvel**.
1. Na caixa de texto Opções de Depuração, insira as configurações de log conforme descrito na seção anterior, por exemplo, **2-a4-b5-c6**

   ![Configuração do Forms](assets/forms_configuration.png)

   Configuração de formulários

## Upload de logs {#uploading-logs}

Se o destino for definido como 1, todas as mensagens de log do script do cliente serão direcionadas ao console. Se um administrador exigir esses registros junto com os registros do servidor, defina o nível de destino como 2. Neste nível, todos os logs são coletados em um objeto JS no lado do cliente e, se o formulário for renderizado com o Perfil padrão, o botão **Enviar logs** será exibido à esquerda do botão **Realçar campos existentes** na barra de ferramentas. Quando o usuário clica no link, todos os logs coletados são publicados no servidor e são registrados no arquivo de log de erros configurado no servidor.

Por padrão, todas as informações são adicionadas ao arquivo error.log no diretório /crx-repository/logs/.

Para alterar o local e o nome do arquivo de log:

1. Faça logon no Configuration Manager como administrador. A URL padrão do Configuration Manager é `https://'[server]:[port]'/system/console/configMgr`.
1. Clique em **Configuração do logger do Apache Sling**. Uma caixa de diálogo é exibida.

   ![logconfig-1](assets/logconfig-1.png)

1. Altere o **Nível de Log** para Depurar.

1. Especifique o caminho e o nome do **Arquivo de Log**.

   >[!NOTE]
   >
   >Para criar logs no mesmo diretório em que outros arquivos de log são mantidos, especifique ../logs/&lt;filename> na propriedade Arquivos de Log.

1. Altere o **Logger** para **HTMLFormsPerfLogger** e clique em **Salvar**.
