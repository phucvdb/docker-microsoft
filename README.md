# docker-microsoft

###Creating ACS with Swarm Cluster with Powershell

    Login-AzureRmAccount
    Get-AzureRmSubscription
    #sample deployment
    $TemplateUri = "https://raw.githubusercontent.com/phucvdb/azure-quickstart-templates/master/101-acs-swarm/azuredeploy.json"
    $RESOURCE_GROUP_NAME = "ACS-Demo"
    $DEPLOYMENT_NAME = "cli.acs-06092016"
    $REGION = "southeastasia"
    New-AzureRmResourceGroup -Name $RESOURCE_GROUP_NAME -Location $REGION
    New-AzureRmResourceGroupDeployment -Name $DEPLOYMENT_NAME -ResourceGroupName $RESOURCE_GROUP_NAME -TemplateUri $TemplateUri

###Acces to Swarm Cluster
    using ssh with private key to masterFQDN via port 2200
    
    azureuser@...# export DOCKER_HOST=:2375
### Deploy a new container
    user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web
    
    //Checking result via link of agentFQDN
    e.g: http://cliacsdemoagents.southeastasia.cloudapp.azure.com/
    
    
    
