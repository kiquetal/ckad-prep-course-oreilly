### Application design and build domain objects

- Container images
 Terminology
 Containerization process
 Docker Engine commands


Container
 Packages an application into a single unit of software including its runtime,environemnt,application binary,dependencies and configuration

Container Runtime Engine
 A software component that can run containers on a host operating system

Container orchestrator
Uses a container runtime engine to instantiate a container
Automates and manages worklosad with features like scalability,networking

Containerfile
SPells out what needs to happen when the software is built in the form of a alist of instructions

Contariner registry
Shares container images in a central location and makes them available for consumption

Container image
Packages an application into a single unit of softare including its runtime
Built from the containerfile


- Jobs and CronJobs
 One-time workload execution
 Scheduled workload execution



- Single and multi-container pods
 Running application workload in k8s
 Namespaces
 Design patterns



- Container Storage

 Ephemeral volumes
 Persistent volumes
