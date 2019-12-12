
## AIot + Machine Learning Service

### Azure Resoure
1.IoT Hub  
2.Function App  
3.Event Hub  
4.Stream Analytics  
5.Machine Learning Service  
 
### IoT Hub

1. Create the IoT Hub  
2.	Open the IoT Hub  
3. Add consume group <yourname>  
4. Create Device  
4. Get Connection String  

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

### Event Hub

1.	Create a Event Hub  
2.	Create hub in the Event Hub  

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


