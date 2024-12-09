# API Sample Test

## Getting Started

This project requires a newer version of Node. Don't forget to install the NPM packages afterwards.

You should change the name of the ```.env.example``` file to ```.env```.

Run ```node app.js``` to get things started. Hopefully the project should start without any errors.

## Explanations

The actual task will be explained separately.

This is a very simple project that pulls data from HubSpot's CRM API. It pulls and processes company and contact data from HubSpot but does not insert it into the database.

In HubSpot, contacts can be part of companies. HubSpot calls this relationship an association. That is, a contact has an association with a company. We make a separate call when processing contacts to fetch this association data.

The Domain model is a record signifying a HockeyStack customer. You shouldn't worry about the actual implementation of it. The only important property is the ```hubspot```object in ```integrations```. This is how we know which HubSpot instance to connect to.

The implementation of the server and the ```server.js``` is not important for this project.

Every data source in this project was created for test purposes. If any request takes more than 5 seconds to execute, there is something wrong with the implementation.

## Improvements

I already make some improvements in this project, creating some reusable functions, but we can improve more, following the guidelines below:

Code Quality and Readability: Adopting TypeScript is a priority to enforce static typing, improving maintainability and reducing runtime errors. Structuring reusable HubSpot-related logic into a dedicated service file, such as HubSpotService, would separate concerns and centralize API interactions. Adding comprehensive comments and adhering to consistent formatting (Prettier or ESLint) would enhance readability. Including JSDoc comments for functions and parameters can further improve developer experience.

Project Architecture: Following a modular structure by separating core functionalities into distinct layers (service, controller, utilities) will make the codebase more scalable. Implementing dependency injection for services (Inversify.js) can improve testability and decouple dependencies. Using a configuration management library, like dotenv or config, ensures sensitive API credentials and constants are centralized and secure.

Code Performance: Optimizing performance is crucial when dealing with multiple API calls. Implementing queues (Async, Bull) for each entity ensures asynchronous processing, reducing response time for the primary task. Instead of making API calls sequentially, batch API calls where supported or use parallel requests with proper rate limiting to handle large datasets efficiently. Additionally, we can search first in the database some collected data such as contact details, also caching frequently accessed data, using Redis or in-memory storage like Node.js Map, can minimize redundant calls.

Error Handling: Introduce a standardized error-handling mechanism to gracefully handle edge cases, like missing or invalid contactId. Implement retries with exponential backoff for transient errors to ensure resilience.

Testing: Add unit and integration tests to validate key functionalities, such as association retrieval and contact lookup. Tools like Jest and a mocked HubSpot API would help ensure robust test coverage without hitting live APIs.

By implementing these strategies, the project would achieve better maintainability, scalability, and performance, ensuring a smoother development experience and improved user satisfaction.

