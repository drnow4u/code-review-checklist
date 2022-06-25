# Code Review Checklist
What should be check during code review

## Check list
- [ ] Function or method precondition
- [ ] Function or method postcondition
- [ ] Object invariants
- [ ] Return value contract


## Return value contract

```java
var vehicle = vehicleService.findEnabledForOrganisation(organisationId)
assert vehicle.enabled()
```

Motivation:
The contract can change for `vehicleService.findEnabledForOrganisation(organisationId)` and the client of API should detect it with e.g. `assert vehicle.enabled()`.

