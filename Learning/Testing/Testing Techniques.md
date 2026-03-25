### Testing Pyramid

1. **Unit Testing**: We make unit testing for all the functions and methods in our code base to make our program is running correctly.

	- The number of test cases depends on the testing strategy.
	- All lines in the code should be tried and tested.
		- In case this is very complex or impossible: _The function is doing too much or the logic were written without testability in mind_.
		- Test coverage = Percentage of lines covered by tests.
	- In military or aviation industries, unit testing is also called _Modified Condition Decision Coverage_ (MCDC).
		- In addition to make 100% test coverage, we need to test every single decision as well. -> If we have 3 conditions, we need to write 8 ($2^3$) extra cases to cover all possible scenarios.

2. **Component Testing**: Component testing tests each component of the application in isolation (e.g., Full Stack App -> Front End Component, API Component, Database Component).

	- We should mock out all the components that the current tested component is talking to.
	- _There is two types of coverage scenarios_:
		- _Happy Path_: the component is used as intended, _dependencies respond normally, inputs are valid, and the user flow completes successfully_. You assert the primary outcome and key UI states along the way (e.g., renders expected data, enables the primary action, submits successfully, shows success feedback).
		- _Unhappy Path_: something goes wrong or deviates from the ideal. This includes invalid inputs, missing/empty data, slow or failed network calls, permission/feature flags off, unexpected props, and edge interactions. -> The main idea is to assert that the component fails "well".
	
3. **Integration Tests**: In this tests, we aim to test each integration of our components (e.g., API - Database).

	- Cross component boundaries.
	- Expect real outputs instead of mocked one's.
	- Validate observable behavior between integrations (e.g., HTTP Responses, Databases Transactions, Queued Messages or Events, etc.).
		- _White Box Testing_: If the scope of the integration starts where the business logic begins, is considered a white box test (e.g., Testing to create and persist a user in database directly from the database repository).
		- _Back Box Testing_: If the test do not involve the business logic in the test, we consider this as a black box test. (e.g., Same example but calling the API instead of using the DB Repository).

4. **End to End Testing**: 