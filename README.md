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
    
###Demo 1
    Composefile:
    
    web:
        image: "yeasy/simple-web"
        ports:
            - "80:80"
        restart: "always"
        
    user@ubuntu:~$docker-compose up -d
    user@ubuntu:~docker ps
    //browser to AGENTFQDN 
    user@ubuntu:~docker-compose scale web=**3**
        
###Demo 2
    Composefile:
    web:
        image: adtd/web:0.1
        ports:
            - "80:80"
        links:
            - rest:rest-demo-azure.marathon.mesos
    rest:
        image: adtd/rest:0.1
        ports:
            - "8080:8080"
    
    user@ubuntu:~/compose$ docker-compose up -d
    //browser to AGENTFQDN 
    
    
