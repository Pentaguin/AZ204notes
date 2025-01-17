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
