**Avito Backend 2022 Account Balance Microservice Project - Python version**

Link to the task - https://github.com/avito-tech/internship_backend_2022

Technology Stack:
- Programming Language: **Python (3.10)**

- Web-framework: **FastAPI**

- ORM: **SQLAlchemy**

- Database: **PostgreSQL**



**Project Description**:

<ins>Information service - Balances/transactions info</ins>
- Provides user with his/her accounts' (both reserve and regular) info (including balance amount)

    Example request:
    >curl -X 'GET' \
      'http://127.0.0.1:8000/v1/information/account-balance/2' \
      -H 'accept: application/json'
    
    Example response body:
    >[
        {
            "user_id": 2,
            "type": "regular",
            "balance": 199.99
         },
        {
            "user_id": 2,
            "type": "reserve",
            "balance": 0
        }
      ]

- Provides user with info on all transactions on his/her accounts (both reserve and regular) - a list of transactions with description on where and why the funds were credited/debited from the account balance is provided. Sorting (by date and amount) and pagination of results are provided as an option

    Example request:
    >curl -X 'GET' \
      'http://127.0.0.1:8000/v1/information/account-transactions/2?page=1&sort_by_amount=false&sort_by_date=false' \
      -H 'accept: application/json'
    
    Example response:
    >curl HTTP /1.1 www.pppp.ru

<ins>Transaction service - Transactions functionality</ins>
- Money is deposited (using 3rd party services) to the user regular account (*for the first time*) - regular account info is added to the 'user_accounts' table with the funds deposited (reserve account info is added to the 'user_accounts' table as well)
*OR*
Money is deposited (using 3rd party services) to the user regular account (*NOT for the first time*) - deposited funds are added to the balance of an existing regular account

    Example request:
    >curl -X 'PATCH' \
      'http://127.0.0.1:8000/v1/transactions/deposit' \
      -H 'accept: application/json' \
      -H 'Content-Type: application/json' \
      -d '{
      "type": "deposit",
      "amount": 199.99,
      "to_user_id": 2
    }'
    
    Example response:
    >curl HTTP /1.1 www.pppp.ru

- Money transfers between users - funds are added to the balance of a to_user and withdrawn from the balance of a from_user

    Example request:
    >curl HTTP /1.1 www.pppp.ru
    
    Example response:
    >curl HTTP /1.1 www.pppp.ru

- Order is placed and money is transferred from user's regular account to the reserve one 

    Example request:
    >curl HTTP /1.1 www.pppp.ru
    
    Example response:
    >curl HTTP /1.1 www.pppp.ru

- Order is cancelled and money is transferred back from user's reserve account to the regular one

    Example request:
    >curl HTTP /1.1 www.pppp.ru
    
    Example response:
    >curl HTTP /1.1 www.pppp.ru

- Order is delivered and money is transferred from user's reserve account to the company account

    Example request:
    >curl HTTP /1.1 www.pppp.ru
    
    Example response:
    >curl HTTP /1.1 www.pppp.ru
    
<ins>Report service - Reports functionality</ins>
- Provides .csv report with total revenues for each service rendered in the requested period. 

    Example request:
    >curl HTTP /1.1 www.pppp.ru
    
    Example response:
    >curl HTTP /1.1 www.pppp.ru


**OpenAPI documentation (with Swagger UI and more detailed description of API)**:
>'/docs'

 
**To run the containers**:
> docker-compose up --build

**To fill the database with test data, use**:
> /scripts/database_populate.sql
