## Release Notes

### 2.2.0 TP

The Cloudbreak 2.2.0 TP release is technical preview: it is not suitable for production environments.

____________________________

#### New Features
____________________________

TBD


____________________________

#### Behavioral Changes
____________________________

TBD 

____________________________

#### Fixed Issues 
____________________________

The following issues have been fixed in Cloudbreak 2.2.0 TP: 

| Jira |  Description |
|---|---|
| BUG-91768 | The *Add* button used for adding tags does not work. |
| BUG-90848 | "Do Not Use Security Group" option does not work for a new network. | 
| BUG-91827 | After cluster has been stopped, Event History shows "Infrastructure Has Been Terminated". |
| BUG-91701 | Cluster resize is unclear: the cluster name and cluster information in the text above the scaling controls are incorrect. | 
| BUG-91892 | "Recipe name is already taken" error when using a recipe description longer than 255 characters. | 

 
____________________________

#### Known Issues
____________________________

##### (RMP-10114) Auto-scaling Is Not Available

Auto-scaling functionality is not available in Cloudbreak 2.2.0 TP. 
____________________________



##### (BUG-91835) Default Ambari Node Security Group Has Port 9443 Inbound CIDR Set to 0.0.0.0/0 

By default, port 9443 is set to 0.0.0.0/0 CIDR for inbound access on the default-ambari-security-group.  

*Workaround*: If you choose to use the default-ambari-security-group for your Ambari host group security group, it is strongly recommended that you limit this CIDR in the security group to only allow traffic from your Cloudbreak VM instance IP.  

[Comment]: <> (This item is closed. Need to verify the change.)
____________________________



##### (BUG-91543) Networks With No Subnets Are Not Supported 

You cannot create a cluster using an existing network that does not have any subnets. You must use a network that includes at least one subnet. If you try to use a network with no subnets, the cluster fails with the following error:   

*Infrastructure creation failed. Reason: Invalid value for field 'resource.network': 'https://www.googleapis.com/compute/v1/projects/siq-haas/global/networks/cbd-test'. A subnet mode Network must be specified for Subnetwork creation.: [ resourceType: GCP_SUBNET, resourceName: testgc-20171110211021 ]*
  
*Workaround*: Do not use this option. It will be removed in a future release.  
____________________________



##### (BUG-90985) OpenStack Cluster Creation Fails at Network Configuration

When creating a cluster on OpenStack, if you do not select an existing network and subnet, the cluster fails with an error similar to:  
*Infrastructure creation failed. Reason: At least one of the following properties must be specified: network, network_id.*   
*Infrastructure creation failed. Reason: The Parameter (router_id) was not provided.*

*Workaround*: When creating a cluster on OpenStack, you must select an existing network and subnet. 
____________________________



##### (BUG-91810) Network and Subnet Listed as N/A

When creating a new network and subnet for your cluster, the network and subnet information is unavailable on the cluster details page, showing "N/A".

*Workaround*: If you want to check which network and subnet are used for your cluster, navigate to the cloud provider account and find the cluster instances that were created for your cluster. Next, check which virtual network and subnet they are associated with. The steps vary depending on the provider.  
____________________________



##### (BUG-91077) Node Status Is Not Consistent with Ambari

If your blueprint contains Druid, cluster node status may be "healthy" after a cluster is created, even though the Druid component has not started.     
*Workaround*: Manually start Druid by using Ambari web UI.  
____________________________



##### (BUG-91077) Nodes Are Unhealthy After Sync

If your blueprint contains Druid, cluster node status may change to "unhealthy" after synchronizing with the cloud provider using the "Sync" option.    
*Workaround*: Manually start Druid by using Ambari web UI and then "Sync" again.  
____________________________



##### (BUG-91013) Incorrect Node Status After Cluster Restart 

You may sporadically experience an issue where after you stop and restart a cluster, the node status displayed in the "Hardware" section is incorrect.   

[comment]: <> (Not sure what the workaround is for BUG-91013?)
____________________________



##### (BUG-91071) Syntax Error During Cluster Downscale

When trying to downscale your cluster below the minimum required number of nodes, you may get the following error: *SyntaxError: Unexpected end of JSON input*.
 
*Workaround*: 

Check the *Event History* for more information:  

* If you tried to scale the cluster below the minimum required number of nodes, you will see: *New node(s) could not be removed from the cluster. Reason There is not enough node to downscale. Check the replication factor and the ApplicationMaster occupation.* It may take a few minutes for this message to appear in the the *Event History*.   
* In other cases, you should see a message informing you that downscale was successful. It may take a few minutes for this message to appear in the the *Event History*.  
____________________________





