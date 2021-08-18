# Neighbour Stalker
## Stalk Your Neighbours (For Fun And Profit!)

## Contents:
1. Overview and Startup
2. Relational Schema
3. HTTP Pathways
4. Example Requests
5. Additional API Rules

## Overview: 
A neighbourhood collaboration/stalking to keep track of people, houses, and addresses of houses in the community!

### Who will use it? 
Nosy neighbours, I guess?

### What will users be able to do?
- Look up a house, it’s address, and owner
- Look up people in neighbourhood within certain age brackets and with specific household sizes

## Startup:
Startup guide pending creation of API

## Relational Schema: 
### Person at Household: 
| Field | Data Type | Description |
| :--- | :--- | :--- |
| FirstName | char(30) | Person's first name |
| LastName | char(30) | Person's Last Name |
| Age | int(0-120) | Person's Age |
| DoB | date | Person's Date of Birth |
| HouseID | integer | The Unique Property Reference Number (UPRN) |
| PersonID | integer | The Perons Unique Id Number in the Database |

### House Data: 
| Field | Data Type | Description |
| :--- |:--- | :--- |
| Owner | char(60) | Owner's Full Name |
| Address | text | Street Address |
| Postcode | char | House Postcode |
| HouseID | integer | The Unique Property Reference Number (UPRN) |
| OccupantNo | int.(0-20) | Number of Occupants at Property |

### SQL DB Example: 
| FirstName | LastName | Age | DoB | HouseID | PersonID |
| :--- | :--- | :--- | :--- | :--- | :--- |
| John | Johnson | 21 | 1/1/2000 | 1 | 1 |
| Joe | Johnson | 27 | 1/1/1994 | 1 | 2 |

| Owner | Address | Postcode | HouseID | OccupantNo. |
| :--- |:--- |:--- | :--- | :--- | 
| John Johnson | 123 Fake Street | AB1 2CD | 1 | 2 |

## HTTP Pathways:
```
GET /houses 
GET /houses/:id 
GET /houses/:id/occupants
POST /houses
PATCH /houses/:id
DELETE /houses/:id
GET /people
POST /people
PATCH /people/:id
DELETE /people/:id
```

### What each pathway does: 
| Field | Data Type |
| :--- |:--- |
| GET /houses | Display all houses |
| GET /houses/:id | Display address, posstcode, owner & number of occupants at specific house |
| GET /houses/:id/occupants | Display address, names and ages of occupants at specific house |
| POST /houses | Allows a new house to be added to database; redirects |
| DELETE /houses/:id | Removes house from database |
| GET /people | Data Type |
| POST /people | Adds new person to database; redirects |
| PATCH /people/:id | Allows updating of persons name and address within database |
| DELETE /people/:id | Removes house from database |

## Example Request:
```
GET /houses/:id
res = 200
Host: api.neighbourstalker.com
Authorisation: 123456789qwertyuiop
Content-Type: application/json
Accept: application/json

[
    {
    "Home Address": "123 Fake Street",
    "Postcode": "AB1 2CD",
    "Owner": "John Doe",
    "Occupant No": 2,
    "Occupants": '[{"FirstName": "John", "LastName": "Johnson", "Age": 21, "DoB":1/1/2000}, {"FirstName": "Joe", "LastName": "Johnson", "Age": 27, "DoB":1/1/1994}]', 
    }
]
```

## Additional API Rules:


### Possible Errors:
| HTTP Error | Error Message |
| :--- |:--- |
| 400 - Bad Request | Required fields weren't filled in properly |
| 401 - Unauthorised | Server Understood Request, but request has not been applied because it lacks valid authentication credentials for the target resource. |
| 403 - Forbidden | Server Understood Request But Refuses to Authorise |
