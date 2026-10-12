---
title: Refatoração de SocialUtils
description: O pacote com.adobe.cq.social.ugcbase.SocialUtils foi substituído no AEM 6.1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%
---
# Refatoração de SocialUtils {#socialutils-refactoring}

## Pacote SocialUtils obsoleto {#socialutils-package-deprecated}

O pacote `com.adobe.cq.social.ugcbase.SocialUtils` foi substituído no AEM 6.1.

As tabelas a seguir listam os métodos a serem usados no lugar dos métodos `SocialUtils`.

## Pacote SocialResourceUtilities  {#socialresourceutilities-package}

| Métodos em com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities | Notas |
|---|---|
| CheckPermission booleano (Resolvedor ResourceResolver, Caminho da string, Ação da string) |  |
| SocialResourceProvider getSocialResourceProvider (recurso do recurso) |  |
| SocialResourceConfiguration getStorageConfig(Recurso) |  |
| Recurso getUGCResource(Resource userResource) |  |
| Recurso getUGCResource(Resource userResource, ResourceResolverFactory rrf) | novo |
| Recurso getUGCResource(Resource userResource, ResourceResolverFactory rrf, Cadeia de caracteres resourceTypeHint) | novo |
| Recurso getUGCResource(Resource userResource, String resourceTypeHint) |  |
| booleano hasModeratePermissions(recurso) |  |
| String resourceToACLPath(Recurso) |  |
| String resourceToUGCStoragePath(recurso) | substitui String resourceToUGCPath(Resource resource) |
| Cadeia de caracteres UGCToResourcePath(Resource resource) |  |
| Cadeia de caracteres UGCToResourcePath(Cadeia de caracteres ugcPath) | assinatura de método alterada |
| Cadeia de caracteres UGCToResourcePath(Cadeia de caracteres ugcPath, resolvedor ResourceResolver) | novo |

| Métodos em `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities | Notas |
|---|---|
| SocialResourceProvider getSocialResourceProvider (recurso do recurso) | substitui SocialResourceProvider getConfiguredProvider(recurso do recurso) |

## Pacote SCFUtilities {#scfutilities-package}

| Métodos em `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| String getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, tamanho int) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE size) |
| Página getContainingPage(Recurso) |
| String getSocialProfileURL(Nome de usuário da cadeia de caracteres, resolvedor ResourceResolver, página da página) |
| UserProperties getUserProperties(Resolvedor ResourceResolver, ID de usuário da cadeia de caracteres) |

## Somente para uso interno {#for-internal-use-only}

| booleano canAddNode(Session session, Caminho da string) |
|---|
| String createUniqueNameHint(Mensagem da string) |
| String createUniqueNameHint(Mensagem de string, int numRandomChars) |
| String generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Página getPage(Caminho da string, resolvedor ResourceResolver) |
| String getPagePath(Recurso) |
| String getPagePath(Caminho da string) |
| String getResourceTypeForIncludedResource(Componente do recurso, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Resource resource, String styleProperty, String defaultValue) |
| booleano isResourceOwner(Resource resource) |
| String mapUGCPath(Recurso) |
| String mapUGCPath(String ugcPath, resolvedor ResourceResolver) |
| booliano mayPost(ResourceResolver resolver, Recurso de recurso) |
| String prepareUserGeneratedContent(Resolvedor ResourceResolver, Caminho da string) |

## Métodos não estão mais disponíveis {#methods-no-longer-available}

| Node createNode(ResourceResolver resolver, Caminho da string, nodeType da string) |
|---|
| Resource getResourceAtPath(Resolvedor ResourceResolver, Caminho da cadeia de caracteres) |
| Resource getResourceAtPath(Resolvedor ResourceResolver, Caminho da string, ResourceType da string) |
| Configuração getStorageCloudServiceConfig(Recurso) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| resolver mayAccessUGC(ResourceResolver) booleano |
