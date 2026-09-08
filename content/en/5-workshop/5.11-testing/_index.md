---
title: "5.11 Testing"
weight: 11
---

## Testing Objective

The complete end-to-end monitoring flow is tested:

**Generate CPU load → CloudWatch receives the metric → Alarm changes to `In alarm` → SNS sends email → CPU decreases → Alarm returns to `OK`.**

## Test Result

| Test Scenario | Expected Result | Actual Result | Evaluation |
|---|---|---|---|
| Generate CPU load | CPU > 70% | CPU reached about 87.2% and could reach higher during the test | Passed |
| Check Alarm | `OK → In alarm` | Alarm changed to `In alarm` | Passed |
| Check SNS | Alert email is sent | Email received with Alarm Details and Reason | Passed |
| Stop CPU load | CPU decreases | CPU returned to normal | Passed |
| Recovery | `In alarm → OK` | Alarm returned to `OK` | Passed |

## Conclusion

The complete monitoring and alerting workflow was successfully verified end to end.
