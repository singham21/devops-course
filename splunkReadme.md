# Project Title

Splunk Integration with OCP 4.x

## Getting Started

### Prerequisites

Pre Requsites are as follows
1. Splunk Instance
2. Hec token generated for Splunk
3. Indexes created in Splunk

# Playbook

By using the splunk-implement.yaml playbook it deploys helm charts which includes a Splunk-built Fluentd HEC plugin to ship logs and metadata, and a metrics deployment that captures the cluster metrics into Splunk’s Metric Store to use with the Splunk Analysis Workspace

## Installation

1. Run the playbook splunkocp_prereq.yml\
This playbook will call the SplunkScript role\
Goto SplunkScript role vars folder main.yml and below is the input that has to be configured based on the requirement\
splunkpath is the path in master to download helm, Splunk connect for Kubernetes helm charts and values.yml file.
Project is the project name where the Helm charts are deployed which are Splunk-supported deployment of Fluentd* to the Kubernetes cluster

   ---\
splunkpath: /var/home/core/splunk1\
project: splunk-kubernetes-logging

2. Edit the host file so that only one master will be decommented and all others commented so that the playbook will execute only on one master\

   ansible-playbook -i hosts splunkocp_prereq.yml

3. Edit the values.yaml file according to the splunk configuration\
   Provide Splunk instance ip\
     Hec token of splunk
 
4. Edit the main.yml file in vars folder\
   splunk_path: /var/home/core/splunk1-- Path where values.yml file exists in master
   
     
5. Run the playbook SplunkK8sImplement.yml\
   This playbook will install the helm charts by deploying pods on each node in the cluster which will ship the logs and metadata to the splunk.

    ansible-playbook -i hosts SplunkK8sImplement.yml

## Verification

Goto Splunk instance search and reporting in left after splunk enterprise. In search enter index="openshift" which gives the logs

## Usage

Splunk Connect for Kubernetes is a collection of Helm charts that deploy a Splunk-supported deployment of Fluentd* to your Kubernetes cluster. It includes a Splunk-built Fluentd HEC plugin to ship logs and metadata, and a metrics deployment that captures your cluster metrics into Splunk’s Metric Store to use with the Splunk Analysis Workspace.