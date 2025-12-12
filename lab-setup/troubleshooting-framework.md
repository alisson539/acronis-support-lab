# Troubleshooting Framework (60-Second Method)

This is the structured troubleshooting approach I will use in interviews and real cases:

1. **Define the problem clearly**
   - Reproduce the issue
   - Confirm expected vs actual behavior

2. **Isolate the layer**
   - Agent
   - OS
   - Network
   - Acronis cloud service
   - Customer environment

3. **Form quick hypotheses**
   - Based on logs, symptoms, and known patterns

4. **Run low-risk tests**
   - Restart services
   - Check connectivity
   - Validate credentials/policies
   - Inspect logs

5. **Collect evidence**
   - Event Viewer / system logs
   - Acronis agent logs
   - HAR files
   - curl / TLS results

6. **Communicate status**
   - Set expectations
   - Provide ETA
   - Update SLA timers

7. **Resolve or escalate**
   - If resolved: verify with customer & document
   - If not: escalate with repro, impact, scope, and artifacts

This framework aligns with Acronis Tier 1 expectations for case intake, triage, communication, and escalation quality.