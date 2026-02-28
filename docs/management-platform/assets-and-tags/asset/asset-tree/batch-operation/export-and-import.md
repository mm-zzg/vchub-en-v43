# Export and Import

Used for backing up models or instances, and for copying models or instances to other asset trees.

## **Export**

Export all data under the model or instance tab to a JSON file.

**Export Model**

In the Model tab, after clicking the Export button, the models in the current asset will be exported as a JSON file.

![alt text](20.png)

![alt text](21.png)

**Export  Instance**

In the Instance tab, after clicking the Export button, the instances in the current asset will be exported as a JSON file.

![alt text](22.png)

![alt text](23.png)

**Model JSON example:**

 [tags_20240123154106.json](https://docs.wagoscada.cn/wiki/api/wiki/editor/QHXVK91b/QpQSaNuz/resources/space%3A23PH16Z2?token=W.wNE97FCuk47_v-XXTk3fHr8QneP06TpGB_FjplKZUXK-aL89VdH1v_4mCJ8GAAGAIIAfqCiJBW10xgg9NBt1b6j2WqJYbQ)

**Instance JSON example:**

 [tags_20240123154106.json](https://docs.wagoscada.cn/wiki/api/wiki/editor/QHXVK91b/QpQSaNuz/resources/space%3A23PH16Z2?token=W.wNE97FCuk47_v-XXTk3fHr8QneP06TpGB_FjplKZUXK-aL89VdH1v_4mCJ8GAAGAIIAfqCiJBW10xgg9NBt1b6j2WqJYbQ)

## **Import**

Import the exported JSON file.

**Import Model**

In the Model tab, click the Batch Operation button.

![alt text](24.png)

In the pop-up window, click the "Import" button.

![alt text](25.png)

**Import Instance**

In the Instance tab, click the Batch Operation button.

![alt text](26.png)

In the pop-up window, click the "Import" button.

![alt text](27.png)

**Notes:**

1. After clicking the More button, the user can choose to import a JSON file that was previously exported. The imported file must match the current tab (Model or Instance); otherwise, an error message will be displayed.<br>
 ![alt text](28.png)
 
2. When importing instance data separately, ensure that the corresponding model objects exist in the current tree; otherwise, the import will fail.
