# Federator.ai Extension

**Federator.ai Extension** is a Chrome Extension to provide **NetApp Kubernetes Service** ([NKS](https://nks.netapp.io)) users the multi-cloud Cost Recommendation for 'Day 1 - Deployment' of Kubernetes cluster.



## Prerequisites

- [federatorai-operator](https://nks.netapp.io/solutions/gallery/trusted-charts) installed from **NKS Solutions**

  

## Install Federator.ai Extension

- download the latest release of [**Federator.ai Extension**](https://github.com/containers-ai/federatorai-extension/tree/master/release) to the desktop and extract it 

- open the Chrome browser and go to **Extension Management** [(chrome://extensions/)](chrome://extensions/) page.

- enable **Developer Mode** by clicking the toggle switch on the top-right of the page

- click **Load unpacked** button and select **chrome-extension** folder from extracted zip file

- login to **NKS**, then you can see our recommendations when you deploy a new cluster or manage your clusters

  > **Note**: If the NKS page is opened before extension installed, please reload the NKS page to make extension effect.

  

## How to Use 

1. **Enabling Federator.ai Extension**

   - After Federator.ai Extension is installed, the extension logo ![logo](/images/favicon.png) will show on the top-right corner of Chrome navigation bar. Click the logo to enable the extension.

     

2. **Deploying a new Kubernetes cluster**

   - click **Deploy a Cluster Now** from [NKS](https://cloud.netapp.com/kubernetes-service) and select preferred cloud provider

   - follow the wizard to create cluster before 

   - **Federator.ai Extension** will show your deploying cost and recommended allocations for different cloud providers

     

