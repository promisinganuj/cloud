## APP Engine YAML file has “hadlers” and “libraries”
## Two API Management Tools:
### Cloud Endpoints:
- Implements an easy to deploy proxy in front of the application
- It provides an API console to wrap up those capabilities in an easy to manage interface.
- Easy to expose APIs
- Make sure it's only consumed by other trusted developers
- Provides an easy way to monitor and log the API usage
- Provides a single coherent way for the application to know which end user is making the call.

### APPIGEE Edge
- A platform for making APIs available to customers and partners
- Focus on business problems like rate limiting, quotas, and analytics.
- Typically used by providers providing SaaS to other customers
- Contains analytics, monetization and a d developer portal
- Backend services of APPIGEE needn’t be in GCP
- Preferred for Migration Projects (to peel off the application and creating micro services)

## Development in the Cloud:
- Cloud Source Repositories
- Cloud Functions
### Deployment Manager
- Provides repeatable deployments
- Create a .yaml template desctibing your environment and use DM to create resources

## Stackdriver
### Monitoring
- Platform, system and application metrics
- Uptime/health checks
- Dashboard and Alerts
### Logging
- Platforml, system and application logs
- Log search, view, filter and export
- Log-based metrics
### Debug
- Debug Application
### Error Reporting
- Error Notification
- Error dashboard
### Trace
- Latency reporting
- Per-URL latency
