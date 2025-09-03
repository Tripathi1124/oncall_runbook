# Service Name

## Oncall Runbook

### Troubleshooting Common Issues

#### Service Down
1. Check service health: `curl https://api.service.com/health`
2. Check logs: `kubectl logs -f deployment/service-name`
3. Restart if needed: `kubectl rollout restart deployment/service-name`
4. Verify recovery: Monitor dashboards for 5 minutes

#### High Memory Usage  
1. Check memory metrics in Grafana dashboard
2. Identify memory leaks: `kubectl top pods`
3. If > 80% usage, restart: `kubectl rollout restart deployment/service-name`
4. Check for recent deployments that might cause issues

#### Database Connection Issues
1. Test DB connectivity: `nc -zv db-host 5432`
2. Check connection pool: Look for connection timeouts in logs
3. Restart application if connections exhausted
4. Scale up DB connections if needed

### Emergency Contacts
- Primary: @john-doe (Slack: @johndoe)  
- Secondary: @jane-smith (Slack: @janesmith)

### Related Dashboards
- [Service Health](https://grafana.com/service-health)
- [Error Rates](https://grafana.com/errors)