---
title: Propriedades de configuração do gerenciamento de correspondência
seo-title: Correspondence Management Configuration Properties
description: Este tópico explica como você pode modificar o Asset Composer com configurações específicas da solução. Este tópico detalha as propriedades que podem ser editadas, com sua descrição, valores padrão e valores aceitáveis.
seo-description: This topic explains how you can modify Asset Composer with solution-specific configurations. This topic details the properties you can edit, with their description, default values, and acceptable values.
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 4%

---

# Propriedades de configuração do gerenciamento de correspondência {#correspondence-management-configuration-properties}

Para configurar essas propriedades, abra o seguinte URL em um navegador: `https://<server>:<port>/<contextPath>/system/console/configMgr` e selecione **Configurações de gerenciamento de correspondência**.

O Gerenciamento de correspondência tem as seguintes propriedades de configuração:

<table>
 <tbody>
  <tr>
   <th><p><strong>Propriedade</strong></p> </th>
   <th><p><strong>Descrição</strong></p> </th>
   <th><p><strong>Padrão</strong></p> </th>
   <th><p><strong>Valores aceitáveis</strong></p> </th>
  </tr>
  <tr>
   <td><p>Recuo</p> </td>
   <td>Recuo em módulos<p> </p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Qualquer número</p> </td>
  </tr>
  <tr>
   <td>Largura mínima do número</td>
   <td>Largura mínima a ser aplicada no campo marcador/número, ao usar Listas numeradas além de números romanos</td>
   <td>8,0 mm</td>
   <td>Qualquer número</td>
  </tr>
  <tr>
   <td><p>Largura mínima dos números romanos</p> </td>
   <td><p>Largura mínima a ser aplicada no campo marcador/número, ao usar números romanos</p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Qualquer número</p> </td>
  </tr>
  <tr>
   <td>Tipo de representação</td>
   <td>O tipo de representação que o aplicativo Criar correspondência usa para renderizar a visualização da carta. </td>
   <td>HTML Rendition</td>
   <td>Representação de HTML / Representação de PDF</td>
  </tr>
  <tr>
   <td><p>Ativar o realce PDF CCR</p> </td>
   <td><p>Habilita o destaque no PDF no aplicativo Criar correspondência</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de realce do Target</p> </td>
   <td><p>Tipo de realce do Target no aplicativo Criar correspondência</p> </td>
   <td><p>border</p> </td>
   <td><p>borda / preenchimento / nenhum</p> </td>
  </tr>
  <tr>
   <td><p>Cor de realce do Target</p> </td>
   <td><p>Cor de realce do Target no aplicativo Criar correspondência</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>Qualquer cor RGB no formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de realce do conteúdo</p> </td>
   <td><p>Tipo de realce de conteúdo no aplicativo Criar correspondência</p> </td>
   <td><p>Preenchimento</p> </td>
   <td><p>borda / preenchimento / nenhum</p> </td>
  </tr>
  <tr>
   <td><p>Cor de realce do conteúdo</p> </td>
   <td><p>Cor de realce do conteúdo no aplicativo Criar correspondência</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Qualquer cor RGB no formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de realce do campo</p> </td>
   <td><p>Tipo de realce de campo no aplicativo Criar correspondência</p> </td>
   <td><p>fill</p> </td>
   <td><p>borda / preenchimento / nenhum</p> </td>
  </tr>
  <tr>
   <td><p>Cor de realce do campo</p> </td>
   <td><p>Cor de realce do campo no aplicativo Criar correspondência</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Qualquer cor RGB no formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tempo limite do aplicativo</p> </td>
   <td><p>Tempo limite do aplicativo em segundos</p> </td>
   <td><p>1200</p> </td>
   <td><p>Qualquer número</p> </td>
  </tr>
  <tr>
   <td><p>Nome do parâmetro do documento PDF</p> </td>
   <td><p>Nome do parâmetro para documento PDF no pós-processo</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>Qualquer nome da variável de string</p> </td>
  </tr>
  <tr>
   <td><p>Nome do parâmetro de dados XML</p> </td>
   <td><p>Nome do parâmetro para documento XML (dados) em pós-processo</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>Qualquer nome da variável de string</p> </td>
  </tr>
  <tr>
   <td><p>Nome do parâmetro do documento XDP</p> </td>
   <td><p>Nome do parâmetro para documento XDP enviado ao processo de publicação</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>Qualquer nome da variável de string</p> </td>
  </tr>
  <tr>
   <td><p>Nome do parâmetro de URL de redirecionamento</p> </td>
   <td><p>Nome do parâmetro para o URL de redirecionamento enviado do processo de postagem Esse valor pode ser qualquer nome de variável da string</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>Qualquer nome da variável de string</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de envio de PDF</p> </td>
   <td><p>Tipo de envio de PDF (tipo de PDF gerado ao enviar a partir do aplicativo Criar correspondência)</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>interativo/não interativo</p> </td>
  </tr>
  <tr>
   <td><p>Otimizar a instância do dicionário de dados</p> </td>
   <td><p>Permite a transferência otimizada da Instância do Dicionário de Dados por servidor e cliente</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Correção automática de inconsistências </p> </td>
   <td><p>Quando ativado, ele trata automaticamente as possíveis inconsistências em Atribuições de Carta</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Usar Formatos de Dados Configurados</p> </td>
   <td><p>Controla o uso de formatos de edição de dados configurados e do formato de exibição de dados</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Formatos de exibição de dados</p> </td>
   <td><p>Especifica o formato de exibição específico da localidade para dados</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-aaaa; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-aaaa; numberDecimalSeparator=,; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-aaaa; numberDecimalSeparator=,; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-aaaa; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>Formato de edição de dados</p> </td>
   <td><p>Editar formato para dados. Isso é usado ao gravar dados como String ou analisar dados de String</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-aaaa; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>—<p> </p> </td>
  </tr>
  <tr>
   <td><p>Gerenciar instâncias de carta na publicação</p> </td>
   <td><p>Ativar/desativar a funcionalidade Gerenciar carta (aplicável somente para o servidor de publicação)</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoria</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria. Quando falso, os logs de auditoria de todas as ações serão desativados</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar Auditoria de Leitura</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para leituras de ativos</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Ativar Criar Auditoria</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para criação de ativos</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoria de atualização</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para atualização de ativos</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar Auditoria de Reverter</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para a reversão de ativos</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoria de publicação</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para publicação de ativos</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Ativar auditoria SaveAsDraft</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para salvar rascunhos de cartas</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoria de envio</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para envio de carta</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoria de email</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para cartas de correio eletrônico</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoria de impressão</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para impressão de cartas</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Ativar Auditoria de Entrega Personalizada</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para entrega personalizada de cartas</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Nome do parâmetro dos documentos anexos</p> </td>
   <td><p>Nome do parâmetro para documentos do anexo enviados ao processo de publicação</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>Qualquer nome da variável de string</p> </td>
  </tr>
  <tr>
   <td><p>Raiz do usuário do CM</p> </td>
   <td><p>URL da pasta que contém todos os ativos de usuário do Gerenciamento de correspondência</p> </td>
   <td><p>—</p> </td>
   <td><p>Local de pasta válido</p> </td>
  </tr>
  <tr>
   <td><p>Tamanho do Cache de Carta</p> </td>
   <td><p>Especifique o Número máximo de letras a serem mantidas em cache.</p> <p>Alterar esse valor resultará na limpeza de <code>in-memory</code> cache.</p> </td>
   <td><p>100</p> </td>
   <td><p>Qualquer valor numérico</p> </td>
  </tr>
  <tr>
   <td><p>Ativar Cache de Carta</p> </td>
   <td><p>Ative/desative o cache de letras.</p> <p>Alterar esse valor resultará na limpeza de <code>in-memory </code> cache.</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Solicitação de elementos de dados</p> </td>
   <td><p>Mantém os elementos de dados ordenados na interface de criação de correspondência de acordo com sua sequência em Carta</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Recarregamento de suporte</p> </td>
   <td><p>Ative/desative o suporte de recarregamento em letras renderizadas no lado do servidor.</p> <p>Desabilitar isso melhorará o desempenho da renderização de letras.</p> </td>
   <td><p>falso</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Pasta Temp</td>
   <td>Localização da pasta temporária.</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>Salvar Remoto</td>
   <td>Salva as Instâncias da Carta no autor de processamento especificado.</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Opções de compatibilidade</td>
   <td>Opções de compatibilidade do formato configname:configvalue separadas por vírgula.</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>Diretório de depuração </p> <p> </p> </td>
   <td>Local da pasta do sistema de arquivos para depuração. Se o diretório não <code>exists</code>, nenhum dumps de depuração será gerado.</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
