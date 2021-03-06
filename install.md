# Prism Install

Prism is installed using a Helm chart. During Helm chart deployment, Prism resources are created: 

1. API deployment and services
1. UI deployment 
1. Prism namespace
1. Action config maps 
1. Builtin substitutions  
1. Status mappings 

## Prism namespace 

All prism Kubernetes resources are created in the prism namespace.  The prism namespace is built equivalent to issuing this command: 

```
kubectl create namespace prism 
```

## Builtin Substitutions 

Builtin subsitutions are created in config map 'builtin' in the prism namespace: 

```
apiVersion: v1
kind: ConfigMap
metadata:
   name: builtin
   namespace: prism
data:
   icp_console_url: "<ICP console URL>"
   kibana_url: "<Kibana URL>"
   liberty_log_dashboard_prefix: "Liberty-Problems-K5-" 
   liberty_log_dashboard_name: "<Liberty Kibana dashboard name>" 
```

**Internal details**

1. icp_console_url is obtained from TBD 
1. kibana_url is obtained by looking up the host and nodeport of the service named 'kibana'. 
1. liberty_log_dashboard_prefix specifies the static portion of the Liberty Kibana dashboard name. The full name includes a release date. 
1. liberty_log_dashboard_name is obtained by searching for an "id" that starts with the liberty_log_dashboard_prefix in the output from the following API invocation: 

   ${kibana_url}/api/saved_objects/dashboard
   
   The output: 

   ```
   {"saved_objects":
      [
         {"id":"Liberty-Problems-K5-20180315","type":"dashboard","version":1, ... }
      ]
   }
   ```
