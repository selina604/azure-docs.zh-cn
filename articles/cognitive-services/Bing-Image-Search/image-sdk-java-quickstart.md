---
title: 快速入门：在 Java 中使用 SDK 请求和筛选图像
description: 本快速入门将使用 Java 请求和筛选必应图像搜索返回的图像。
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 02/16/2018
ms.author: v-gedod
ms.openlocfilehash: 280a4b67d81b0734ea983c1d7fe1389e59651ccd
ms.sourcegitcommit: a2ae233e20e670e2f9e6b75e83253bd301f5067c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2018
ms.locfileid: "41929832"
---
# <a name="quickstart-request-and-filter-images-using-the-sdk-and-java"></a>快速入门：使用 SDK 和 Java 请求和筛选图像

必应图像搜索 SDK 提供了用于图像查询以及对结果进行分析的 REST API 功能。 

Git Hub 上提供了 [Java 必应图像搜索 SDK 示例的源代码](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master/Search/BingImageSearch)。 

## <a name="application-dependencies"></a>应用程序依赖项
在“搜索”下获取[认知服务访问密钥](https://azure.microsoft.com/try/cognitive-services/)。 通过使用 Maven、Gradle 或其他依赖项管理系统安装必应图像搜索 SDK 依赖项。 Maven POM 文件需要以下声明：
```
 <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.cognitiveservices</groupId>
      <artifactId>azure-cognitiveservices-imagesearch</artifactId>
      <version>0.0.1-beta-SNAPSHOT</version>
    </dependency>
 </dependencies> 
```
## <a name="image-search-client"></a>图像搜索客户端
向类实现中添加以下导入。
```
import com.microsoft.azure.cognitiveservices.imagesearch.*;
import com.microsoft.azure.cognitiveservices.imagesearch.ImageObject;
import com.microsoft.azure.cognitiveservices.imagesearch.PivotSuggestions;
import com.microsoft.azure.cognitiveservices.imagesearch.Query;
import com.microsoft.azure.cognitiveservices.imagesearch.implementation.ImageInsightsInner;
import com.microsoft.azure.cognitiveservices.imagesearch.implementation.ImageSearchAPIImpl;
import com.microsoft.azure.cognitiveservices.imagesearch.implementation.ImagesInner;
import com.microsoft.azure.cognitiveservices.imagesearch.implementation.TrendingImagesInner;
import com.microsoft.rest.credentials.ServiceClientCredentials;
import okhttp3.Interceptor;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
```
实现 **ImageSearchAPIImpl** 客户端，它需要 **ServiceClientCredentials** 类的一个实例。
```
public static ImageSearchAPIImpl getClient(final String subscriptionKey) {
    return new ImageSearchAPIImpl("https://api.cognitive.microsoft.com/bing/v7.0/",
            new ServiceClientCredentials() {
                @Override
                public void applyCredentialsFilter(OkHttpClient.Builder builder) {
                    builder.addNetworkInterceptor(
                            new Interceptor() {
                                @Override
                                public Response intercept(Chain chain) throws IOException {
                                    Request request = null;
                                    Request original = chain.request();
                                    // Request customization: add request headers
                                    Request.Builder requestBuilder = original.newBuilder()
                                            .addHeader("Ocp-Apim-Subscription-Key", subscriptionKey);
                                    request = requestBuilder.build();
                                    return chain.proceed(request);
                                }
                            });
                }
            });
}

```
搜索关于“Canadian Rockies”的图像。 验证结果数。 输出 **firstImageResult**、**pivotSuggestions** 和 **queryExpansions** 参数的值。
```
public static void imageSearch(String subscriptionKey)
{
     ImageSearchAPIImpl client = ImageSrchSDK.getClient(subscriptionKey);

    try
    {
        ImagesInner imageResults = client.searchs().list("canadian rockies");
        System.out.println("\r\nSearch images for query \"canadian rockies\"");

        if (imageResults == null)
        {
            System.out.println("No image result data.");
        }
        else
        {
            // Image results
            if (imageResults.value().size() > 0)
            {
                ImageObject firstImageResult = imageResults.value().get(0);

                System.out.println(String.format("Image result count: %d", imageResults.value().size()));
                System.out.println(String.format("First image insights token: %s", firstImageResult.imageInsightsToken()));
                System.out.println(String.format("First image thumbnail url: %s", firstImageResult.thumbnailUrl()));
                System.out.println(String.format("First image content url: %s", firstImageResult.contentUrl()));
            }
            else
            {
                System.out.println("Couldn't find image results!");
            }

            System.out.println(String.format("Image result total estimated matches: %s", imageResults.totalEstimatedMatches()));
            System.out.println(String.format("Image result next offset: %s", imageResults.nextOffset()));

            // Pivot suggestions
            if (imageResults.pivotSuggestions().size() > 0)
            {
                PivotSuggestions firstPivot = imageResults.pivotSuggestions().get(0);

                System.out.println(String.format("Pivot suggestion count: %d", imageResults.pivotSuggestions().size()));
                System.out.println(String.format("First pivot: %s", firstPivot.pivot()));

                if (firstPivot.suggestions().size() > 0)
                {
                    Query firstSuggestion = firstPivot.suggestions().get(0);

                    System.out.println(String.format("Suggestion count: %s", firstPivot.suggestions().size()));
                    System.out.println(String.format("First suggestion text: %s", firstSuggestion.text()));
                    System.out.println(String.format("First suggestion web search url: %s", firstSuggestion.webSearchUrl()));
                }
                else
                {
                    System.out.println("Couldn't find suggestions!");
                }
            }
            else
            {
                System.out.println("Couldn't find pivot suggestions!");
            }

            // Query expansions
            if (imageResults.queryExpansions().size() > 0)
            {
                Query firstQueryExpansion = imageResults.queryExpansions().get(0);

                System.out.println(String.format("Query expansion count: %d", imageResults.queryExpansions().size()));
                System.out.println(String.format("First query expansion text: %s", firstQueryExpansion.text()));
                System.out.println(String.format("First query expansion search link: %s", firstQueryExpansion.searchLink()));
            }
            else
            {
                System.out.println("Couldn't find query expansions!");
            }
        }
    }

    catch (ErrorResponseException ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage());
    }

}

```
搜索关于“Gibraltar”的图像并针对动画 GIF 和宽屏比率进行筛选。 验证结果数。 输出第一个结果的 **insightsToken**、**thumbnailUrl** 和 **webUrl** 参数的值。
```
public static void imageSearchWithFilters(String subscriptionKey)
{
     ImageSearchAPIImpl client = ImageSrchSDK.getClient(subscriptionKey);

    try
    {
        ImagesInner imageResults = client.searchs().list("Gibraltar", null, null, null, null, ImageAspect.WIDE, null,
                null, null, null, null, null, null, ImageType.ANIMATED_GIF, null, null, null, null, null, null,
                null, null, null, null, null, null, null);
        System.out.println("\r\nSearch images for \"Gibraltar\" results that are animated gifs and wide aspect");

        if (imageResults == null)
        {
            System.out.println("Didn't see any image result data.");
        }
        else
        {
            // First image result
            if (imageResults.value().size() > 0)
            {
                ImageObject firstImageResult = imageResults.value().get(0);

                System.out.println(String.format("Image result count: %s", imageResults.value().size()));
                System.out.println(String.format("First image insightsToken: %s", firstImageResult.imageInsightsToken()));
                System.out.println(String.format("First image thumbnail url: %s", firstImageResult.thumbnailUrl()));
                System.out.println(String.format("First image web search url: %s", firstImageResult.webSearchUrl()));
            }
            else
            {
                System.out.println("Couldn't find image results!");
            }
        }
    }

    catch (ErrorResponseException ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage());
    }

}

```
搜索热门图像。 验证 **categories** 和 **tiles** 参数。
```
public static void imageTrending(String subscriptionKey)
{
    ImageSearchAPIImpl client = ImageSrchSDK.getClient(subscriptionKey);

    try
    {
        TrendingImagesInner trendingResults = client.trendings().list();
        System.out.println("\r\nSearch trending images");

        if (trendingResults == null)
        {
            System.out.println("Didn't see any trending image data.");
        }
        else
        {
            // Categories of images
            if (trendingResults.categories().size() > 0)
            {
                TrendingImagesCategory firstCategory = trendingResults.categories().get(0);
                System.out.println(String.format("Category count: %d", trendingResults.categories().size()));
                System.out.println(String.format("First category title: %s", firstCategory.title()));

                // Tiles for images
                if (firstCategory.tiles().size() > 0)
                {
                    TrendingImagesTile firstTile = firstCategory.tiles().get(0);
                    System.out.println(String.format("Tile count: %d", firstCategory.tiles().size()));
                    System.out.println(String.format("First tile text: %s", firstTile.query().text()));
                    System.out.println(String.format("First tile url: %s", firstTile.query().webSearchUrl()));
                }
                else
                {
                    System.out.println("Couldn't find tiles!");
                }
            }
            else
            {
                System.out.println("Couldn't find categories!");
            }
        }
    }

    catch (ErrorResponseException ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage());
    }

}

```
使用查询“Degas”搜索图像，然后搜索第一个图像结果的详细信息。 
```
public static void imageDetail(String subscriptionKey)
{
    ImageSearchAPIImpl client = ImageSrchSDK.getClient(subscriptionKey);

    try
    {
        ImagesInner imageResults = client.searchs().list("degas");
        if (imageResults.value().size() > 0)
        {
            ImageObject firstImage = imageResults.value().get(0);
            List<ImageInsightModule> modules = new ArrayList<ImageInsightModule>();
            modules.add(ImageInsightModule.ALL);
            ImageInsightsInner imageDetail = client.details().list("degas", null, null, null, null, null, null, null,
                null, null, null, null, null, null, firstImage.imageInsightsToken(), modules, "en-us",
                null, null);
                    //query: "degas", insightsToken: firstImage.ImageInsightsToken, modules: modules).Result;
            System.out.println(String.format("\r\nSearch detail for image insightsToken=%s",
                    firstImage.imageInsightsToken()));

            if (imageDetail != null)
            {
                // Insights token
                System.out.println(String.format("Expected image insights token: %s",
                        imageDetail.imageInsightsToken()));

                // Best representative query
                if (imageDetail.bestRepresentativeQuery() != null)
                {
                    System.out.println(String.format("Best representative query text: %s",
                            imageDetail.bestRepresentativeQuery().text()));
                    System.out.println(String.format("Best representative query web search url: %s",
                            imageDetail.bestRepresentativeQuery().webSearchUrl()));
                }
                else
                {
                    System.out.println("Couldn't find best representative query!");
                }

                // Image caption
                if (imageDetail.imageCaption() != null)
                {
                    System.out.println(String.format("Image caption: %s",
                            imageDetail.imageCaption().caption()));
                    System.out.println(String.format("Image caption data source url: %s",
                            imageDetail.imageCaption().dataSourceUrl()));
                }
                else
                {
                    System.out.println("Couldn't find image caption!");
                }

                // Pages that include the image
                if (imageDetail.pagesIncluding().value().size() > 0)
                {
                    ImageObject firstPage = imageDetail.pagesIncluding().value().get(0);
                    System.out.println(String.format("Pages including count: %d",
                            imageDetail.pagesIncluding().value().size()));
                    System.out.println(String.format("First page content url: %s",
                            firstPage.contentUrl()));
                    System.out.println(String.format("First page name: %s",
                            firstPage.name()));
                    System.out.println(String.format("First page date published: %s",
                            firstPage.datePublished()));
                }
                else
                {
                    System.out.println("Couldn't find any pages including this image!");
                }

                // Related searches
                if (imageDetail.relatedSearches().value().size() > 0)
                {
                    Query firstRelatedSearch = imageDetail.relatedSearches().value().get(0);
                    System.out.println(String.format("Related searches count: %d",
                            imageDetail.relatedSearches().value().size()));
                    System.out.println(String.format("First related search text: %s",
                            firstRelatedSearch.text()));
                    System.out.println(String.format("First related search web search url: %s",
                            firstRelatedSearch.webSearchUrl()));
                }
                else
                {
                    System.out.println("Couldn't find any related searches!");
                }

                // Images that are visually similar
                if (imageDetail.visuallySimilarImages().value().size() > 0)
                {
                    ImageObject firstVisuallySimilarImage = imageDetail.visuallySimilarImages().value().get(0);
                    System.out.println(String.format("Visually similar images count: %d",
                            imageDetail.relatedSearches().value().size()));
                    System.out.println(String.format("First visually similar image name: %s",
                            firstVisuallySimilarImage.name()));
                    System.out.println(String.format("First visually similar image content url: %s",
                            firstVisuallySimilarImage.contentUrl()));
                    System.out.println(String.format("First visually similar image size: %s",
                            firstVisuallySimilarImage.contentSize()));
                }
                else
                {
                    System.out.println("Couldn't find any related searches!");
                }

                // Image tags
                if (imageDetail.imageTags().value().size() > 0)
                {
                    InsightsTag firstTag = imageDetail.imageTags().value().get(0);
                    System.out.println(String.format("Image tags count: %d",
                            imageDetail.imageTags().value().size()));
                    System.out.println(String.format("First tag name: %s",
                            firstTag.name()));
                }
                else
                {
                    System.out.println("Couldn't find any related searches!");
                }
            }
            else
            {
                System.out.println("Couldn't find detail about the image!");
            }
        }
        else
        {
            System.out.println("Couldn't find image results!");
        }
    }

    catch (ErrorResponseException ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage());
    }
}
```
将本文中描述的方法添加到一个类中，并为该类添加一个用于执行代码的主函数。
```
package ImageSDK;
import com.microsoft.azure.cognitiveservices.imagesearch.*;

public class ImageSrchSDK {

    public static void main(String[] args) {
    
        imageSearch("YOUR-SUBSCRIPTION-KEY");
        imageSearchWithFilters("YOUR-SUBSCRIPTION-KEY");
        imageTrending("YOUR-SUBSCRIPTION-KEY");
        imageDetail("YOUR-SUBSCRIPTION-KEY");

    // Include the methods described in this article.
}

```
## <a name="next-steps"></a>后续步骤

[认知服务 Java SDK 示例](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples)
