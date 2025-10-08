````markdown name=ER-diagram.md
# Airline ER Diagram (Mermaid) — Safe rendering

```mermaid
erDiagram
    AIRPORT {
      string Airport_code
      string Name
      string City
      string State
    }

    AIRPLANE_TYPE {
      string Type_name
      string Company
      int Max_seats
    }

    AIRPLANE {
      string Airplane_id
      int Total_no_of_seats
    }

    FLIGHT {
      string Airline
      int Number
      string Weekdays
    }

    FLIGHT_LEG {
      string Airline
      int Number
      int Leg_no
      string Dep_airport_code
      string Arr_airport_code
      datetime Scheduled_dep_time
      datetime Scheduled_arr_time
    }

    LEG_INSTANCE {
      string Airline
      int Number
      int Leg_no
      date Date
      int No_of_avail_seats
      datetime Dep_time
      datetime Arr_time
    }

    FARE {
      string Airline
      int Number
      string Code
      decimal Amount
      string Restrictions
    }

    SEAT {
      string Seat_no
    }

    RESERVATION {
      string Customer_name
      string Cphone
    }

    %% Relationships (Crow's Foot)
    AIRPLANE_TYPE ||--o{ AIRPLANE : "TYPE"
    AIRPLANE_TYPE }o--o{ AIRPORT : "CAN_LAND"

    FLIGHT ||--o{ FLIGHT_LEG : "LEGS"

    AIRPORT ||--o{ FLIGHT_LEG : "DEPARTURE"
    AIRPORT ||--o{ FLIGHT_LEG : "ARRIVAL"

    FLIGHT_LEG ||--o{ LEG_INSTANCE : "INSTANCE_OF"

    AIRPORT ||--o{ LEG_INSTANCE : "DEPARTS"
    AIRPORT ||--o{ LEG_INSTANCE : "ARRIVES"

    AIRPLANE ||--o{ LEG_INSTANCE : "ASSIGNED"

    FLIGHT ||--o{ FARE : "FARES"

    LEG_INSTANCE ||--o{ RESERVATION : "RESERVATION"
    SEAT ||--o{ RESERVATION : "RESERVATION"
