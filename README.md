# Service Name

## Oncall Runbook

## ERP connection setup

Follow below steps to create new erp connection and share erp isntance id : 

* Get the organization Id
  * Obtain the workspace ID for the customer.
  * Use this workspace ID to retrieve the organization ID using the provided curl command:

curl --location 'https://businesshierarchy-prod-http.internal.cleartax.co/api/businessHierarchy?nodeType=WORKSPACE&getSubtree=true&getOrganisationPath=true&nodeId=your_workspace_id' \
     --header 'Content-type: application/json'

* Create Demo Workspace Configs
  * Use the prescribed API endpoint to create and configure the ERP connection:
    * Create ERP Connection: POST /internal/erp_connection
    * Configure ERP Query Settings (this may require details from the config table or platform documentation)
    * Set up Time Table Management State as needed for the integration.
    * Once setup is complete, share the generated ERP instance ID with the requester.
  * Optionally, you can use the Retool feature to create the ERP connection.

* Migrate from Demo to Production (for Existing Users)
  * Generate a config snapshot in the Demo workspace using:

curl -X GET "https://your-api-domain.com/internal/erp_connection/generateConfigSnapshot" \
  -H "x-erp-instance-id: your-demo-erp-instance-id" \
  -H "x-workspace-id: your-demo-workspace-id"

  * Import this config snapshot into Production using:

curl -X POST "https://your-api-domain.com/internal/erp_connection/importConfigSnapshot" \
  -H "x-erp-instance-id: your-prod-erp-instance-id" \
  -H "x-workspace-id: your-prod-workspace-id" \
  -H "Content-Type: application/json" \
  -d '@path-to-config-snapshot-file.json'

  * Enable the required artifact and set the project name.

## Service Down
1. Check service health: `curl https://api.service.com/health`
2. Check logs: `kubectl logs -f deployment/service-name`
3. Restart if needed: `kubectl rollout restart deployment/service-name`
4. Verify recovery: Monitor dashboards for 5 minutes

## High Memory Usage  
1. Check memory metrics in Grafana dashboard
2. Identify memory leaks: `kubectl top pods`
3. If > 80% usage, restart: `kubectl rollout restart deployment/service-name`
4. Check for recent deployments that might cause issues

## Database Connection Issues
1. Test DB connectivity: `nc -zv db-host 5432`
2. Check connection pool: Look for connection timeouts in logs
3. Restart application if connections exhausted
4. Scale up DB connections if needed

## Related Dashboards
- [Service Health](https://grafana.com/service-health)
- [Error Rates](https://grafana.com/errors)
