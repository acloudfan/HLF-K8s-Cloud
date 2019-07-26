#Docker file for setting up the acme peer
FROM hyperledger/fabric-peer:1.4.2

LABEL  maintainer="Rajeev Sakhuja <raj@acloudfan.com>"

#1. Create a folder
RUN mkdir -p /var/hyperledger/config

#2. Copy the crypto for peer crypto
COPY ./config/crypto-config/peerOrganizations/acme.com/peers/peer1.acme.com /var/hyperledger/peer1.acme.com

#3. Copy the crypto for admin crypto
COPY ./config/crypto-config/peerOrganizations/acme.com/users /var/hyperledger/users

#4. Copy the anchor peer update tx
COPY ./config/acme-peer-update.tx /var/hyperledger/config

#5. Copy the channel create tx file
COPY ./config/airlinechannel.tx  /var/hyperledger/config

#6. Copy the core YAML
COPY ./config/acme/core.yaml /var/hyperledger/config

#7. Copy the bins
COPY ./bins /var/hyperledger/bins

#8. Copy the test chaincode
COPY ./nodechaincode  /var/hyperledger/nodechaincode

#9. Set the working dir
# RUN  echo "cd /var/hyperledger/bins" >> $HOME/.profile
RUN  echo "cd /var/hyperledger/bins" >> $HOME/.bashrc

#10. Set the context for Admin user
RUN echo ". /var/hyperledger/bins/set-context.sh" >> $HOME/.bashrc

#11. Launch the peer
CMD peer node start
