# Code Review Checklist
What should be check during code review

## Check list

You can copy below checklist to your review in GitLab.

```
- [ ] All business requirements described in ticket are implemented
- [ ] A non-breaking change
- [ ] Function or method precondition
- [ ] Function or method postcondition
- [ ] Code coverage
- [ ] Tests' assertions sabotage
- [ ] Object invariants
- [ ] [Return value contract](https://github.com/MarcinNowak-codes/code-review-checklist/blob/main/README.md#return-value-contract)
- [ ] Test case: happy and unhappy path
- [ ] [Endpoint test case](https://github.com/MarcinNowak-codes/code-review-checklist/blob/main/README.md#endpoint-test-case)
- [ ] Code should not contains any secret, key or certificate, details https://owasp.org/www-project-wrongsecrets/
- [ ] Parametrised tests
- [ ] DB Transaction boundary
- [ ] DB index
- [ ] Thread Safety
- [ ] Is delete of objects (Garbage Collector) or entity in DB handled correctly?
- [ ] Endpoints versioning
- [ ] Value Object for e.g. UserId (wrapper class)
- [ ] Is WireMock used to simulate communication to external services over HTTP?
- [ ] Is TestConteiner used to simulate database?
- [ ] Unnessesry thread creation e.g. in Spring Boot controller is creating async task and doing nothing when waiting for task complition. 
- [ ] Thread deadlock e.g. async task1 is creating async task2 and for complition. Both task are assigned to same thread pool and there is no free thread.
- [ ] Abuse of `var` e.g. `var response = service.gettings()`
- [ ] Deserialization with fallback. When consuming data from other service via HTTP, Kafka, JMS etc. always try to deserialize as stricly as possible (e.g. FAIL_ON_UNKNOWN_PROPERTIES for ObjectMapper). If it fails log error message and try again deserialize with relaxed rules. You don't want to be wake up at 2 in night becouse someone add new field.

Details can be found [Code Review Checklist](https://github.com/MarcinNowak-codes/code-review-checklist/blob/main/README.md)
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

## DB Transaction boundary ##

- Is transactoin required?
- Is message in message queue not consumed when transaction is rolled back?

## Thread Safetly ##

- Are used class in fields thread safe?
- Is critical section necessary?


## Endpoint test case

- happy
- unhappy path
- security (authorisation, Content Security Policy, etc.)
- information disclosure of client A to client B or unauthenticated attacker in multi tanent application
