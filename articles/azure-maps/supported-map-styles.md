---
title: Azure Maps 中支持的地图样式 | Microsoft Docs
description: Azure Maps 支持的地图样式
author: walsehgal
ms.author: v-musehg
ms.date: 08/28/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: 8f0910e9040c962bae30a33b91a93e71e692dfdb
ms.sourcegitcommit: c29d7ef9065f960c3079660b139dd6a8348576ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "44713436"
---
# <a name="azure-maps-supported-map-styles"></a>Azure Maps 支持的地图样式
Azure Maps 支持四种不同的内置地图样式。 下面列出了样式及其说明。

## <a name="road"></a>道路
**道路**地图是一个标准地图，可显示道路、自然特征和人为特征以及这些特征的标签。

![道路](./media/supported-map-styles/road.png)

**适用 API：**
* [地图图像](https://docs.microsoft.com/rest/api/maps/render/getmapimage)
* [地图图块](https://docs.microsoft.com/rest/api/maps/render/getmaptile)
* JS 地图控件

## <a name="satellite"></a>卫星 
**卫星**样式是卫星和航拍图像的组合。

![卫星](./media/supported-map-styles/satellite.png)

**适用 API：**
* [卫星图块](https://docs.microsoft.com/rest/api/maps/render/getmapimagerytilepreview)
* JS 地图控件

## <a name="satelliteroadlabels"></a>Satellite_Road_Labels
此地图样式是道路和标签叠加在卫星和航拍图像上的混合体。

![satellite_road_labels](./media/supported-map-styles/satellite_road_labels.png)

**适用 API：**
* JS 地图控件

## <a name="grayscaledark"></a>Grayscale_Dark
**灰度深色**是道路地图样式的深色版本。

![gray_scale](./media/supported-map-styles/grayscale_dark.png)

**适用 API：**
* JS 地图控件 