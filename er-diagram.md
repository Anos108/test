```mermaid
erDiagram
    AIRPORT {
      string Airport_code PK
      string Name
      string City
      string State
    }

    AIRPLANE_TYPE {
      string Type_name PK
      string Company
      int Max_seats
    }

    AIRPLANE {
      string Airplane_id PK
      int Total_no_of_seats
    }

    FLIGHT {
      string Airline PK1
      int Number PK2
      string Weekdays
    }

    FLIGHT_LEG {
      string Airline FK
      int Number FK
      int Leg_no PK3
      string Dep_airport_code FK
      string Arr_airport_code FK
      datetime Scheduled_dep_time
      datetime Scheduled_arr_time
    }

    LEG_INSTANCE {
      string Airline FK
      int Number FK
      int Leg_no FK
      date Date PK4
      int No_of_avail_seats
      datetime Dep_time
      datetime Arr_time
    }

    FARE {
      string Airline FK
      int Number FK
      string Code PK3
      decimal Amount
      string Restrictions
    }

    SEAT {
      string Seat_no PK
    }

    RESERVATION {
      string Customer_name
      string Cphone
    }

    %% Relationships (Crow's Foot)
    AIRPLANE_TYPE ||--o{ AIRPLANE : "TYPE"
    AIRPLANE_TYPE }o--o{ AIRPORT : "CAN_LAND"

    FLIGHT ||--o{ FLIGHT_LEG : "LEGS"

    %% FLIGHT_LEG airports (scheduled times are attributes on FLIGHT_LEG)
    AIRPORT ||--o{ FLIGHT_LEG : "DEPARTURE"
    AIRPORT ||--o{ FLIGHT_LEG : "ARRIVAL"

    %% Instances of legs
    FLIGHT_LEG ||--o{ LEG_INSTANCE : "INSTANCE_OF"

    %% LEG_INSTANCE airports (actual times are attributes on LEG_INSTANCE)
    AIRPORT ||--o{ LEG_INSTANCE : "DEPARTS"
    AIRPORT ||--o{ LEG_INSTANCE : "ARRIVES"

    %% Assignment of airplane to a leg instance
    AIRPLANE ||--o{ LEG_INSTANCE : "ASSIGNED"

    %% Fares per flight
    FLIGHT ||--o{ FARE : "FARES"

    %% Reservations: seat booked on a leg instance
    LEG_INSTANCE ||--o{ RESERVATION : "RESERVATION"
    SEAT ||--o{ RESERVATION : "RESERVATION"
```
