# Service Name

## Oncall Runbook

## Erp connection
1. Get the organization Id
  * Requestor will share the workspaceID in the request.
  * Use this workspaceID to retrieve the organizationID using the below API:
```
curl --location 'https://businesshierarchy-prod-http.internal.cleartax.co/api/businessHierarchy?nodeType=WORKSPACE&getSubtree=true&getOrganisationPath=true&nodeId={workspaceID}' \
--header 'Content-type: application/json'
```
2. Share the organizationId obtained from the response above.

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
