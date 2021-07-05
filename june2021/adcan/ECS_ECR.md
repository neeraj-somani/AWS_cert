# ECS_ECR
- Elastic Container Service and Registry

### Containers
- Solves problems of Virtualization
- So what is virtualization?
  - Ideally, it should be called as OS virtualization.
  - Its a process of running multiple Operating system on same physical hardware.
  - These multiple OS is almost identical and consume a lot of machine resources in creating virtual environment and not supporting application tasks.
  - This problem is solved by containers.
- Container Engine (Docker)
  - A continer conceptually very similar to VM, but with a small twick.
  - a container runs as a process within the host OS. Hence, opposite of vitualization which runs multiple OS on top of host OS and hypervisor.
  - A container process inside container engine can utilized the host OS capability to deal with networking and file I/O.
  - This container would run a single process within that OS, potentially one of many but inside that process its like an isolated OS. It has its own file system, it can run child processes inside it, etc... 
  - Example, a container could run a web-server, or an application server, and do so in a completely isolated way.
  - In this way it consumes very limited memory and computation from host, that is used for application annd any runtime environment elements, example libraries and dependencies. 
  - This is one of the most imp benefit of containers, that we can run multiple applications on a single piece of hardware.

### Docker Images (Container images)
- its made of multiple independent layers.
- its created by using a docker file.
- Each line creates file system layer inside docker image.
- images are created from a base image or scratch.
- images contain readonly layers, changes are layered onto the image using a differential architecture.
- A docker image is how we create a docker container. 

### Docker Containers
- Its just a running copy of a docker image, with one difference, it also has one read-write file system layer.
- This read/write layer allows containers to run, example, if log file are generated or if application generates or reads data, all that gets stored in read/write layer of container.
- Remember, each layer is differential and it stores only the changes made against it versus the layer below.

### Container Registry
- its a registry or hub of container images.

### Refresher notes
- Dockerfiles are used to build images
- Portable - self-contained, always run as expected
- lightweight - parent OS used, fs layers are shared
- container only runs the application & environment it needs
- provides much of the isolation VM's do
- ports are 'exposed' to the host and behond...
- Application stacks can be multi-container...


### Elastic Container Service (ECS)
- Its a product which allows users to use the containers running on infrastructure, which AWS fully manage or partially manage. 
- Users get benefit of managed container hosts. Reduce admin overhead.
- ECS is to containers what EC2 is to virtual machines.
- ECS users, clusters, which run in one of two modes, 
  - EC2 mode and Fargate mode.
- EC2 mode 
  - This uses EC2 mode as container hosts. They are just normal EC2 hosts running the ECS software.
  - With EC2 mode you pay for the EC2 instances regardless of container usage
- Fargate Mode
  - Its a serverless way of running docker containers, in which AWS manages the container host part.
  - you just need to define an architect to your env using containers.
  - Fargate mode uses shared AWS infrastructure and ENI's which are injected into your VPC
  - You pay only for container resources used while they are running.
- ECS takes instructions and orchestrates where and how to run those containers. 
- ECS allows you to create clusters
- ECR (Elastic Container Registry)
  - it just container image registry/repository. 
  - Very similar to docker hub.
- Few things that we mention in **container definition**
  - example, which port container image is running on host
  - task definition
    - a task in ECS is self-contained application. A task could have one container defined inside it or many.
    - A simple application can use a single container but you can build complex application by using multiple containers in a task. example, web application container and a database container.
    - it stores the resources used by task, CPU, memory, networking mode that task uses, they store the compatibility mode.
    - **exam ques 100%** other most imp thing that it contains, is task role, its an IAM role that a task assume, to gain temp credentials to interact with AWS resources.
    - A task in itself is not highly available and highly scalable. 
    - Hence in-order to scale the task, AWS provides Service definition.
  - Some other things that container definition stores:-
    - like a pointer to where the container is stored, what port is exposed. The rest is defined in task definition.
  - Service definition
    - this defines how the application (task) scaling should work.
    - how many copies of task needs to be run. 
- Now these task services gets deployed to ECS cluster.

### Summary
- Container definition - image & port
- Task definition - Security (task role), container(s), resources
- Task Role - IAM Role which the TASK assumes
- service - how many copies, HA, Restarts

### Some links
- https://docs.aws.amazon.com/AmazonECS/latest/APIReference/API_ContainerDefinition.html
- https://docs.aws.amazon.com/AmazonECS/latest/APIReference/API_TaskDefinition.html
- https://docs.aws.amazon.com/AmazonECS/latest/developerguide/cluster-capacity-providers.html

### ECS Cluster Types
- EC2 vs ECS(EC2) vs Fargate
  - If you use containers ... use ECS
  - Large workload.... price conscious -- use EC2
  - Large Workload .... overhead concious - use Fargate
  - small / burst workloads -- use fargate
  - Batch / Periodic workloads -- use Fargate
