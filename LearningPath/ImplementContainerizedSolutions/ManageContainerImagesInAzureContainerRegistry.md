# Azure Container Registry (ACR):
- Store and maintain container images and related artifacts.

### Use cases
- ACR supports:
  - `pulling images`: Deploy to Kubernetes, Docker Swarm or azure services like AKS and App Service
  - `pushing images`: Integrating with CI/CD tools like Azure Pipelines or Jenkins
  - `ACR Tasks`: Automate image rebuilding on base image updates, code commits, or multi-step workflows for building, test and patching container images in parallel.

### Service Tiers
1. Basic
   - Cost-effective for learning or low usage
   - Supports all features from standard/premium
   - Limited storage and image throughput
2. Standard
  - More storage and image throughput than Basic
  - Should satisfy most scenario's.
3. Premium
   - Highest storage and concurrent operations
   - offers Geo-replication, content trust and private link for restricted access
   - For high volume usage and advanced needs

### Supported images and artifacts
- When grouped into repositories, each image is a read-only snapshot of a Docker-compatible container.
- Supports Windows and Linux images.
- Stores Docker container images. But can also store other formats like: Helm charts and Open Container Initiative (OCI)-compliant images.


# Storage capabilities
1. `Encryption-at-rest`: 
   - All container images and artifacts in your registry are encrypted at rest. 
   - All images are encrypted before storing. 
   - All images are decrypted on-the-fly when your app/service pull the image
2. `Regional storage`:
   - Data is stored in the region where the registry is created to meet data residency and compliance.
   - In most regions, Azure may store registry data in a paired region
   - Data isn't automatically recovered during a regional outage. Enable geo-replication for multi-region storage and improved performance or resiliency.
3. `Geo-replication (only premium)`
   - Protects against regional failures, ensuring access to your registry.
   - Speeds up pushes and pulls by storing images closer to distributed development and deployment locations.
4. `Zone redundancy (only premium)`:
   - Replicate your registry across 3 AZ in the same region
   - Ensures high availability and resilience within th region
5. `Scalable storage`:
   - Add unlimited repo, images, layers or tags within the storage limit of your registry
   - High numbers of repositories or tags may slow down the registry.
   - Deleted resources cannot be recovered.

# ACR Tasks
- Cloud-based container image building for Linux, Windows and ARM
- On-demand container image builds let you build your app in the cloud instead of doing it on your local machine. Speeds up dev process and make it more efficient
- Automatically build images when source code updates, container base image update or timers.

| OS      | Architecture                     |
|---------|----------------------------------|
| Linux   | AMID64<br/>Arm<br/>Arm64<br/>386 |
| Windows | AMD64                            |

### Task scenarios
Each task uses a source code context (like a Git repository or local files) to build the container image or artifact.
- `Quick task`:
  - Build and push a single container image to a registry in the cloud without needing a local Docker setup.
- `Automatically triggered tasks`: Set triggers to update image when:
  - Source code updates
  - Base image update
  - Schedule
- `Multi-step task`
  - Perform more complex workflows with multiple image builds and containers.
  - YAML

# Explore elements of a Dockerfile
- Instruction script to build Docker image. It typically includes the information:
  - Base/parent image we use to create the new image
  - Commands to update the base OS and install other software
  - Build artifacts
  - Services to expose, such as storage and network configs
  - Command to run when the container is launched

```
# Use the .NET 6 runtime as a base image
FROM mcr.microsoft.com/dotnet/runtime:6.0

# Set the working directory to /app
WORKDIR /app

# Copy the contents of the published app to the container's /app directory
COPY bin/Release/net6.0/publish/ .

# Expose port 80 to the outside world
EXPOSE 80

# Set the command to run when the container starts
CMD ["dotnet", "MyApp.dll"]
```
