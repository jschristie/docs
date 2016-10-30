# Load Balancer configuration for Gluu CE Cluster

## Using Amazon ELB

### SSL cert/key for Load balancer

-  openssl genrsa -out clustering_gluu_org_private_key.pem 204
- openssl req -sha256 -new -key clustering_gluu_org_private_key.pem -out clustering_gluu_org_csr.pem
- openssl x509 -req -days 365 -in clustering_gluu_org_csr.pem -signkey clustering_gluu_org_private_key.pem -out clustering_gluu_org_crt.pem
