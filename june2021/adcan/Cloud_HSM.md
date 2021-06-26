# CloudHSM
- an AWS provided Hardware Security Module product.
- CloudHSM is required to achieve compliance with certain security standards such as FIPS 140-2 Level 3.
- https://en.wikipedia.org/wiki/FIPS_140-2
- This is a product similar to KMS
- because it also creates, manages, secures cryptographic materials or keys.
- Few key differences between HSM vs KMS
- KMS
  - With KMS .. AWS manages .. used mostly for encryption with-in AWS and integrates easily with other AWS products.
  - but it has one limitation, that is its a shared service, 
  - meaning, your part of KMS is isolated but under the hood, other accounts within AWS also use the same service
  - Although, account owner has full permission on KMS but AWS also has certain level of access to KMS, which could be concerning for few enterprises
  - because AWS manage the hardware and software of the KMS systems
  - Even behind the scene KMS also use HSM
  - KMS is overall FIPS 140-2 Level 2 compliant, and some level 3 complaint.
  - Another difference is how you access the product, all operations are performed with AWS standard APIs, and all permissions are controlled using AWS IAM permissions
  - Recently KMS updated, and now KMS can use CloudHSM as a custom key store, hence, intergartion between CloudHSM and KMS gives more robust functionalities
- HSM
  - these are industry standard pieces of hardware, which are designed to manage keys and perform cryptographic operations
  - cloudHSM can actually run your own HSM on-premises.
  - cloudHSM is a True "Single Tenant" HSM provided by AWS
  - AWS provisioned it and they are responsible for hardware maintainance
  - but AWS has no access to the part of the unit, wheather keys are stored and managed,
  - customer is fully responsible for its management
  - its actually physically temper resistant piece of hardware 
  - Generally, if a customer loose HSM, there is no way to recover that data. Only customer can do that.
  - CloudHSM is fully FIPS 140-2 Level 3 - compliant, hence its considered more secure and independent than KMS.
  - but in case of CloudHSM, its not so tightly integrated with AWS, you can access CloudHSM using industry standard APIs
    - example, PKCS#11, Java Cryptography Extensions (JCE), Microsoft cryptoNG (CNG) libraries.


### Some additional points
- Generally or Idealy, CloudHSM is not installed inside a VPC that you have any control
- They are idealy deployed in AWS managed cloudHSM VPC, that account owner has no visibility of
- by default its not highly available service, and hence a cluster needs to be configured to make it highly available and robust service
- Once HSM cluster has been configured, they keeps keys and policies in sync when nodes are added or removed
- Usually, you access them using elastic network interfaces.
- An AWS CloudHSM client (agent) needs to be installed on EC2 instance, in-order to access these AWS provided HSM.
- once this client is installed, industry standard APIs (PKCS#11, JCE, CNG) can be used to access them.
- While AWS provision HSM but they don't have access to secure area where key material is held. only customer manage them

### CloudHSM Use cases / scenarios - where to use them and there limitations
- There is no native integration between CloudHSM and Any AWS products/services. example, no S3 SSE
- Although, CloudHSM can used to perform client side encryption, and hence S3 CSE is possible.
- offload the SSL/TLS processing for web servers to cloudHSM
- CloudHSM can also be beneficial or easily utilized with other products like Oracle Databases that support / enable Transport Data Encryption (TDE)
- protect the private keys for an Issuing Certificate Authority (CA)
