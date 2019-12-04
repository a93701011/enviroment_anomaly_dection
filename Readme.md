
## AIot + Machine Learning Service

### Azure Resoure
1.IoT Hub  
2.Function App  
3.Event Hub  
4.Stream Analytics  
5.Machine Learning Service  
 
### IoT Hub

```bash
az iot hub create --resource-group MyResourceGroup --name MyIotHub --sku S1 --location westus --partition-count 4
az iot hub device-identity create --hub-name MyIotHub --device-id MyPythonDevice  
az iot hub device-identity show-connection-string --hub-name MyIotHub --device-id MyPythonDevice --output table
```
1.	Open the IoT Hub
2. Add consume group <yourname>

### Function App
1. Create Function app
2. new IoT Hub Template
3. Integrate Setting
   -- trigger MyIotHub
   -- output MyEventHub

```bash
#r "Newtonsoft.Json"

using System;
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using System.Net.Http;
using System.Net.Http.Headers;

public static void Run(string myIoTHubMessage,out string outputEventHubMessage, ILogger log)
{
       
    log.LogInformation(myIoTHubMessage);  

    string scoringUri = "http://b765cd3e-2c7d-44f7-99f2-f8d9eb1ac480.southcentralus.azurecontainer.io/score";
    
    HttpClient client = new HttpClient();

    var request = new HttpRequestMessage(HttpMethod.Post, new Uri(scoringUri));
    request.Content = new StringContent(myIoTHubMessage);
    request.Content.Headers.ContentType = new MediaTypeHeaderValue("application/json");
    var response = client.SendAsync(request).Result;
    
    string result_jsonstring = response.Content.ReadAsStringAsync().Result.ToString();
    log.LogInformation(result_jsonstring);
    outputEventHubMessage = result_jsonstring;
}
```

5.	Stream Analytics


### Event Hub

### Stream Analytics
1.	Create another Stream Analytics
2.	Setting input : Event Hub
3.	Setting Output : Power BI
4.	Query 
SELECT
    system.timestamp as time
    ,temperature
    ,humidity
    ,anomaly
into powerbi
FROM
    eventhub timestamp by EventProcessedUtcTime


### Machine Learning Service Workspace
1.	Lunch machine learning workspace studio
2.	Create a Notebook VM compute
3.	Upload Jupyter notebook File
4.	Open amlconfiguration.ipynb, run all cell in this jupyter notebook
5.	Open anomaly detection model.ipynb, run all cells in this jupyter notebook
6.	Go back to the Azure Machine Service Portal
