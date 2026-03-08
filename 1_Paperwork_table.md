Paper Work – CDAC Admission System

| No. | Field     | Details               |
| --- | --------- | --------------------- |
| 1   | Form_no   | Int, compulsory       |
| 2   | Name      | Alphabets, compulsory |
| 3   | CCAT_rank | Int                   |

Address
| No. | Field      | Details         |
| --- | ---------- | --------------- |
| 1   | Address_id | Int, compulsory |
| 2   | Street     | Chars           |
| 3   | State      | Alphabets       |
| 4   | Pincode    | Int, 6 digits   |
| 5   | City       | Alphabets       |

Student_detail
| No. | Field      | Details          |
| --- | ---------- | ---------------- |
| 1   | Form_no    | Int, Foreign Key |
| 2   | Address_id | Int, Foreign Key |

Courses
| No. | Field       | Details          |
| --- | ----------- | ---------------- |
| 1   | Course_id   | Int              |
| 2   | Course_name | Chars            |
| 3   | Course_fees | Fractional value |

CDAC_Centre
| No. | Field           | Details                  |
| --- | --------------- | ------------------------ |
| 1   | Centre_id       | Int                      |
| 2   | Centre_name     | Chars                    |
| 3   | Centre_pincode  | Int, 6 digits            |
| 4   | Centre_capacity | Int (cannot be negative) |

Preferences
| No. | Field         | Details          |
| --- | ------------- | ---------------- |
| 1   | Preference_id | Int              |
| 2   | Form_no       | Int, Foreign Key |
| 3   | Centre_id     | Int, Foreign Key |
| 4   | Course_id     | Int, Foreign Key |
| 5   | Preference_no | Int              |
| 6   | Freeze        | Boolean (Yes/No) |


Seat_Allocation
| No. | Field         | Details |
| --- | ------------- | ------- |
| 1   | Allocation_id | Int     |
| 2   | Form_no       | Int     |
| 3   | Course_id     | Int     |
| 4   | Centre_id     | Int     |
| 5   | Round_no      | Int     |

