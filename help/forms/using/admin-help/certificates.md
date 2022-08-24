---
title: Gerenciar certificados
seo-title: Managing certificates
description: Saiba como importar e exportar um certificado e editar suas configurações de confiança.
seo-description: Learn how to import and export a certificate and edit its trust settings.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Gerenciar certificados {#managing-certificates}

Usando o Gerenciamento de armazenamento de confiança, você pode importar, editar e excluir certificados confiáveis no servidor para a validação de assinaturas digitais e autenticação de certificado. É possível importar e exportar qualquer número de certificados. Depois que um certificado é importado, você pode editar as configurações de confiança e o tipo de armazenamento de confiança. Considere as seguintes opções ao combinar tipos de armazenamento de confiança:

* **Confiança para Autenticação de Certificado com CA:** Para validação de CRL, também selecione Confiança para identidade.
* **Confiança para Autenticação de Certificado com ICA:** Selecione Somente Confiança para Identidade. Uma ICA não deve ser confiável para a Autenticação de Certificado. Se você confiar no ICA para autenticação de certificado, o ICA se tornará um CA para construção de caminho. Se a ICA for confiável para Autenticação de Certificado e Identidade, o certificado do fornecedor da CA será ignorado porque a ICA se torna a CA.
* **Confiança no OCSP Server com HTTPs:** Se o servidor do entrevistado OSCP residir em um local HTTPs, você também deverá selecionar Confiança para conexões SSL. Se o entrevistado do OSCP exigir a validação da CRL, certifique-se também de selecionar Confiança para identidade.
* **Raiz Adobe:** Não selecione Conexões SSL ou Tipos de Armazenamento de Confiança do Servidor OCSP. A Raiz Adobe não é confiável para Conexões SSL e Servidor OCSP. O Adobe não emite certificados OCSP e SSL. A raiz Adobe é implicitamente confiável com um alias name=&quot;ADOBEROOT&quot;.

Somente certificados X509v3 são compatíveis. Esse tipo de certificado pode ser fornecido em um arquivo binário codificado por DER (arquivo .cer) ou em um arquivo de texto que contenha uma versão codificada em Base64 do mesmo certificado codificado por DER (incluindo certificados X509 no formato PEM (Privacy Enhanced Mail).

Os certificados necessários para concluir uma verificação de assinatura devem estar no mesmo armazenamento (HSM ou banco de dados).

Também é possível importar e excluir certificados usando a API do Gerenciador de Confiança. Para obter detalhes, consulte &quot;Importação de certificados usando a API do Gerenciador de Confiança&quot; e &quot;Exclusão de certificados usando a API do Gerenciador de Confiança&quot; em [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

## Importar um certificado {#import-a-certificate}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de armazenamento de confiança > Certificados]**.
1. Clique em Importar e, em Tipo de Armazenamento de Confiança, selecione uma destas opções:

   * **Confiança para conexões SSL:** Especifica que AEM formulários podem usar certificados para se conectar a sistemas externos por SSL.
   * **Confiança para assinatura de certificação:** Especifica que os certificados são confiáveis em operações de assinatura de documento para certificar assinaturas digitais do autor.
   * **Confiança para assinatura:** Especifica que os certificados são confiáveis em operações de assinatura de documento para assinaturas digitais de não autor.
   * **Confiança para Autenticação de Certificado:** Especifica AEM formulários usa certificados para autenticar usuários usando autenticação de certificado ou de cartão inteligente.
   * **Confiança para o servidor OCSP:** Especifica que AEM formulários podem usar certificados para se conectar a respondedores externos OCSP
   * **Confiança para identidade:** Especifica que os certificados podem ser usados para confiar em informações diferentes dos tipos especificados acima.

   >[!NOTE]
   >
   >O armazenamento de confiança confia implicitamente em um Certificado raiz Adobe para autenticação de certificado, assinatura, assinatura de certificação e identidade.

1. Na caixa Alias, digite o identificador do certificado.
1. Clique em **[!UICONTROL Procurar]** para localizar o certificado e clique em **[!UICONTROL OK]**.

## Exportar um certificado {#export-a-certificate}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de armazenamento de confiança > Certificados]**.
1. Clique no nome do alias do certificado a ser exportado. O **[!UICONTROL Detalhes do certificado]** será exibida.
1. Clique em **[!UICONTROL Exportar]**, siga as instruções para exportar o certificado e clique em **[!UICONTROL OK]**.

## Editar as configurações de confiança de um certificado e o tipo de armazenamento de confiança {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de armazenamento de confiança > Certificados]**.
1. Clique no nome do alias do certificado a ser editado.
1. Clique em **[!UICONTROL Atualizar Certificado]**.
1. Para alterar o nome Alias do certificado, digite um novo nome na caixa Alias .
1. Para atualizar o tipo de armazenamento de confiança para o certificado, selecione o tipo de armazenamento de confiança apropriado.
1. Para atualizar as restrições de política, na caixa Políticas do Certificado, digite as informações da política e clique em **[!UICONTROL OK]**.

## Excluir um certificado {#delete-a-certificate}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de armazenamento de confiança > Certificados]**.
1. Marque as caixas de seleção dos certificados a serem excluídos, clique em **[!UICONTROL Excluir]** e, em seguida, clique em **[!UICONTROL OK]**.
