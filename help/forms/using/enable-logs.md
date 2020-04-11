---
title: Ativar o registro em log para formulários HTML5
seo-title: Ativar o registro em log para formulários HTML5
description: O utilitário logger ativa o registro em log de um formulário e ajuda a depurar problemas relacionados ao formulário.
seo-description: O utilitário logger ativa o registro em log de um formulário e ajuda a depurar problemas relacionados ao formulário.
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Ativar o registro em log para formulários HTML5{#enable-logging-for-html-forms}

Você pode configurar o utilitário logger para start criando registros para formulários HTML5. O utilitário logger tem vários níveis, você pode definir um nível conforme suas necessidades. Os formulários HTML5 têm componentes de servidor e cliente. Você pode configurar registros para ambos os componentes.

## Configuração do registro no servidor {#configuring-server-side-logging}

Execute as seguintes etapas para configurar os registros do servidor:

1. Ir para `https://'[server]:[port]'/system/console/configMgr`. Localize e abra a opção de configuração *do agente de log do* Apace Sling. Uma caixa de diálogo é exibida:

   ![ Caixa de diálogo da opção de configuração do registrador de Sling Apace](assets/logconfig.png)

   Opção de configuração do agente de log do Apace Sling

1. Altere o Nível **do** log para **Depuração**.

1. Especifique o nome e o caminho do Arquivo **de** Log.

   >[!NOTE]
   >
   >Para gerar logs no diretório de log de formulários HTML5, adicione ../logs/ antes do nome do arquivo.

1. Altere o **Logger** para **HTMLFormsPerfLogger**. Clique em **Salvar**.

## Configurando o registro de cliente {#configuring-client-logging}

Você pode usar os seguintes métodos para habilitar o logon do lado do cliente em formulários HTML5:

* Uso do parâmetro request nomeado `log`
* Uso do CQ Configuration Manager

### Habilitar o registro usando o parâmetro de solicitação {#enabling-logging-using-request-parameter}

Usando esse método, você pode gerar logs para uma solicitação específica. O nome do parâmetro request é `log. O URL do log é o seguinte:

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

A configuração do log é composta pelo nível do log e pela categoria do logger.

#### Destino do registro {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>Destino do registro</strong></th>
   <th><strong>Descrição</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>Os registros são direcionados para o <strong>console do navegador</strong></td>
  </tr>
  <tr>
   <td>2</td>
   <td>Os logs são coletados em um objeto JavaScript no lado do cliente e podem ser publicados no <strong>Servidor</strong> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>Ambas as opções acima<br /> </td>
  </tr>
 </tbody>
</table>

#### Níveis de registro {#log-levels}

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
   <td>TRAÇO<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>7</td>
   <td>TODAS<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Categorias do registrador {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>Categoria de registro</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>uma sessão gerenciada no quadro branco</td>
   <td>xfa (logs relacionados ao mecanismo de script)</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView (logs relacionados ao mecanismo de layout)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf (registros relacionados ao desempenho)<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Configuração do registro {#log-configuration}

No URL do log, o parâmetro da string de configuração do query é definido da seguinte forma:

`{destination}-{a level}-{b level}-{c level}`

Por exemplo:

<table>
 <tbody>
  <tr>
   <th>Configuração do registro</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>Destino: Nível xfa do servidor<br /> : Nível de INFO<br /> xfaView: Nível DEBUG<br /> xfaPerf: TRAÇO</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O nível de log padrão para cada categoria de log a (xfa), b (xfaView) e c (xfaPerf) é 2 (ERRO). Assim, para configuração de log: 2-b6, os níveis de log para categorias diferentes são:
>a xfa: 2 (ERRO de nível padrão)
>b (xfaView): 6 (TRACE especificado pelo usuário)
>a (xfaPerf): 2 (ERRO de nível padrão)

### Habilitar o registro usando o Configuration Manager {#enabling-logging-using-configuration-manager}

Se você usar o Configuration Manager para ativar o registro, os registros serão gerados para cada solicitação de renderização até que o registro seja desabilitado novamente.

1. Faça logon no CQ Configuration Manager em `https://'[server]:[port]'/system/console/configMgr` e faça logon com as credenciais de administrador.
1. Procure e clique em Configurações **de formulários** móveis.
1. Na caixa de texto Opções de depuração, digite as configurações de log conforme descrito na seção anterior, por exemplo, **2-a4-b5-c6**

   ![Configuração de formulários](assets/forms_configuration.png)

   Configuração de formulários

## Carregar logs {#uploading-logs}

Se o destino for definido como 1, todas as mensagens de log de script do cliente serão direcionadas para o console. Se um administrador exigir esses logs juntamente com os logs do servidor, defina o nível de destino como 2. Nesse nível, todos os registros são coletados em um objeto JS no lado do cliente e, se o formulário for renderizado com o Perfil padrão, um botão **Enviar registros** será exibido à esquerda do botão **Realçar campos** existentes na barra de ferramentas. Quando o usuário clica no link, todos os logs coletados são publicados no servidor e são registrados no arquivo de log de erros configurado no servidor.

Por padrão, todas as informações são adicionadas ao arquivo error.log no diretório /crx-repository/logs/.

Para alterar o local e o nome do arquivo de log:

1. Faça logon no Configuration Manager como administrador. O URL padrão do Configuration Manager é `https://'[server]:[port]'/system/console/configMgr`.
1. Clique em **Apache Sling Logging Logger Configuration (Configuração** do registrador Apache Sling). Uma caixa de diálogo é exibida.

   ![logconfig-1](assets/logconfig-1.png)

1. Altere o Nível **do** log para Depuração.

1. Especifique o caminho e o nome do Arquivo **de** Log.

   >[!NOTE]
   >
   >Para criar logs no mesmo diretório onde outros arquivos de log são mantidos, especifique ../logs/&lt;nome do arquivo> na propriedade Arquivos de Log.

1. Altere o **Logger** para **HTMLFormsPerfLogger** e clique em **Salvar**.
