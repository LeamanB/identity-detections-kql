# Identity Sign-in IP Variance with Risk Context (KQL)

KQL hunting query for Microsoft Entra ID `SigninLogs` that surfaces user accounts with IP address churn and preserves identity risk fields for analyst review.

---

## Detection

The query:
- Filters to successful sign-ins
- Groups by user
- Flags accounts with multiple source IPs in a defined window
- Returns risk level/state, apps, locations, and timestamps for investigation

File:
`detections/signin_ip_variance_with_risk.kql`

---

## Validation

Executed in Azure Log Analytics against live `SigninLogs`.

- 34 sign-in events over 30 days
- Multi-country logic returned 0 matches (expected for low-volume tenant)
- Tuned variant returned results by identifying IP variance for a user

---

## Analyst Use

This output is a hunting lead.  
Typical follow-up:
- Check IP reputation / ASN
- Compare device and client app consistency
- Review Entra ID risk state and MFA activity

---

## Tuning

- Time window: `7d`, `14d`, `30d`
- IP threshold: increase for VPN-heavy environments
- Allowlist known egress ranges as needed

---

## Scope

Source: Microsoft Entra ID `SigninLogs`  
Use: SOC / Identity monitoring
