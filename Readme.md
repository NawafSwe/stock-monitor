# Investor built-in project: This project is built-in for the investor to set threshold for stock prices and get notified when the stock price is above the threshold.

# Tech stack used in the project:
- Python
- FastAPI
- Cockroachdb
- RabbitMQ
-  Celery and Celery-Beat to schedule tasks

# How to run the project:
- Clone the project
- Install docker and docker-compose
- Run the following command to start the project:
``` make up ``` to install and run the docker images for the project which includes the following:
  - Cockroachdb
  - RabbitMQ
  - 
- Create your own python environment:
  - ``python3 -m venv venv``
- Activate python environment:
  - ``source venv/bin/activate``

- Run the following command to start the celery and beat:
  - ``celery -A api.main.celery_app beat``
- Run the following command to start the fastAPI server:
  - ``uvicorn api.main:app --host 0.0.0.0 --port 8000``

- Once you start the project, there will be already defined alert rules for the investor. You can check the rules by going to the following url:
  - http://localhost:8000/alert-rules
- Export the postman collection from this project to try out the other endpoints.

# Architectural patterns used in the project:
  - Followed the DDD pattern to structure the project, applying value-objects, entities,repositories, and events.
  - Layered architecture, by separating routing logic from business logic and data access logic.
  - Applying Asynchronous communication pattern between services using RabbitMQ and Celery.
  - Messaging concepts, segregating commands and events, and using the event-driven architecture to communicate between services.

# Decisions and tradeoffs:
- Creating repository to handle the data access logic, which makes it easier to change the data source in the future, instead of creating pure function to handle the work.
- Abstracting classes to make it easier to change the implementation in the future, by following DPI principle, which we let services/functions depends on the higher level not the lower level of implementation details.
