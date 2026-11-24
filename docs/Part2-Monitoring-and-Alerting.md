# Part 2: Threat Monitoring & Detection

## Log Analytics Workspace
- Name: `nova-fintech-law`
- Region: East US 2
- VM connected and sending data

## VM Insights
Enabled for the production VM. Performance and dependency data flowing.

## Public IP Diagnostic Settings
- Resource: Public IP of the web VM
- Destination: Log Analytics workspace
- Logs + Metrics enabled

## Alert Rule
- **Signal:** Percentage CPU
- **Condition:** Greater than 80%
- **Duration:** 5 minutes
- **Severity:** Sev 2
- **Action Group:** Email notification

## Evidence Required
- Log Analytics workspace overview
- VM Insights connected status
- Public IP diagnostic settings
- Alert rule configuration
- Action group email recipient
- Fired alert or email notification

## Screenshot Naming
```
part2_log_analytics_workspace.png
part2_vm_insights.png
part2_publicip_diagnostics.png
part2_alert_rule.png
part2_action_group.png
part2_alert_fired.png
```
