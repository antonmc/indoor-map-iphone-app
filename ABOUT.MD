Kubecoin Booth Primer
---------------------

#### Motivation

Kubecoin is an experiment to poke at capturing personal (health) information in a private, respectful, secure and trustworthy way.

It was also created as a fun, and interesting way to put IBM Cloud technology in the hands and pockets of developers, among other things it uses the following IBM Technology:

- IBM Cloud Container Service
- IBM Cloud Functions
- IBM Blockchain
- IBM Mongo Database by Compose
- IBM Cloud Foundry
- IBM MQTT Service

The backend is written in Node.JS, the iOS app in Swift 4 and the Android app in Java.

It was developed by Anthony Amanse, Ishan Gulhane, Hovig Ohannessian, Raheel Zubairy

Here's a high level overview of the technology:

![kubecoin screens](https://raw.githubusercontent.com/antonmc/kubecoin/master/design/architecture.png)

## Runtime flow

1. Kubecoin Mobile App uses HealthKit (iOS) or Google Fit (android) to get the users' step count.
2. The step count is then sent to the Blockchain network on Kubernetes and in return, the user will be rewarded with "Kubecoins" by the blockchain network. The chaincode is the logic behind the blockchain network.
3. The node servers on Kubernetes is an interface between the MongoDB and the mobile app. This allows us to get the state of the users without having to query the blockchain network which could take longer.
4. The dashboard uses a Cloud Foundry to host its front-end and get data from the MongoDB.

Here's a deeper architecture dive of the **Android/Kubernetes** integration:
https://github.com/IBM/android-kubernetes-blockchain/blob/master/README.md


##### iPhone App on iTunes
developed by Anton McConville & Anthony Amanse

https://itunes.apple.com/us/app/kubecoin/id1369165644?mt=8

##### Android App on Google Play
developed by Anthony Amanse

https://play.google.com/store/apps/details?id=com.amanse.anthony.fitcoinandroid&hl=en

##### Kubecoin Dashboard:
https://kubecoin.mybluemix.net/

We want to show this on a display as much as possible.

##### Kubecoin Shop dashboard
to complete transactions (enter contract id and complete):
https://kubecoin-shop.mybluemix.net/shop

We want to keep this to ourselves to show a participant when they cash in.

##### FAQ

1. How does the steps get converted into Kubecoins?
    * The steps are sent to the Blockchain network. The chaincode is the logic behind the functions of the blockchain. We configured it to reward users 1 Kubecoin for every 100 steps.

2. Why choose Kubernetes for production?
    * Kubernetes does provide scalability and resiliency. But working with different services, it would be easier to use a container orchestration tool to easily manage this services without redeploying everything.
    * The hyperledger fabric was designed to work in dockers but we chose to have it in Kubernetes compared to running it in a virtual server. This also makes them easier to manage with one platform. To provide resiliency with the blockchain network (its ledger/transactions and state database), they are using NFS volumes as its storage.
3. What does the Cloud Function do?
    * The cloud function generates the random avatar and name that is assigned to a user of the app. It made sense to make this a serverless function since it would only be needed at user registration. This also makes it easier to change our set of avatars and name it generates.
4. What's inside the IBM Cloud Container Service (Kubernetes)?
    * https://github.com/IBM/android-kubernetes-blockchain/blob/master/README.md
