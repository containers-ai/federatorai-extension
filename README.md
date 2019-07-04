# Federator.ai Extension

**Federator.ai Extension** is a Chrome Extension to provide **NetApp Kubernetes Service** ([NKS](https://nks.netapp.io)) users both Cost Recommendation for Day 1 - Deployment and Cost Monitoring/Analysis/Recommendation for Day 2 - Operation of Kubernetes cluster on public cloud.



## Prerequisites

- [federatorai-operator](https://nks.netapp.io/solutions/gallery/trusted-charts) installed from **NKS Solutions**

  

## Install Federator.ai Extension

- download the latest release of [**Federator.ai Extension**](https://github.com/containers-ai/federatorai-extension/tree/master/release) to the desktop and extract it 

- open the Chrome browser and go to **Extension Management** [(chrome://extensions/)](chrome://extensions/) page.

- enable **Developer Mode** by clicking the toggle switch on the top-right of the page

- click **Load unpacked** button and select **chrome-extension** folder from extracted zip file

- login to [NKS](https://cloud.netapp.com/kubernetes-service), then you can see our recommendations when you deploy a new cluster or manage your clusters

  > **Note**: If the NKS page is opened before extension installed, please reload the NKS page to make it  effect.

  

## How to Use 

1. **Enabling Federator.ai Extension**

   - After Federator.ai Extension is installed, the extension logo ![logo](/images/favicon.png) will show on the top-right corner of chrome navigation bar. Click the logo to enable the extension.

     

2. **Deploying a new Kubernetes cluster**

   - click **Deploy a Cluster Now** from [NKS](https://cloud.netapp.com/kubernetes-service) and select preferred cloud provider

   - follow the wizard to create cluster before 

   - **Federator.ai Extension** will show your deploying cost and recommended allocations for different cloud providers

     

3. **Deploying the example application**

   - deploy the example application - **nginx** in your cluster by running command:

     ```$ kubectl apply -f nginx.yaml```

     **nginx.yaml**:

     ```
     ---
     apiVersion: v1
     kind: Namespace
     metadata:
       name: nginx
     ---
     apiVersion: apps/v1
     kind: Deployment
     metadata:
       name: nginx
       namespace: nginx
       labels:
         app: nginx  # federator.ai uses the label to monitor nginx
     spec:
       selector:
         matchLabels:
           app: nginx
       replicas: 2
       template:
         metadata:
           labels:
             app: nginx
         spec:
           containers:
           - name: nginx
             image: nginx:latest
             ports:
             - containerPort: 80
     ```

     

   - check if these **nginx** pods are running by command

     ``` $ kubectl get pods -n nginx```

     

 4. **Deploying the example application**

    - create the _AlamedaScaler_ CR to monitor **nginx** by command

      ```$ kubectl apply -f alamedaautoscaler.yaml```

      **alamedaautoscaler.yaml**

      ```
      apiVersion: autoscaling.containers.ai/v1alpha1
      kind: AlamedaScaler
      metadata:
        name: alameda-nginx
        namespace: nginx
      spec:
        selector:
          matchLabels:
            app: nginx
      ```

    - check an application's status by running 

      ```$ kubectl get alamedascaler -o yaml --all-namespaces```



5. You can see our recommendation while you manage your cluster on NKS. **Federator.ai** will show the predicted resource usages in the next week and Reserved Instance (RI) recommendation for different providers.

   > **Note**: After _AlamedaScaler_ CR is created, Federator.ai starts to gather resource usage metrics. It takes 5 hours for the first prediction result generated.

