---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-16"

keywords: openshift, roks, rhoks, rhos, http2, quota

subcollection: openshift

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}



# Service limitations
{: #openshift_limitations}

{{site.data.keyword.openshiftlong}} and the OpenShift open source project come with default service settings and limitations to ensure security, convenience, and basic functionality. Some of the limitations you might be able to change where noted.
{: shortdesc}
<br>

If you anticipate reaching any of the following Red Hat OpenShift on IBM Cloud limitations, [contact IBM Support](/docs/get-support?topic=get-support-getting-customer-support) and provide the cluster ID, the new quota limit, and the region in your support ticket.
{: tip}

## Service and quota limitations
{: #tech_limits}

Red Hat OpenShift on IBM Cloud comes with the following service limitations and quotas that apply to all clusters, independent of what infrastructure provider you plan to use. Keep in mind that the [classic](#classic_limits) and [VPC](#ks_vpc_gen2_limits) cluster limitations also apply.
{: shortdesc}

| Category | Description |
| -------- | ----------- |
| API rate limits | 200 requests per 10 seconds to the Red Hat OpenShift on IBM Cloud API from each unique source IP address. |
| App deployment | The apps that you deploy to and services that you integrate with your cluster must be able to run on the operating system of the worker nodes. |
| Cluster quota | You cannot exceed 100 clusters per region and per [infrastructure provider](/docs/openshift?topic=openshift-infrastructure_providers). If you need more than 100 clusters, [contact IBM Support](/docs/get-support?topic=get-support-getting-customer-support). In the support case, include the new cluster quota limit for the region and infrastructure provider that you want. |
| Container images | You cannot use the [Container Image Security Enforcement (CISE) Helm chart](/docs/Registry?topic=Registry-security_enforce) with OpenShift clusters. |
| Free clusters | You can create only standard clusters, not free clusters. Instead, you can create a free Kubernetes cluster, and then redeploy the apps that you try out in the Kubernetes cluster to your OpenShift cluster. |
| Kubernetes | Make sure to review the [Kubernetes project limitations](https://kubernetes.io/docs/setup/best-practices/cluster-large/){: external}. |
| OpenShift | Make sure to review the [OpenShift Container Platform limitations](https://docs.openshift.com/container-platform/4.3/scalability_and_performance/planning-your-environment-according-to-object-maximums.html){: external} for your version.|
| Kubernetes pod logs | To check the logs for individual app pods, you can use the terminal to run `oc logs <pod name>`. Do not use the Kubernetes dashboard to stream logs for your pods, which might cause a disruption in your access to the Kubernetes dashboard. |
| Logging | <img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> **OpenShift 3.11 only**: <ul><li>You cannot run the Ansible playbook to deploy the [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.openshift.com/container-platform/3.11/install_config/aggregate_logging.html){: external} because you cannot modify the default configuration of the Red Hat OpenShift on IBM Cloud cluster.</li><li>Collecting and forwarding API audit logs to {{site.data.keyword.la_full_notm}} is not supported.</li></ul> |
| Monitoring | <ul><li>Because IBM manages your cluster master, event alerting for the master is disabled. IBM monitors your cluster master and fixes issues as they are detected. For this reason, in the Administrator perspective of the OpenShift, you might see a `Not available` message for the control plane status.</li><li>The [built-in Prometheus](/docs/openshift?topic=openshift-deploy_app#openshift_access_oc_services) alert manager includes two rules that display as active alerts in a `FIRING` state: `KubeControllerManagerDown` and `KubeSchedulerDown`. These components are part of the IBM-managed cluster master, so you can ignore these alerts.</li></ul>|
| Multifactor authentication | If your account uses [multifactor authentication (MFA)](/docs/iam?topic=iam-types), the OpenShift web console cannot authenticate and does not work. |
| Pod instances | You can run 110 pods per worker node. If you have worker nodes with 11 CPU cores or more, you can support 10 pods per core, up to a limit of 250 pods per worker node. The number of pods includes `kube-system` and `ibm-system` pods that run on the worker node. For improved performance, consider limiting the number of pods that you run per compute core so that you do not overuse the worker node. For example, on a worker node with a `b3c.4x16` flavor, you might run 10 pods per core that use no more than 75% of the worker node total capacity. |
| Worker node quota | You cannot exceed 500 worker nodes across all clusters in a region, per [infrastructure provider](/docs/openshift?topic=openshift-infrastructure_providers). If you need more than 500 worker nodes in a region, [contact IBM Support](/docs/get-support?topic=get-support-getting-customer-support). In the support case, include the new worker node quota limit for the region and infrastructure provider that you want.|
| Worker pool size | You must have a minimum of 2 worker nodes per zone in your worker pool at all times. You cannot scale worker pools down to zero. Because of the worker node quota, you are limited in the number of worker pools per cluster and number of worker nodes per worker pool. For example, with the default worker node quota of 500 per region, you might have up to 500 worker pools of 1 worker node each in a region with only 1 cluster. Or, you might have 1 worker pool with up to 500 worker nodes in a region with only 1 cluster. |
{: summary="This table contains information on general Red Hat OpenShift on IBM Cloud limitations. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Red Hat OpenShift on IBM Cloud limitations"}

<br />




### Version 4.3 cluster limitations
{: #ocp4_limitations}

Review limitations that are specific to OpenShift version 4.3 clusters. Keep in mind that the [service](#tech_limits) and [classic cluster](#classic_limits) or [VPC cluster](#ks_vpc_gen2_limits) limitations also apply.
{: shortdesc}

| Category | Description |
| -------- | ----------- |
| Cluster autoscaling | The Red Hat OpenShift cluster autoscaler from the OpenShift **Administration > Cluster Settings** console or `ClusterAutoscaler` object from the `autoscaling.openshift.io/v1` API is not supported. Instead, use the [`ibm-iks-cluster-autoscaler` Helm plug-in](/docs/openshift?topic=openshift-ca). |
| Cluster updates | You must [update your cluster](/docs/openshift?topic=openshift-update) by using the Red Hat OpenShift on IBM Cloud API, CLI, or console tools. You cannot update your cluster version from OpenShift Container Platform tools such as the OpenShift web console. |
| Container logs | If you use a container logging operator such as Fluentd to send logs to an Elasticsearch stack, you must [update the cluster logging deployment to use the `/var/data` path to container logs](/docs/openshift?topic=openshift-health#oc_logging_operator).|
| Key management service (KMS) provider | You cannot use a KMS provider such as {{site.data.keyword.keymanagementservicelong}} to encrypt secrets in your cluster. |
| Private clusters | Depending on the infrastructure provider, your options for private clusters are limited.<ul><li>**VPC**: When you create your VPC cluster in the {{site.data.keyword.cloud_notm}} console, your cluster has both a public and a private service endpoint. If you want only a private service endpoint, you must create the cluster [in the CLI](/docs/openshift?topic=openshift-clusters#cluster_vpcg2_cli) instead, and include the `--disable-public-service-endpoint` flag. If you include this flag, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers.</li><li>**Classic**:You cannot create classic OpenShift clusters with a private service endpoint. Version 4.3 clusters must have only the public service endpoint enabled. Also, as with version 3.11, you cannot create clusters with only private VLAN connectivity.</li></ul> |
| Logging | To set up an [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.openshift.com/container-platform/4.3/logging/cluster-logging.html){: external}, see [installing the cluster logging operator](/docs/openshift?topic=openshift-health#oc_logging_operator).|
| Service catalog | The service catalog is not supported. Use [Operators](/docs/openshift?topic=openshift-operators#operators_4) instead. Do not use the OperatorHub to install the service catalog. |
| Serverless | The Knative managed add-on is not supported. Instead, try out the tech preview for the [OpenShift Serverless operator](https://docs.openshift.com/container-platform/4.3/serverless/serverless-getting-started.html){: external}. |
| Service mesh | The Istio managed add-on is not supported. Instead, use the [Red Hat service mesh operator](https://docs.openshift.com/container-platform/4.3/service_mesh/servicemesh-release-notes.html){: external}. **Note**: The default {{site.data.keyword.cloud_notm}} configuration of the routers enables host networking, which is not compatible with the service mesh network policy. For the service mesh ingress to work, [apply a network policy](https://gist.githubusercontent.com/kitch/39c504a2ed9e381c2aadea436d5b52e4/raw/d8efa69f41d41425b16bb363a881a98d40d3708c/mesh-policy.yaml){: external}.|
| Virtual private cloud (VPC) | As with version 3.11, you cannot create OpenShift version 4.3 clusters in a VPC. |
{: summary="This table contains information on limitations for OpenShift Container Platform version 4.3 clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="OpenShift Container Platform version 4.3 cluster limitations"}



## Classic cluster limitations
{: #classic_limits}

Classic infrastructure clusters in Red Hat OpenShift on IBM Cloud are released with the following limitations.
{: shortdesc}

### Compute
{: #classic_compute_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Operating system | You cannot create a cluster with worker nodes that run multiple operating systems, such as OpenShift on Red Hat Enterprise Linux and community Kubernetes on Ubuntu. |
| Worker node flavors | Worker nodes are available in [select flavors](/docs/openshift?topic=openshift-planning_worker_nodes#shared_dedicated_node) of compute resources. |
| Worker node host access | For security, you cannot SSH into the worker node compute host. |
| Worker node instances | You cannot exceed 500 worker nodes across all clusters in a region. If you see an IBM Cloud infrastructure capacity limit on the number of instances per data center or that are ordered each month, [contact IBM Support](/docs/get-support?topic=get-support-getting-customer-support).  |
{: summary="This table contains information on compute limitations for classic clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Classic cluster compute limitations"}

### Networking
{: #classic_networking_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Ingress ALBs | <ul><li>The Ingress application load balancer (ALB) can process 32,768 connections per second. If your Ingress traffic exceeds this number, [scale up the number of ALB replicas](/docs/openshift?topic=openshift-ingress-manage#scale_albs) in your cluster to handle the increased workload.</li><li>HTTP/2 is not supported.</li><li>The names of the `ClusterIP` services that expose your apps must be unique across all namespaces in your cluster.</li></ul> |
| Network load balancers (NLB)| <ul><li>You cannot create version 2.0 network load balancers (NLB 2.0) to expose your apps.</li><li>You cannot create subdomains for private NLBs.</li><li>You can register up to 128 subdomains. This limit can be lifted on request by opening a [support case](/docs/get-support?topic=get-support-getting-customer-support).</li></ul> | 
| Private VLANs only | Private network load balancers (NLBs) cannot be registered with the domain name server (DNS), so the cluster cannot be created with only a private network interface. Worker nodes must be connected to both public and private VLANs. You can still create a private service to expose your apps on only the private network. |
| Service endpoints | When you create a cluster, you must enable the public service endpoint, and can optionally enable the private service endpoint in version 3.11. | 
| strongSwan VPN service | See [strongSwan VPN service considerations](/docs/openshift?topic=openshift-vpn#strongswan_limitations). |
| Service IP addresses | You can have 65,000 IPs per cluster in the 172.21.0.0/16 range that you can assign to Kubernetes services within the cluster. |
| Subnets per VLAN | Each VLAN has a limit of 40 subnets. |
{: summary="This table contains information on networking limitations for classic clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Classic cluster networking limitations"}

### Storage
{: #classic_storage_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Volume instances | You can have a total of 250 IBM Cloud infrastructure file and block storage volumes per account. If you mount more than this amount, you might see an "out of capacity" message when you provision persistent volumes. For more FAQs, see the [file](/docs/FileStorage?topic=FileStorage-file-storage-faqs#provision) and [block](/docs/BlockStorage?topic=BlockStorage-block-storage-faqs#authlimit) storage docs. If you want to mount more volumes, [contact IBM Support](/docs/get-support?topic=get-support-getting-customer-support). In your support ticket, include your account ID and the new file or block storage volume quota that you want.  |
| File storage | Because of the way that {{site.data.keyword.cloud_notm}} NFS file storage configures Linux user permissions, you might encounter errors when you use file storage. If so, you might need to configure [OpenShift Security Context Constraints](https://docs.openshift.com/container-platform/4.3/authentication/managing-security-context-constraints.html){: external} or use a different storage type. |
{: summary="This table contains information on storage limitations for classic clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Classic cluster storage limitations"}

<br />


## VPC Gen 2 compute cluster limitations
{: #ks_vpc_gen2_limits}

VPC Generation 2 compute clusters in Red Hat OpenShift on IBM Cloud are released with the following limitations. Additionally, all the underlying [VPC quotas, VPC limits](/docs/vpc?topic=vpc-quotas), [VPC service limitations](/docs/vpc?topic=vpc-limitations), and [regular service limitations](#tech_limits) apply.
{: shortdesc}

### Compute
{: #vpc_gen2_compute_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Encryption | The secondary disks of your worker nodes are encrypted at rest by default by the [underlying VPC infrastructure provider](/docs/vpc?topic=vpc-block-storage-about#about-vpc-provider-managed-encryption). However, you cannot [bring your own encryption to the underlying virtual server instances](/docs/vpc?topic=vpc-creating-instances-byok).|
| Location | VPC Gen 2 clusters are available only in [select multizone metro locations](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc-gen2). |
| Operating system | You cannot create a cluster with worker nodes that run multiple operating systems, such as OpenShift on Red Hat Enterprise Linux and community Kubernetes on Ubuntu. |
| Versions | VPC Gen 2 clusters must run OpenShift version 4.3 or later. |
| Virtual Private Cloud | See [Known limitations](/docs/vpc-on-classic?topic=vpc-on-classic-known-limitations) and [Quotas](/docs/vpc-on-classic?topic=vpc-on-classic-quotas). |
| v2 API | VPC clusters use the [Red Hat OpenShift on IBM Cloud v2 API](/docs/openshift?topic=openshift-cs_api_install#api_about). The v2 API is currently under development, with only a limited number of API operations currently available. You can run certain v1 API operations against the VPC cluster, such as `GET /v1/clusters` or `ibmcloud oc cluster ls`, but not all the information that a Classic cluster has is returned or you might experience unexpected results. For supported VPC v2 operations, see the [CLI reference topic for VPC commands](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_classic_vpc_about). |
| Worker node flavors | Only certain flavors are available for worker node [virtual machines](/docs/openshift?topic=openshift-planning_worker_nodes#vm). Bare metal machines are not supported.|
| Worker node host access | For security, you cannot SSH into the worker node compute host. |
| Worker node instances | You can have up to 100 worker nodes per VPC cluster. This limit can be lifted on request by opening a [support case](/docs/get-support?topic=get-support-getting-customer-support).|
| Worker node updates | You cannot update or reload worker nodes. Instead, you can delete the worker node and rebalance the worker pool with the `ibmcloud oc worker replace` command. |
{: summary="This table contains information on compute limitations for VPC Gen 2 clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="VPC Gen 2 cluster compute limitations"}

### Networking
{: #vpc_gen2_networking_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Network speeds | [VPC Gen 2 compute profile network speeds](/docs/vpc?topic=vpc-profiles) refer to the speeds of the worker node interfaces. The maximum speed available to your worker nodes is `16Gbps`. Because IP in IP encapsulation is required for traffic between pods that are on different VPC Gen 2 worker nodes, data transfer speeds between pods on different worker nodes might be slower, about half the compute profile network speed. Overall network speeds for apps that you deploy to your cluster depend on the worker node size and application's architecture. |
| NodePort | You can access an app through a NodePort only if you are connected to your private VPC network, such as through a VPN connection. To access an app from the internet, you must use a VPC load balancer or Ingress service instead. |
| Pod network | VPC access control lists (ACLs) filter incoming and outgoing traffic for your cluster at the subnet level, such as traffic through the VPC load balancer. To control traffic within the cluster at the pod-to-pod level, you cannot use VPC security groups or ACLs. Instead, use [Calico](/docs/openshift?topic=openshift-network_policies) and [Kubernetes network policies](/docs/openshift?topic=openshift-vpc-network-policy#kubernetes_policies), which can control the pod-level network traffic that uses IP in IP encapsulation. |
| Public gateway | You must attach a public gateway to the VPC subnet so that the worker nodes have access to the public network, to run default OpenShift components such as the web console and OperatorHub.|
| Service endpoints | When you create your VPC cluster in the {{site.data.keyword.cloud_notm}} console, your cluster has both a public and a private service endpoint. If you want only a private service endpoint, you must create the cluster [in the CLI](/docs/openshift?topic=openshift-clusters#cluster_vpcg2_cli) instead, and include the `--disable-public-service-endpoint` flag. If you include this flag, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers.|
| strongSwan VPN service | The strongSwan service is not supported. To connect your cluster to resources in an on-premises network or another VPC, see [Using VPN with your VPC](/docs/vpc?topic=vpc-vpn-onprem-example). |
| Subnets | <ul><li>See [VPC networking limitations](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_limitations).</li><li>Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.</li></ul> |
| VPC load balancer | See [VPC load balancer limitations](/docs/openshift?topic=openshift-vpc-lbaas#lbaas_limitations). |
| VPC security groups | You must [allow inbound traffic requests to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-network-policy#security_groups). |
{: summary="This table contains information on networking limitations for VPC Gen 2 clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="VPC Gen 2 cluster networking limitations"}

### Storage
{: #vpc_gen2_storage_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Supported types | You can set up {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.databases-for}} only. |
| Unsupported types | NFS File Storage and {{site.data.keyword.block_storage_is_short}} are not supported. |
{: summary="This table contains information on storage limitations for VPC Gen 2 clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="VPC Gen 2 cluster storage limitations"}





