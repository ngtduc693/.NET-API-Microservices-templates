# .NET API Microservices templates

This is a sample for API Microservices templates that I have diligently researched and designed to help you organize your code clearly

Structure Code Standard for reference:

Solution/

├── Solution items\
├── src -->'Source code'\
│   ├── API --> 'Expose apis for application'\
│   │   ├── (ref: Application-Infrastructure--Persistence-Presentation)\
│   │   └── Folders\
│   │       ├── Abstractions\
│   │       └── DependencyInjection\
│   │           ├── Extensions\
│   │           └── Options\
│   ├── Application --> 'Handler usercase using mediatR library'\
│   │   ├── (ref: Domain) => User Repository interface at domainlayer\
│   │   └── Folders\
│   │       ├── Abstractions\
│   │       ├── Behaviors\
│   │       ├── DependencyInjection\
│   │       │   ├── Extensions\
│   │       │   └── Options\
│   │       └── UserCases\
│   │           ├── V1\
│   │           │   ├── Commands\
│   │           │   │   ├── Account\
│   │           │   │   ├── Identity\
│   │           │   │   ├── Catalog\
│   │           │   │   ├── Communication\
│   │           │   │   ├── Customer\
│   │           │   │   ├── Order\
│   │           │   │   ├── Inventory\
│   │           │   │   └── ...\
│   │           │   └── Queries\
│   │           │       ├── Account\
│   │           │       ├── Identity\
│   │           │       ├── Catalog\
│   │           │       ├── Communication\
│   │           │       ├── Customer\
│   │           │       ├── Order\
│   │           │       ├── Inventory\
│   │           │       └── ...\
│   │           ├── V2\
│   │           └── ...\
│   ├── Domain --> 'Store entity and business logic -> Core application'\
│   │   ├── (ref: None)\
│   │   └── Folders/\
│   │       ├── Abstractions/\
│   │       │   ├── IDomainEvent.cs\
│   │       │   ├── IMessage.cs\
│   │       │   ├── Aggregates/\
│   │       │   │   ├── IAggregateRoot : IEntity\
│   │       │   │   └── abstract class AggregateRoot<TValidator> : Entity<TValidator>, IAggregateRoot\
│   │       │   ├── Entities/\
│   │       │   │   ├── IEntity.cs\
│   │       │   │   └── abstract class Entity<TValidator> : IEntity\
│   │       │   └── Repositories --> Interface\
│   │       ├── Aggregates\
│   │       ├── Entities/\
│   │       │   ├── Profiles\
│   │       │   └── ...\
│   │       ├── Enumerations\
│   │       └── ValueObject/\
│   │           ├── Product(string Description, string Name, string Brand, string Category, string Unit, string Sku)\
│   │           ├── ...\
│   ├── Infrastructure --> 'Integration with external likes Job, email, provider token ...'/\
│   │   ├── (ref: Application-Persistence)\
│   │   └── Folders/\
│   │       ├── Abstractions\
│   │       ├── Authentication\
│   │       ├── BackgroundJobs/\
│   │       │   └── ProcessOutboxMessagesJob.cs\
│   │       ├── DependencyInjection/\
│   │       │   ├── Extensions\
│   │       │   └── Options\
│   │       └── EmailService\
│   ├── Infrastructure.MessageBus --> 'Working with rabbitMQ: Consume Command and Event'/\
│   │   ├── (ref: Application)\
│   │   └── Folders/\
│   │       ├── Abstractions\
│   │       ├── Consumers/\
│   │       │   ├── Commands\
│   │       │   └── Events\
│   │       ├── DependencyInjection/\
│   │       │   ├── Extensions\
│   │       │   └── Options\
│   │       ├── PipeFilters\
│   │       └── PipeObservers\
│   ├── Persistance | Infrastructure.EF --> 'Working with database'/\
│   │   ├── (ref: Domain)\
│   │   └── Folders/\
│   │       ├── Configurations\
│   │       ├── Constants/\
│   │       │   └── TableNames.cs\
│   │       ├── Infrastructure/\
│   │       │   └── PrivateResolver.cs\
│   │       ├── Interceptors/\
│   │       │   ├── ConvertDomainEventsToOutboxMessagesInterceptor.cs\
│   │       │   └── UpdateAuditableEntitiesInterceptor.cs\
│   │       ├── Migrations\
│   │       ├── Outbox/\
│   │       │   └── OutboxMessage.cs\
│   │       ├── Repositories\
│   │       ├── ApplicationDbContext.cs\
│   │       └── UnitOfWork.cs\
│   ├── Infrastructure.XXX (if you have another DB instance)\
│   ├── (ref: Domain)\
│   ├── Folders/\
│   │   ├── Abstractions/\
│   │   ├── DependencyInjection/\
│   │   │   ├── Extensions\
│   │   │   └── Options\
│   │   ├── Idempotence/\
│   │   │   └── IdempotentDomainEventHandler.cs\
│   │   ├── ProjectionDbContext.cs\
│   │   └── ProjectionGateway.cs --> Repository\
│   ├── Presentation  --> 'Define api using apicontroller or minimalapi(recommand but will hard maintanin)' /\
│   │   ├── (ref: Application-Infrastructure)\
│   │   └── Folders/\
│   │       ├── Abstractions/\
│   │       │   ├── ApiController.cs\
│   │       │   └── ApplicationApi.cs\
│   │       ├── Controllers/\
│   │       │   ├── V1\
│   │       │   ├── V2\
│   │       │   └── ...\
│   │       ├── APIs/
│   │       │   ├── Accounts => Asp.Versioning.Builder =>> HasApiVersion\
│   │       │   └── ...\
│   │       └── DependencyInjection/\
│   │           ├── Extensions\
│   │           └── Options\
│   └── Contract --> 'Defined common for project'/\
│       └── Folders/\
│           ├── Abstractions\
│           ├── DataTransferObjects\
│           ├── Enumerations\
│           ├── JsonConverters\
│           ├── Shared/\
│           │   ├── Result.cs\
│           │   └── ResultT.cs\
│           └── Services/\
│               ├── Account/\
│               │   ├── Account.proto\
│               │   ├── Command.cs\
│               │   ├── DomainEvent.cs\
│               │   ├── Projection.cs\
│               │   └── Query.cs\
│               ├── Catalog\
│               ├── Communication\
│               ├── Identity\
│               ├── ...\
└── test --> 'Unit test' /\
    ├── Architecture.Tests\
    ├── API.Tests\
    ├── Application.Tests\
    ├── Domain.Tests\
    ├── Infrastructure.Tests\
    ├── Persistance.Tests\
    └── Presentation.Tests\

─ src: Contains the project's source code, divided into different layers and modules.\
── API: Contains API endpoints to interact with the application.\
── Application: Handles use cases using the MediatR library.\
── Domain: Contains core application entities and business logic.\
── Infrastructure: Integration with external services like Job, email, and token providers.\
── Infrastructure.MessageBus: Works with RabbitMQ, including consuming Commands and Events.\
── Persistence: Works with the database, using Entity Framework.\
── Infrastructure.XXX: Works with multi instance DB.\
── Presentation: Defines APIs using ApiController or MinimalAPI.\
── Contract: Defines common structures for the project, such as DTOs, Enums, JsonConverters, and services.
─ test: Contains unit tests for each part of the system.
