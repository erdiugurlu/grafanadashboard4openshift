# Custom Dashboard For Openshift Clusters

OpenShift cluster can be measured at various levels by using this dashboard. You can get general metrics of OpenShift Clusters on this dashboard. Such as, Cluster CPU Usage, Cluster Memory Usage and Cluster Disk Usage etc...

## Requirements

This dashboard was deployed and tested with OpenShift 4.6 and Grafana v7.3.6. 

Besides OpenShift Monitoring Tech Stack, you should have a custom Grafana server.

## Deployment

Before importing this dashboard, Grafana server that we will use should integrate with Anthos Query endpoint of the OpenShift cluster. 

In order to create a Promotheus datasource, we need a Bearer Token of a Service Account which is granted the cluster-monitoring-view cluster role.

grafana-serviceaccount was created in the OpenShift cluster. 

```
oc create serviceaccount grafana-serviceaccount
```
The service account was granted the cluster-monitoring-view.
```
oc adm policy add-cluster-role-to-user cluster-monitoring-view -z grafana-serviceaccount
```
In order use the token to connect the Promotheus server. 
```
oc serviceaccounts get-token grafana-serviceaccount -n my-grafana
```

After this action, you can use the token and Thanos Query endpoint to connect the Promotheus server in your cluster. 

Afterwards, you can import the dashboard json file. 

If you are unable to see some information on the dashboard, please make sure that the Promotheus server runs and store the data.