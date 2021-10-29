# Popug-jira architecture :parrot:

## Table of content

* [Event Storming](#event-storming)
* [Data model](#data-model)
* [Domain model](#domain-model)
* [Communication in the system](#communication-in-the-system)
  
## Event Storming

1. **Login**
    - Actor - Account
    - Command - Login to app
    - Data - ???
    - Event - Account.Logined
2. **Create Task**
    - Actor - Account
    - Command - Create Task
    - Data - Task + Account id
    - Event - Task.Created
3. **Assign Task**
    - Actor - Account (Admin / Manager)
    - Command - Assign task
    - Data - Task + Account id
    - Event - Task.StatusChanged
4. **Complete Task**
    - Actor - Account
    - Command - Complete task
    - Data - Task + Account id
    - Event - Task.StatusChanged
5. **Accrual / Withdrawal money**
    - Actor - Task.StatusChanged / Task.Created
    - Command - Accrual / Withdraw money
    - Data - Task + Account id
    - Event - Balance.Updated
6. **Calculate daily income**
    - Actor - Cron
    - Command - Calculate income
    - Data - Balance + Account id
    - Event - Balance.Reset
7. **Create audit**
    - Actor - Balance.Updated / Balance.Reset
    - Command - Create audit
    - Data - Balance + Account id
    - Event - ???
8. **Send email**
    - Actor - Balance.Reset
    - Command - Send email
    - Data - Balance + Account id
    - Event - ???


- Account, Account role, Account auth
- Task, Task status
- Balance, Balance audit

## Data model
![Data model](https://i.ibb.co/sqkWHsq/data-model.png)

## Domain model
![Data model](https://i.ibb.co/VSxzXBS/domain-model.png)

## Communication in the system
![Data model](https://i.ibb.co/gR3xJBK/communication-in-the-system.png)

- **Sync**:
  - BC for auth service
  - BC for task service
  - Authorization process

- **Async**:
  - CUD-events for accounts
  - BE for creating task
  - BE for changing status
  - BC for calculation balance of employee
  - BE for reset balance
  - BC for audit
  - BC for email
  
**CUD event data**
  - Account id
  - Account role
  - Account email