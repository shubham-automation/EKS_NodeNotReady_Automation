# EKS_NodeNotReady_Automation

1. Create CloudFormation stack using CF_Node_Reboot_Alert_Automation.yaml

2. Copy the value of **ApiUrl** from output of CloudFormation stack

3. For kube-prometheus-stack helm chart use below commands and files
   I. helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   II. helm upgrade --install kube-prometheus-stack prometheus-community/kube-prometheus-stack -f kube-stack-values.yaml
   III. kubectl apply -f prometheus-values.yaml

4. For community prometheus helm chart use below commands and files
   I. helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   II. helm upgrade --install prometheus prometheus-community/prometheus -f prometheus-values.yaml


When EKS worke node goes into NdeNotReady state then alertmanager will send an alert to AWS API Gateway and which will trigger the lambda function that will first check if the node is running or not, if it is running then lambda function will reboot that node else it will first start the node and then reboot it. Once reboot successfully we can see EKS worker node is in ready state.
