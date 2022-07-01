# Code Review Checklist
What should be check during code review

## Check list

You can copy below checklist to your review in GitHub and GitLab.

```
- [ ] All business requirements described in ticket are implemented
- [ ] Function or method precondition
- [ ] Function or method postcondition
- [ ] Code coverage
- [ ] Tests' assertions sabotage
- [ ] Object invariants
- [ ] Return value contract
- [ ] Test case: happy and unhappy path
- [ ] Endpoint test case: happy and unhappy path, security (authorization, Content Security Policy, etc.)
- [ ] Code should not contains any secret, key or certificate, details https://owasp.org/www-project-wrongsecrets/
- [ ] Parametrized tests
```

## Object invariants

* Java - constraints
* SQL - `NOT NULL`, `CONSTRAINT CHECK`

## Return value contract

```java
var vehicle = vehicleService.findEnabledForOrganisation(organisationId)
assert vehicle.enabled()
```

Motivation:
The contract can change for `vehicleService.findEnabledForOrganisation(organisationId)` and the client of API should detect it with e.g. `assert vehicle.enabled()`.


## Parametrized tests

During development new tests are added to cover all edgecase. It can happen that 2 or more tests are differ only with value of parameter. In such situation common code should be extracted and parameter in test should be used with e.g. `@ParameterizedTest` in Junit 


