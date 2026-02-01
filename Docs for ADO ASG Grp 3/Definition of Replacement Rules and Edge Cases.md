### **3.1.2 Defined Replacement Rules**

| Rule ID | Issue Type | Example Values | Replacement Value | Logic Applied (SQL) |
| :--- | :--- | :--- | :--- | :--- |
| **R1** | Empty/Blank Strings | `""`, `" "` | `NULL` | `NULLIF(TRIM(Column), '')` |
| **R2** | Explicit Placeholders | `"N/A"`, `"Unknown"`, `"Null"` | `NULL` | `CASE WHEN Column IN ('N/A', 'Unknown') THEN NULL...` |
| **R3** | Text formatting | `"  Store A  "` | `"Store A"` | `TRIM(Column)` |
| **R4** | Invalid Zeroes | `0` (in text fields) | `NULL` | `NULLIF(Column, '0')` |

