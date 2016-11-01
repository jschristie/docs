# Load Balancer configuration for Gluu CE Cluster

## Using Amazon ELB

  - Select 'Classic Load Balancer'
  - Click on 'Create Load Balancer'
  - Define Load Balancer settings: 
     - Load Balancer Name: Anything deployer prefer
     - Create LB Inside: My Default VPC ( by default )
     - Load Balancer Protocol: HTTPS/443 
     - Instance Protocol: HTTPS/443
  - Assign Security Groups: Default
  - Configure Security Settings: Deployer can either use 'ACM' to generate cert or can update existing certificate and key. For this doc creation, we are using our existing cert/key. 
  - Configure Health Check: 
     - Ping Protocol: HTTPS
     - Ping Port: 443
     - Pint Path: /monitoring.html ( Deployer need to put 'monitoring.html' inside Gluu Server container:/var/www/html/ )
     - Advanced Details: Default
  - Add EC2 

### SSL cert/key for Load balancer

-  openssl genrsa -out clustering_gluu_org_private_key.pem 204
- openssl req -sha256 -new -key clustering_gluu_org_private_key.pem -out clustering_gluu_org_csr.pem
- openssl x509 -req -days 365 -in clustering_gluu_org_csr.pem -signkey clustering_gluu_org_private_key.pem -out clustering_gluu_org_crt.pem


#### Configure custome hostname

https://console.aws.amazon.com/route53/home?

 - Hosted Zone
 - 'Go To Record Sets'
