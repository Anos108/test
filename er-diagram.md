
Nguyên nhân lỗi và cách sửa nhanh
- Mermaid ER trên GitHub không chấp nhận hậu tố số như PK1, PK2, PK3, PK4. Chỉ dùng PK hoặc FK (không có số).
- Lỗi bạn gặp “Expecting 'ATTRIBUTE_WORD', got 'ATTRIBUTE_KEY'” xảy ra khi parser thấy FK (hoặc PK) ở vị trí nó đang chờ tên thuộc tính, thường là do dòng trước có token PKx không hợp lệ làm “vỡ” cú pháp hoặc do hai thuộc tính dính trên cùng một dòng.
- Cách an toàn nhất để hiển thị trên GitHub: bỏ toàn bộ PK/FK trên dòng thuộc tính (chỉ để type + name). Khóa/quan hệ vẫn thể hiện bằng các đường nối.

Dưới đây là 2 bản đã sửa. Bản A (an toàn nhất) bỏ PK/FK trong phần thuộc tính. Bản B giữ PK/FK nhưng chuẩn hóa về PK/FK (không số). Bạn chỉ cần dùng một trong hai.

Bản A — chắc chắn render trên GitHub
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
