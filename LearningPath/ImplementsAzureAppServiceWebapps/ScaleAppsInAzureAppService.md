# Autoscaling:
- Adjust available resources based on current demand.
- Triggered by a schedule or when resource is low e.g. CPU usage grows / memory occupancy increase / more incoming requests.

Scale out options:
1. `Azure autoscale`
- Use rules. for example: 
  - Add another web server if CPU > 70% for 10 min. 
  - Remove if CPU < 40% for 15 min.
- Autoscaling doesn't have any effect on the CPU power, memory, or storage. It only changes the number of web servers / instances.
- Improves elasticity (for example increased/reduced activity during holidays)
- Improves availability and fault tolerance

2. `Azure App Service automatic scaling`
- No need to manually create rules. Azure does it.

# Autoscale factors
1. Scale based on `metrics` (number of http requests, disk queue length)
2. Scale based on `schedule` (Every day at 8 - 10 am)
- Metrics for autoscale rules for web app:
  - CPU %
  - Memory %
  - Disk Queue Length
  - Http Queue Length
  - Data in (number of bytes received)
  - Data out (number of bytes sent)

# Autoscale actions
- example: scale-out (add) / scale-in (remove) instance if CPU % reach a threshold
- It uses operators:
  - Greater than
  - Less than
  - Equal to
- Cooldown period