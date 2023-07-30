DeviceInfo
| where SensorHealthState == “Inactive” or SensorHealthState == “Misconfigured”
| summarize max(Timestamp) by DeviceName, SensorHealthState, OnboardingStatus, OSPlatform
| extend LastUpdatedTime = max_Timestamp
| project DeviceName, [‘LastUpdatedTime’],OSPlatform, SensorHealthState, OnboardingStatus
