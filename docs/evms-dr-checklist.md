# EVMS Disaster Recovery Checklist

Practical checklist for **RPO/RTO planning and failover drills** on an electronic voucher management / EVD platform.

## 1. Targets to publish

| Domain | RPO target (fill in) | RTO target (fill in) | Freeze rule if lag exceeded |
|--------|----------------------|----------------------|-----------------------------|
| PIN store | | | Freeze issue |
| Inventory ledger | | | Freeze issue; optional redeem-only |
| Float / credit | | | Pause credit changes |
| Customer read APIs | | | Stale-OK vs fail-closed |

## 2. Technical prerequisites

- [ ] Encrypted cross-region replica or equivalent standby
- [ ] Point-in-time recovery backups tested quarterly
- [ ] Lag metrics visible to on-call (seconds behind primary)
- [ ] Automated health checks with human approve on promote (unless agreed auto)
- [ ] Channel clients idempotent across failover
- [ ] Secrets / KMS keys available in standby region

## 3. Failover runbook steps

- [ ] Declare incident and notify partners if SLA requires
- [ ] Read replication lag / last applied LSN or equivalent
- [ ] If lag > RPO: enter degraded mode (document which APIs stay up)
- [ ] Promote standby; shift traffic
- [ ] Run checksums: serial counts, last sell IDs, float totals
- [ ] Open redeem, then issue, then credit APIs in order
- [ ] Post-incident: reconcile exceptions, write timeline

## 4. Drill cadence

- Tabletop quarterly; technical failover at least annually (or per policy)
- Measure actual RTO; update runbooks when steps drift
- Include finance and security observers when PIN store is involved

## Related

See the main [README](../README.md). Product context: [voucher reconciliation and PIN security](https://evdsystem.com/evd-software/voucher-reconciliation-pin-security-evms/).
