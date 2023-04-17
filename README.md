# IWS-Prometheus-Grafana
 Demo setup for Prometheus and Grafana IWS Dashboard

 **Purpose**:
The purpose of this repository is to provide a sample prometheus.yml file for connection to IBM Workload Scheduler 9.5 FP 4 an 10.1. The example is for users who attended the IBM AIOps IwS  Track on May 04 2023. It is to allow IWS admins to have a go themselves before looking at how to do it internally and get benefits from Observaility.

 **Assumptions**:
The following assumptions have been made when these instructions were put together:
1. Docker is installed already within the readers environment, either on the person's desktop/laptop or a server
2. The reader has access to the internet, without a restriction to connect to the test MDM & DWC
3. The reader is an experienced IWS administrator who will understand the ouput shown on the Grafana Dashboard

If you find any assumptions I've missed then please let me know in the issues section.

 **Steps**:
1. Download the prometheus.yml file and put it in an accessable folder. This file will be known as path-to-your-prometheus.yml
2. Install the docker container for Prometheus using:
   1. docker run -d --name prometheus -p 9090:9090 -v “path-to-your-prometheus.yml":/etc/prometheus/prometheus.yml prom/Prometheus
3. Check things are working correctly from your browser, http://hostname:9090, if you're installing on your laptop/desktop go to http://localhost/9090.
   1. Go to Status -> Configuration to make sure the right file has been loaded
   2. Go to Status -> Tagets and make sure both MDM and DWC is showing as UP.
4. When this is working correctly then Prometheus is working correctly, become familiar with the interface (e.g. using the metrics explorer (earth symbol) and the metrics shown when you click it.)
5. Install Grafana using:
   1. docker run -d -p 3000:3000 --name grafana grafana/grafana-enterprise
   2. Default ID and Password admin
   3. Change the admin password to something memorable
6. Create a Datasource for Prometheus:
   1. Go to Datasource (Gear symbol)
   2. Add Datasource, select Prometheus
   3. In HTTP, put the URL for the Prometheus container (If in the same Docker Network then use the container IP address and not localhost)
   4. Change the http method to Get
   5. No other paramters need to be changed before pressing Save & test
   6. If it returns successfully then you're good to go
7. Next go to the Automation Hub and download the Grafana Dashboard using the following URL:
   1. https://www.yourautomationhub.io/detail/grafanadashboarddistributedenvironment
   2. Download the json file as an IBM User, no User ID required.
8. Install the Grafana Dashboard and link it to the Prometheus Datasource
   1. Go to Dashboards (four squares in the left hand side)
   2. Select import Dashboard and select the file downloaded
   3. Select the Prometheus datasource as part of the install
9. Go to Dashboards and select "IBM Workload Automation Performance Metrics" dashboard
10. You should now see data being plotted... have fun exploring the data produced. 
 **Conclusions**:
The steps needed to set up Prometheus and Grafana with IWS is straight forward. I hope it gives you the confidence to implement it in your own environment.
