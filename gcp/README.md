By: Raj   raj@acloudfan.com
Content: Part of a course "Hyperledger Fabric Network Setup & Design"
More information: http://acloudfan.com    http://bcmentors.com


Assets specific to GCP
======================
Storage class is the only K8s YAML that is specific to GCP

Setting up fabric in GCP
========================
1. Create a K8s cluster
2. Connect your cluster with the cloud shell
3. Clone this repository
   > git clone https://github.com/acloudfan/HLF-K8s-Cloud.git
4. Setup the storage class
   > cd HLF-K8s-Cloud/gcp
   > kubectl apply -f .
   This will setup the storage class
5. Launch the Acme Orderer
   > cd ..
   > kubectl apply -f ./k8s-acme-orderer.yaml
   Check the logs for 'acme-orderer-0' to ensure there is no error
6. Launch the Acme Peer
   > kubectl apply -f ./k8s-acme-peer.yaml
   Check the logs for 'acme-peer-0' to ensure there is no error
7. Setup the Channel & Join acme peer to it it
   > kubectl exec -it acme-peer-0 /bin/bash
   > ./submit-channel-create.sh
   
   > ./join-channel.sh
   
   Ensure that peer has joined the channel
   > peer channel list

   > exit
9. Launch the budget Peer and join it to the channel
   > kubectl apply -f ./k8s-budget-peer.yaml
   Wait for the container to launch & check the logs for errors

   > kubectl exec -it budget-peer-0 /bin/bash
   > ./fetch-channel-block.sh
   > ./join-channel.sh

   Ensure that peer has joined the channel
   > peer channel list

   > exit
** At this point your K8s Fabric Network is up **

Validating the network
======================
1. Install & Instantiate the test chaincode

   > kubectl exec -it acme-peer-0 /bin/bash

   > ./cc-test.sh  install
   > ./cc-test.sh  instantiate

2. Invoke | Query the chaincode to see the changes in values of a/b
   > ./cc-test.sh  query
   > ./cc-test.sh  invoke

3. Check the values inside the Budget peer
   > kubectl exec -it acme-peer-0 /bin/bash

   > ./cc-test.sh  install

   > ./cc-test.sh  query
   The query should return the same values as you see in acme-peer
   Execute invoke/query in both peers to validate