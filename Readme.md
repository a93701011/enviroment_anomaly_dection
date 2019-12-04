
## AIot + Machine Learning Service

### Azure Resoure
1.IoT Hub  
2.Function App  
3.Event Hub  
4.Stream Analytics  
5.Machine Learning Service  
 
### IoT Hub

ˋˋˋbash

az iot hub create --resource-group MyResourceGroup --name MyIotHub --sku S1 --location westus --partition-count 4
az iot hub device-identity create --hub-name MyIotHub --device-id MyPythonDevice  
az iot hub device-identity show-connection-string --hub-name MyIotHub --device-id MyPythonDevice --output table

ˋˋˋ

### Function App

### Event Hub

### Stream Analytics

### Machine Learning Service Workspace
