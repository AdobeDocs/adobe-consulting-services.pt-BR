---
title: Avisos de integração do Veeva Vault
description: Avisos de integração do Veeva Vault
exl-id: 1a188671-d123-4475-a607-65743ba0dadd
source-git-commit: 07eab1e439626bd3bb3416c9e7d0c1666927a7aa
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# Práticas recomendadas, Medidas de proteção e Avisos

## Versões

Essa integração exige as seguintes versões mínimas de software:

* Adobe Experience Manager, 6.5.5+
* Veeva Vault PromoMats, 20R3.2+

## Privacidade de dados

Essa integração foi projetada para transferir conteúdo entre o Adobe Experience Manager e o Veeva Vault PromoMats. Como controlador de dados, sua empresa é responsável por cumprir todas as leis e regulamentos de privacidade aplicáveis à coleta e ao uso de dados.

## Frequência de sincronização do conteúdo

O conteúdo e os metadados do AEM são sincronizados do AEM para o VVPN quando o fluxo de trabalho de integração é acionado. Isso pode ser feito automática ou manualmente. Os metadados de VPM são sincronizados de VPM para AEM. Isso pode ser feito automaticamente por meio de um scheduler ou manualmente por meio de um clique de botão.

## Limitações da integração e práticas recomendadas e medidas de proteção

Considere as seguintes limitações ao usar essa integração:

* Somente os seguintes tipos de dados são suportados ao sincronizar metadados: &quot;Text&quot; e &quot;Multiline Text&quot;.
* Embora a integração seja compatível com conteúdo modular AEM (fragmentos de conteúdo e fragmentos de experiência), ela não é compatível com conteúdo modular VPM.
* Não há suporte para documentos vinculados ao VPM.
* Não há suporte para a sincronização de anotações visuais de VPM com AEM.
* A integração não importa conteúdo do VPM para o AEM.
* Não há suporte para validação de metadados.
* O número de documentos é limitado com base na licença Veeva. Consulte [Limitações de Licença](#veeva-license-limitations).
* O número de chamadas de API é limitado com base na licença Veeva. Para obter mais informações, consulte [Limitações de API](https://developer.veevavault.com/docs/#what-are-rate-limits). Consulte [Limitações de Licença](#veeva-license-limitations).

## Limitações da licença Veeva

É possível monitorar os limites da instância navegando até as configurações gerais do VPM.

![Limites Veeva](assets/veeva-limits.png)
