The provided `git diff` records show several changes across multiple files, including Docker configuration, SQL scripts, Java code, and dependency management files. Here's a review of the changes:

**Docker Configuration:**

* **docker-compose-environment.yml:** A new service for RabbitMQ has been added with the following details:
    * Image: `rabbitmq:3.12.9`
    * Container name: `rabbitmq`
    * Ports: `5672` and `15672` exposed
    * Environment variables for default user and password set to `admin`
    * Command: `rabbitmq-server`
    * Volume: Mounts a local directory for enabled plugins

**SQL Scripts:**

* **promotion-lottery.sql:** The `state` of the `raffle_activity` table has been changed from `'create'` to `'open'`.
* **promotion-lottery_01.sql:** The `stock_count` for `raffle_activity_sku` has been increased from `0` to `20`. The `stock_count_surplus` remains `0`.
* **promotion-lottery_01.sql:** A new entry has been added to the `raffle_activity_account` table with increased counts.
* **promotion-lottery_01.sql:** Multiple new entries have been added to the `raffle_activity_order_001` table, indicating multiple orders.

**Java Code:**

* **pom.xml and promotion-lottery-app/pom.xml:** A new dependency for Spring Boot Starter AMQP has been added, indicating the integration of RabbitMQ messaging.
* **application-dev.yml:** Configuration for RabbitMQ has been added, including connection details and a topic configuration for `activity_sku_stock_zero`.
* **raffle_activity_sku_mapper.xml:** New update statements have been added to update and clear the stock count for a SKU.
* **RaffleOrderTest.java:** The test class now includes setup for activity assembly and a new test case for consuming stock and ensuring database consistency.
* **IActivityRepository.java:** New methods have been added for caching and updating SKU stock count, handling RabbitMQ messages, and clearing queues.
* **ActivitySkuStockZeroMessageEvent.java:** A new event class for handling SKU stock zero messages.
* **ActivitySkuStockKeyVO.java:** A new value object class for representing SKU stock keys.
* **AbstractRaffleActivity.java:** The abstract class now includes additional checks for activity state and date validity.
* **ISkuStock.java:** A new interface for handling SKU stock operations.
* **RaffleActivityService.java:** The service class now implements the `ISkuStock` interface and includes the necessary methods.
* **ActivityArmory.java:** A new class for pre-heating activity SKU data.
* **IActivityArmory.java and IActivityDispatch.java:** New interfaces for activity pre-heating and stock subtraction.
* **ActivityBaseActionChain.java:** The base action chain now includes checks for activity state, date validity, and SKU stock.
* **ActivitySkuStockActionChain.java:** The SKU stock action chain now includes logic for subtracting stock and sending messages.
* **ActivityRepository.java:** The repository class now includes the necessary methods for caching, updating, and clearing SKU stock count, as well as handling RabbitMQ messages.
* **EventPublisher.java:** A new class for publishing messages to RabbitMQ.
* **IRedisService.java:** The Redis service interface now includes a new method for setting a key with an expiration time.
* **RedissonService.java:** The Redisson service class now implements the new method for setting a key with an expiration time.
* **UpdateActivitySkuStockJob.java:** A new scheduled job for updating SKU stock count based on delayed queue messages.
* **ActivitySkuStockZeroCustomer.java:** A new RabbitMQ message consumer for handling SKU stock zero messages.

**General Observations:**

* The project is integrating RabbitMQ for messaging and asynchronous processing.
* There is a focus on ensuring data consistency and handling edge cases, such as stock depletion and activity state validation.
* The codebase is well-structured with clear interfaces and separation of concerns.
* The use of value objects and domain-driven design principles is evident.

**Suggestions:**

* Consider using a more secure password for the RabbitMQ user.
* Ensure that the RabbitMQ management plugin is properly configured and secured.
* Add error handling and retry logic for RabbitMQ message publishing and consumption.
* Consider using a more robust solution for distributed locks, such as Redlock.
* Add unit tests for the new methods and classes.
* Document the new features and changes.

**Overall, the changes appear to be well-thought-out and implemented. The integration of RabbitMQ and the focus on data consistency and validation are positive steps for the project.**