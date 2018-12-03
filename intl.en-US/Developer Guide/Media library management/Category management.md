# Category management {#concept_jy4_cxv_1fb .concept}

## Overview {#section_xy1_dxv_1fb .section}

For more information about how to install and use the SDK, see [Media library SDK-PHP](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/PHP SDK/Overview.md#).

You can add, delete, modify, and query a category. In addition, pay attention to the following logic:

-   Deleting a category does not automatically clear the category ID of an associated media set.
-   The result returned from the category query API can be displayed in the tree structure or list structure. A nested JSON object is returned in the tree structure, while a plane array is returned in the list structure. You can select a structure based on the actual scenario.

## Add a category {#section_ckf_mxv_1fb .section}

For more information about the parameters, see [API reference \> Media category APIs \> Add a category](../../../../reseller.en-US/API Reference/Media category APIs/AddCategory.md#).

```
include_once 'aliyun-php-sdk-core/Config.php';
  use Mts\Request\V20140618 as Mts;
  $accessKeyID = 'test'; //eplace the value with your AccessKeyID
  $accessKeySecret = 'test'; //Replace the value with your AccessKeySecret
  $profile = DefaultProfile::getProfile('cn-hangzhou',
                                        $accessKeyID,
                                        $accessKeySecret);
  $client = new DefaultAcsClient($profile);
```

```
function addCategory($client, $parentId, $categoryName)
  {
      $request = new Mts\AddCategoryRequest();
      $request->setAcceptFormat('JSON');
      $request->setParentId($parentId);
      $request->setCateName($categoryName);
      $response = $client->getAcsResponse($request);
      return $response;
  }
  $category = addCategory($client, null, 'testroot')->{'Category'};
  print_r('Level: '.$category->{'Level'}.
          "\tParentId: ".$category->{'ParentId'}.
          "\tCateId: ".$category->{'CateId'}.
          "\tCateName: ".$category->{'CateName'}."\n");
```

## Update a category {#section_zqx_vxv_1fb .section}

For more information about the parameters, see [API reference \> Media category APIs \> Update a category name](../../../../reseller.en-US/API Reference/Media category APIs/UpdateCategoryName.md#).

```
function updateCategory($client, $categoryId, $categoryName)
  {
      $request = new Mts\UpdateCategoryNameRequest();
      $request->setAcceptFormat('JSON');
      $request->setCateId($categoryId);
      $request->setCateName($categoryName);
      $response = $client->getAcsResponse($request);
      return $response;
  }
  try {
      updateCategory($client, 12345678, 'updatetestroot'); //Replace the value with your category ID
  } catch (ClientException $e) {
      print_r('ClientException:'."\n");
      print_r($e);
  } catch (ServerException $e) {
      print_r('ServerException:'."\n");
      print_r($e);
  }
```

## Delete a category {#section_ust_xxv_1fb .section}

For more information about the parameters, see [API reference \> Media category APIs \> Delete a category](../../../../reseller.en-US/API Reference/Media category APIs/DeleteCategory.md#).

```
function deleteCategory($client, $categoryId)
  {
      $request = new Mts\DeleteCategoryRequest();
      $request->setAcceptFormat('JSON');
      $request->setCateId($categoryId);
      $response = $client->getAcsResponse($request);
      return $response;
  }
  try {
      deleteCategory($client, 12345678); //Replace the value with your category ID
  } catch(ClientException $e) {
      print_r('ClientException:'."\n");
      print_r($e);
  } catch (ServerException $e) {
      print_r('ServerException:'."\n");
      print_r($e);
  }
```

## Query a category {#section_tgz_zxv_1fb .section}

-   Tree structure

    For more information about the parameters, see [API reference \> Media category APIs \> Retrieve a category tree](../../../../reseller.en-US/API Reference/Media category APIs/CategoryTree.md#).

    ```
    function queryCategoryTree($client)
        {
            $request = new Mts\CategoryTreeRequest();
            $request->setAcceptFormat('JSON');
            $response = $client->getAcsResponse($request);
            return $response;
        }
        function printCategoryTree($categoryTree)
        {
            foreach($categoryTree as $category) {
                for ($i = 0; $i < $category->{'Level'}; $i++) {
                    print_r("--");
                }
                print_r('Level: '.$category->{'Level'}.
                        "\tParentId: ".$category->{'ParentId'}.
                        "\tCateId: ".$category->{'CateId'}.
                        "\tCateName: ".$category->{'CateName'}."\n");
                if (array_key_exists('SubcateList', $category)) {
                    printCategoryTree($category->{'SubcateList'});
                }
            }
        }
        $categoryTree = queryCategoryTree($client)->{'CategoryTree'};
        printCategoryTree(json_decode($categoryTree));
    ```

-   List structure

    For more information about the parameters, see [API reference \> Media category APIs \> Retrieve a category list](../../../../reseller.en-US/API Reference/Media category APIs/ListAllCategory.md#).

    ```
     function queryCategoryList($client)
          {
            $request = new Mts\ListAllCategoryRequest();
            $request->setAcceptFormat('JSON');
            $response = $client->getAcsResponse($request);
            return $response  ;
        }
        $categoryList = queryCategoryList($client)->{'CategoryList'}->{'Category'};
        for ($i = 0; $i < count($categoryList); $i++) {
            print_r('Level: '.$categoryList[$i]->{'Level'}.
                    "\tParentId: ".$categoryList[$i]->{'ParentId'}.
                    "\tCateId: ".$categoryList[$i]->{'CateId'}.
                    "\tCateName: ".$categoryList[$i]->{'CateName ' }."\n");
        }
    ```


