---
title: Estratégias de backup para pastas monitoradas
seo-title: Backup strategies for watched folders
description: Este documento descreve como as pastas vigiadas são afetadas por diferentes cenários de backup e recuperação, as limitações e os resultados desses cenários e como minimizar a perda de dados.
seo-description: This document describes how watched folders are affected by different backup and recovery scenarios, the limitations and outcomes of these scenarios, and how to minimize data loss.
uuid: c61997b8-6c36-4bd9-90e5-411841a6c176
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f775933-e989-4456-ad01-9bdf5dee3dad
exl-id: 0d36160a-29fa-4cc4-a0ff-fc681d3e040e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 2%

---

# Estratégias de backup para pastas monitoradas {#backup-strategies-for-watched-folders}

Este conteúdo descreve como as pastas assistidas são afetadas por diferentes cenários de backup e recuperação, as limitações e os resultados desses cenários e como minimizar a perda de dados.

*Pasta assistida* é um aplicativo baseado em sistema de arquivos que chama operações de serviço configuradas que manipulam o arquivo em uma das seguintes pastas na hierarquia de pasta assistida:

* Entrada
* Estágio
* Saída
* Falha
* Preservar

Primeiro, um usuário ou aplicativo cliente solta o arquivo ou a pasta na pasta de entrada. A operação de serviço então move o arquivo para a pasta de estágio para processamento. Depois que o serviço executa a operação especificada, ele salva o arquivo modificado na pasta de saída. Os arquivos de origem processados com êxito são movidos para a pasta preserve e os arquivos de processamento com falha são movidos para a pasta de falha. Quando a variável `Preserve On Failure` estiver habilitado, os arquivos de origem processados com falha serão movidos para a pasta preserve. (Consulte [Configuração de endpoints de pasta observados](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).)

Você pode fazer backup das pastas controladas fazendo backup do sistema de arquivos.

>[!NOTE]
>
>Esse backup é independente do banco de dados ou do processo de backup e recuperação do armazenamento de documentos.

## Como as pastas vigiadas funcionam {#how-watched-folders-work}

Este conteúdo descreve o processo de manipulação de arquivos de pasta monitorada. É importante compreender este processo antes de desenvolver um plano de recuperação. Neste exemplo, a variável `Preserve On Failure` está habilitado para a pasta monitorada. Os arquivos são processados na ordem em que chegam.

A tabela a seguir descreve a manipulação de arquivo de cinco arquivos de amostra (arquivo1, arquivo2, arquivo3, arquivo4, arquivo5) durante todo o processo. Na tabela, o eixo x representa o tempo, como Tempo 1 ou T1, e o eixo y representa as pastas dentro da hierarquia de pastas assistida, como Entrada.

<table>
 <thead>
  <tr>
   <th><p>Pasta</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Entrada</p></td>
   <td><p>arquivo1, arquivo2, arquivo3, arquivo4</p></td>
   <td><p>arquivo2, arquivo3, arquivo4</p></td>
   <td><p>arquivo3, arquivo4</p></td>
   <td><p>arquivo4</p></td>
   <td><p>empty</p></td>
   <td><p>arquivo5</p></td>
   <td><p>empty</p></td>
  </tr>
  <tr>
   <td><p>Estágio</p></td>
   <td><p>empty</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>arquivo4</p></td>
   <td><p>empty</p></td>
   <td><p>arquivo5</p></td>
  </tr>
  <tr>
   <td><p>Saída</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
  </tr>
  <tr>
   <td><p>Falha</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file3_fail, arquivo3 </p></td>
   <td><p>file3_fail, arquivo3 </p></td>
   <td><p>file3_fail, arquivo3 </p></td>
  </tr>
  <tr>
   <td><p>Preservar</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file1 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>arquivo1, arquivo2, arquivo4 </p></td>
   <td><p>arquivo1, arquivo2, arquivo4 </p></td>
  </tr>
 </tbody>
</table>

O texto a seguir descreve a manipulação de arquivo para cada vez:

**T1:** Os quatro arquivos de amostra são colocados na pasta de entrada.

**T2:** A operação de serviço move o arquivo1 para a pasta de estágio para manipulação.

**T3:** A operação de serviço move o arquivo2 para a pasta de preparo para manipulação. Ele coloca os resultados do arquivo1 na pasta de saída e move o arquivo1 para a pasta preserve.

**T4:** A operação de serviço coloca o arquivo3 na pasta de preparo para manipulação. Ele coloca os resultados do arquivo2 na pasta de saída e coloca o arquivo2 na pasta preserve.

**T5:** A operação de serviço coloca o arquivo4 na pasta de preparo para manipulação. A manipulação do arquivo3 falha e a operação de serviço o coloca na pasta de falha.

**T6:** A operação de serviço coloca o arquivo5 na pasta de entrada. Ele coloca os resultados do arquivo4 na pasta de saída, coloca o arquivo4 na pasta preserve .

**T7:** A operação de serviço coloca o arquivo5 na pasta de preparo para manipulação.

## Backup de pastas vigiadas {#backing-up-watched-folders}

É recomendável fazer o backup de todo o sistema de arquivos de pastas monitoradas em outro sistema de arquivos.

## Restaurar pastas vigiadas {#restoring-watched-folders}

Esta seção descreve como restaurar pastas controladas. As pastas assistidas geralmente chamam processos de duração curta que são concluídos em um minuto. Nesses casos, restaurar a pasta assistida com um backup feito a cada hora não impedirá a perda de dados.

Por exemplo, se um backup for feito no momento T1 e o servidor falhar no T7, o arquivo1, o arquivo2, o arquivo3 e o arquivo4 já serão manipulados. A restauração da pasta monitorada com um backup feito em T1 não impede a perda de dados.

Se um backup mais recente foi feito, é possível restaurar os arquivos. Ao restaurar os arquivos, considere em qual pasta de hierarquia de pasta assistida o arquivo atual reside:

**Estágio:** Os arquivos nesta pasta são processados novamente depois que a pasta assistida é restaurada.

**Entrada:** Os arquivos nesta pasta são processados novamente depois que a pasta assistida é restaurada.

**Resultado:** Os arquivos desta pasta não são processados.

**Saída:** Os arquivos desta pasta não são processados.

**Preservar:** Os arquivos desta pasta não são processados.

## Estratégias para minimizar a perda de dados {#strategies-to-minimize-data-loss}

As estratégias a seguir podem minimizar a perda de dados da pasta de saída e entrada ao restaurar uma pasta monitorada:

* Faça backup das pastas de saída e falha frequentemente, por exemplo, a cada hora, para evitar a perda de arquivos de resultado e falha.
* Faça o backup dos arquivos de entrada em uma pasta diferente da que foi assistida. Isso garante a disponibilidade do arquivo após a recuperação caso não seja possível encontrar os arquivos na pasta de saída ou de falha. Certifique-se de que seu esquema de nomenclatura de arquivos seja consistente.

   Por exemplo, se você estiver salvando a saída com `%F.`*extensão*, o arquivo de saída terá o mesmo nome do arquivo de entrada. Isso ajuda a determinar quais arquivos de entrada são manipulados e quais devem ser reenviados. Se você vir somente o arquivo file1_out na pasta de resultados e não o arquivo2_out, o arquivo3_out e o arquivo4_out, é necessário reenviar o arquivo2, o arquivo3 e o arquivo4.

* Se o backup de pasta monitorada que está disponível for anterior ao tempo necessário para processar o trabalho, você deverá permitir que o sistema crie uma nova pasta monitorada e coloque automaticamente os arquivos na pasta de entrada.
* Se o backup disponível mais recente não for recente o suficiente, o tempo de backup será menor do que o tempo necessário para processar os arquivos e a pasta monitorada será restaurada, o arquivo será manipulado em um dos seguintes estágios diferentes:

   * **Fase 1:** Na pasta de entrada
   * **Fase 2:** Copiado para a pasta do estágio, mas o processo ainda não é chamado
   * **Fase 3:** Copiado para a pasta do estágio e o processo é chamado
   * **Fase 4:** Manipulação em progresso
   * **Fase 5:** Resultados retornados

   Se os arquivos estiverem no Estágio 1, eles serão manipulados. Se os arquivos estiverem no Estágio 2 ou 3, coloque-os na pasta de entrada para que a manipulação ocorra novamente.

   >[!NOTE]
   >
   >Se a manipulação de um arquivo ocorrer mais de uma vez, a perda de dados será evitada, mas os resultados poderão ser duplicados.

## Conclusão {#conclusion}

Devido à natureza dinâmica e em constante mudança de uma pasta assistida, a restauração das pastas monitoradas deve ser feita com arquivos com backup em um dia. Uma prática recomendada seria fazer o backup dos resultados, armazenar a pasta de entrada em um servidor e rastrear os arquivos de entrada para que você possa reenviar o trabalho em caso de falha.
