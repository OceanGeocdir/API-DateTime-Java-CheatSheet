# DATA TIME API JAVA

# A. Date-time API Overview

## 1. Introduction

- TỔNG QUAN VỀ API-THỜI GIAN [API-time]

  > Được dùng ISO-8061 như một loại lịch mặc định, dựa vào hệ thống lịch Gregory.

  > The Date-Time API sử dụng:

1. **Unicode Common Locale Data Repository (CLDR)** {Kho dữ liệu Vùng Loại ngôn ngữ Chung Unicode} **{ yyyy-MM-dd HH:mm:ss}**
1. **_Time-Zone Database_** (TZDB). {Cơ sở dữ liệu múi giờ}
1. Cung cấp thông tin múi giờ từ năm 1970 đến nay

### 1.1 Đặc trưng của The Date-time API là một số lịch đặc biệt có thể được sử dụng như:

- _Lịch Hijrah (Hồi giáo)_: HijrahChronology và HijrahDate cho việc làm việc với lịch Hồi giáo.

```
import java.time.chrono.HijrahChronology;
import java.time.chrono.HijrahDate;
```

- _Lịch Minguo (Đài Loan)_: MinguoChronology và MinguoDate cho việc làm việc với lịch Minguo, được sử dụng tại Đài Loan.

```
import java.time.chrono.MinguoChronology;
import java.time.chrono.MinguoDate;
```

- _Lịch Japanese (Nhật Bản)_: JapaneseChronology và JapaneseDate cho việc làm việc với lịch Nhật Bản.

```JapaneseChronology
import java.time.chrono.JapaneseChronology;
import java.time.chrono.JapaneseDate;
```

- _Lịch ThaiBuddhist (Thái Lan)_: ThaiBuddhistChronology và ThaiBuddhistDate cho việc làm việc với lịch Thái Lan theo lịch Phật giáo Thái.

```
import java.time.chrono.ThaiBuddhistChronology;
import java.time.chrono.ThaiBuddhistDate;
```

- _Lịch Minguo (Đại học Môn)_: MinguoChronology và MinguoDate cho việc làm việc với lịch Minguo, được sử dụng tại Đại học Môn ở Mông Cổ.

```
import java.time.chrono.MinguoChronology;
import java.time.chrono.MinguoDate;
```

## 2. Design Principal (Nguyên tắt thiết kế)

- Rõ Ràng (**Clear**):
  Các phương thức trong API được định nghĩa rõ ràng và hành vi của chúng được hiểu và dự đoán. Ví dụ, gọi một phương thức Ngày-Thời gian với tham số giá trị null thường sẽ gây ra một NullPointerException (lỗi tham chiếu đến null).

- Mềm Mượt (**Fluent**):
  API Ngày-Thời gian cung cấp giao diện mềm mượt, làm cho mã nguồn dễ đọc. Vì hầu hết các phương thức không cho phép tham số với giá trị null và không trả về giá trị null, bạn có thể nối các cuộc gọi phương thức lại với nhau và mã nguồn kết quả có thể hiểu nhanh chóng.

- Không Thay Đổi (**Immutable**):
  Hầu hết các lớp trong API Ngày-Thời gian tạo ra các đối tượng không thay đổi [immutable], có nghĩa là sau khi đối tượng được tạo, nó không thể được sửa đổi. Để thay đổi giá trị của đối tượng không thay đổi, bạn cần tạo một đối tượng mới như một bản sao được sửa đổi từ ban đầu. Điều này cũng có nghĩa rằng API Ngày-Thời gian, theo định nghĩa, là an toàn đối với luồng (thread-safe).

- Mở Rộng (**Extensible**):
  API Ngày-Thời gian là mở rộng mọi nơi có thể. Ví dụ, bạn có thể tự định nghĩa các bộ điều chỉnh thời gian và truy vấn riêng của bạn, hoặc xây dựng hệ thống lịch riêng của bạn.

## 3. DATE-Time PACKAGE

### 3.1 java.time PACKAGE

**Gói java.time**:

Gói chính của API Ngày-Thời gian. Chứa các lớp cho việc biểu diễn và quản lý ngày, thời gian, khoảng thời gian và độ dài thời gian.

1. **[java.time]** là gói chính để làm việc với các khái niệm cơ bản liên quan đến ngày-thời gian như {instants} (điểm thời gian cụ thể), durations (độ dài thời gian), dates (ngày), times (thời gian), time zones (múi giờ) và periods (khoảng thời gian).

2. Các lớp trong gói này dựa trên hệ thống lịch ISO, là hệ thống lịch tiêu chuẩn được sử dụng toàn cầu, và các lớp này là không thay đổi (immutable) và an toàn đối với việc đa luồng (thread-safe).

```java.time
import java.time.[tên class trong package]
```

##### **Gói java.time.chrono:**

- Chứa API để biểu diễn các hệ thống lịch khác với lịch ISO mặc định. Cho phép làm việc với các hệ thống lịch như **Hijrah (Hồi giáo)**, **Minguo (Đài Loan)**, **Japanese (Nhật Bản)**, và **ThaiBuddhist (Thái Lan)**. Cũng cho phép tạo ra các hệ thống lịch tùy chỉnh.

##### **Gói java.time.format:**

- Chứa các lớp để định dạng và phân tích các chuỗi ngày-thời gian, để chuyển đổi giữa các đối tượng ngày-thời gian và chuỗi.

##### **Gói java.time.temporal:**

- Mở rộng PI cho việc tương tác giữa các lớp ngày-thời gian, cho phép truy vấn và điều chỉnh trường thời gian (TemporalField và ChronoField) và đơn vị thời gian (TemporalUnit và ChronoUnit).

##### **Gói java.time.zone**

- Chứa các lớp hỗ trợ cho việc làm việc với múi giờ, chênh lệch múi giờ từ múi giờ, và quy tắc múi giờ.
- Mỗi loại lớp ngày-thời gian có mục đích và ứng dụng khác nhau.

  > Ví dụ: Instant đại diện cho một thời điểm cụ thể, LocalDate lưu trữ một ngày không kèm theo múi giờ, LocalTime lưu trữ một thời gian không kèm theo ngày, ZonedDateTime lưu trữ ngày-thời gian kèm theo múi giờ, và nhiều lớp khác để biểu diễn các khái niệm ngày-thời gian khác nhau.

- Gói này cung cấp một loạt các phương thức để thao tác với các đối tượng ngày-thời gian, cho phép bạn thực hiện các hoạt động như tạo, cộng/trừ thời gian, chuyển đổi kiểu dữ liệu, kiểm tra điều kiện và nhiều hoạt động khác liên quan đến ngày-thời gian.

#### **java.time.[CLASS]**

1.  **CLOCK**

- Một đồng hồ cung cấp quyền truy cập đến thời điểm hiện tại, ngày và thời gian sử dụng múi giờ.

```java
import java.time.Clock;

Clock clock = Clock.systemDefaultZone();
Instant instant = Instant.now(clock);
System.out.println(instant);
```

2.  **Duration**

- Một lượng thời gian dựa trên thời gian, chẳng hạn như '34.5 giây'.

```java
Duration duration = Duration.of(amount, ChronoUnit.CHRONO_UNIT_CONSTANT);
```

- Tạo khoảng thời gian 20 giờ

```java
Duration duration = Duration.ofHours(20);
```

```diff
--- // Output: PT20H (20 hours)
```

3.  **Instant**

- Một điểm tức thời trên dòng thời gian.

```java
Instant instant = Instant.now();
```

```diff
---> Output: 2023-08-20T15:16:26.355Z
```

4. **LocalDate**

- Một ngày không kèm theo múi giờ trong hệ thống lịch ISO-8601, ví dụ như 2007-12-03.

```java
LocalDate localDate = LocalDate.of(year, month, day);
```

```java
LocalDate localDate = LocalDate.of(2023, 8, 20);
```

```diff
---> Output: 2023-08-20
```

5. **LocalDateTime**

- Một ngày-thời gian không kèm theo múi giờ trong hệ thống lịch ISO-8601, ví dụ như 2007-12-03T10:15:30.

```java
LocalDateTime localDateTime = LocalDateTime.of(year, month, day, hour, minute, second, nanosecond);
```

- Examples: Tạo ngày và thời gian cụ thể

```java
LocalDateTime localDateTime = LocalDateTime.of(2023, 8, 20, 8, 16, 26, 937);
```

```diff
--- Output: 2023-08-20T08:16:26.937
```

6. **LocalTime**

- Một thời gian không kèm theo múi giờ trong hệ thống lịch ISO-8601, ví dụ như 10:15:30.

```java
LocalTime localTime = LocalTime.of(hour, minute, second, nanosecond);
```

- Tạo thời gian cụ thể

```
LocalTime localTime = LocalTime.of(8, 16, 26, 943);
```

```diff
--- Output: 08:16:26.943
```

7. **MonthDay**

- Một tháng-ngày trong hệ thống lịch ISO-8601, ví dụ như --12-03.

```java
MonthDay monthDay = MonthDay.of(month, day);
```

- Tạo tháng và ngày cụ thể

```
MonthDay monthDay = MonthDay.of(Month.AUGUST, 20);
```

```diff
--- // Output: --08-20
```

8. **OffsetDateTime**

- Một ngày-thời gian với một chênh lệch từ UTC/Greenwich trong hệ thống lịch ISO-8601, ví dụ như 2007-12-03T10:15:30+01:00.

```java
OffsetDateTime offsetDateTime = OffsetDateTime.of(year, month, day, hour, minute, second, nanosecond, ZoneOffset.ofHours(offsetHours));
```

- Tạo ngày, thời gian và độ lệch múi giờ

```
OffsetDateTime offsetDateTime = OffsetDateTime.of(2023, 8, 20, 8, 16, 26, 954, ZoneOffset.ofHours(-7));
```

```diff
--- Output: 2023-08-20T08:16:26.954-07:00
```

9. **OffsetTime**

- Một thời gian với một chênh lệch từ UTC/Greenwich trong hệ thống lịch ISO-8601 _ví dụ như 10:15:30+01:00._

```java
OffsetTime offsetTime = OffsetTime.of(hour, minute, second, nanosecond, ZoneOffset.ofHours(offsetHours));
```

- Tạo thời gian và độ lệch múi giờ

```
OffsetTime offsetTime = OffsetTime.of(8, 16, 26, 957, ZoneOffset.ofHours(-7));
```

```diff
--- // Output: 08:16:26.957-07:00
```

10. **Period**

- Một lượng thời gian dựa trên ngày trong hệ thống lịch ISO-8601,
  chẳng hạn như '2 năm, 3 tháng và 4 ngày'.

```java
Period period = Period.of(amountYears, amountMonths, amountDays);
```

- Tạo khoảng thời gian 10 ngày

```java
Period period = Period.ofDays(10);
```

```diff
--- // Output: P10D (10 days)
```

11. **Year**

- Một năm trong hệ thống lịch ISO-8601, chẳng hạn như 2007.

```[Year] code
Year year = Year.of(year);
```

- Tạo một năm cụ thể

```java
Year year = Year.of(2023);
```

```diff
--- // Output: 2023
```

12. **YearMonth**

- Một năm-tháng trong hệ thống lịch ISO-8601, chẳng hạn như 2007-12.

```[YearMonth] code
YearMonth yearMonth = YearMonth.of(year, month);
```

- Tạo một năm và tháng cụ thể

```java
YearMonth yearMonth = YearMonth.of(2023, 8);
```

```diff
--- // Output: 2023-08
```

13. **ZonedDateTime**

- Một ngày-thời gian với múi giờ trong hệ thống lịch ISO-8601,
  chẳng hạn như 2007-12-03T10:15:30+01:00 Europe/Paris.

```java
ZonedDateTime zonedDateTime = ZonedDateTime.of(year, month, day, hour, minute, second, nanosecond, ZoneId.of("Zone_ID"));
```

- Tạo ngày, thời gian và múi giờ cụ thể

```java
ZonedDateTime zonedDateTime = ZonedDateTime.of(2023, 8, 21, 0, 16, 26, 941, ZoneId.of("Asia/Tokyo"));
```

```diff
--- // Output: 2023-08-21T00:16:26.941+09:00[Asia/Tokyo]
```

14. **ZoneId**

- Một ID múi giờ, chẳng hạn như Europe/Paris.

```java
ZoneId zoneId = ZoneId.of("Zone_ID");
```

-

```

```

```diff
---
```

15. **ZoneOffset**

- Một chênh lệch múi giờ từ Greenwich/UTC, chẳng hạn như +02:00.

```java
ZoneOffset zoneOffset = ZoneOffset.of("Zone_Offset");
```

-

```
ZoneOffset zoneOffset = ZoneOffset.of("+02:00");
```

```diff
--- //Output: +02:00
```

16 **Instant:**

- Instant là một dấu thời gian số họcInstant hiện tại có thể được lấy từ một đối tượng ClockInstant thường được sử dụng để ghi log và lưu trữ một điểm thời gian cụ thể.

```java
Instant instant = Instant.now();
```

- Lấy thời điểm hiện tại

```
Instant instant = Instant.now();
```

```diff
--- // Output: 2023-08-20T15:16:26.355Z
```

17. **LocalDate:**

- LocalDate lưu trữ một ngày mà không kèm theo múi giờNó có thể được sử dụng để lưu trữ ngày sinh nhật.

```java
LocalDate localDate = LocalDate.of(year, month, day);
```

-

```

```

```diff
---
```

18. **LocalTime:**

- LocalTime lưu trữ một thời gian mà không kèm theo ngàyNó có thể được sử dụng để lưu trữ thời gian mở cửa hoặc đóng cửa.

```java

```

-

```

```

```diff
---
```

19. **LocalDateTime:**

- LocalDateTime lưu trữ cả ngày và thời gian mà không kèm theo múi giờ.

```java

```

-

```

```

```diff
---
```

20. **ZonedDateTime:**

- ZonedDateTime lưu trữ cả ngày, thời gian và múi giờ.

```java

```

-

```

```

```diff
---
```

21. **Duration:**

- Duration là một khoảng thời gian dựa trên thời gian, ví dụ '35 seconds'.

```java

```

-

```

```

```diff
---
```

22. **Period**

- Period là một khoảng thời gian dựa trên ngày, ví dụ '2 years, 3 months and 4 days'.

```java
Period period = Period.of(amountYears, amountMonths, amountDays);
```

- Tạo khoảng thời gian 10 ngày

```
Period period = Period.ofDays(10);
```

```diff
--- // Output: P10D (10 days)
```

23. **Month** [ENUM]

- Month lưu trữ một tháng riêng lẻ trong năm, ví dụ như "DECEMBER".

```java
Month month = Month.MONTH_CONSTANT;
```

- Lấy giá trị của tháng [Month_constant]

```
Month august = Month.AUGUST;
```

```diff
--- //Output: AUGUST
```

24. **DayOfWeek** [ENUM]

- DayOfWeek lưu trữ một ngày trong tuần riêng lẻ, ví dụ như "TUESDAY".

```java
public enum DayOfWeek {
  MONDAY,
  TUESDAY,
  WEDNESDAY,
  THURSDAY,
  FRIDAY,
  SATURDAY,
  SUNDAY
}
```

- Thêm ngày từ ngày hiện tại bằng method **flus()**;

```
import java.time.DayOfWeek;

public class DayOfWeekExample {
    public static void main(String[] args) {
        DayOfWeek currentDay = DayOfWeek.WEDNESDAY; // Ngày hiện tại là Thứ Tư
        int daysToAdd = 5; // Số ngày thêm vào

        DayOfWeek futureDay = currentDay.plus(daysToAdd); // Thêm 5 ngày vào Thứ Tư
        System.out.printf("Future day: %s%n", futureDay); // In kết quả
    }
}
```

```diff
--- Future day: MONDAY
```

25. **Year**

- Year lưu trữ một năm riêng lẻ, ví dụ như "2010".

```java
Year year = Year.of(year);
```

- Tạo một năm cụ thể

```
Year year = Year.of(2023);
```

```diff
--- // Output: 2023
```

26. **YearMonth**

- YearMonth lưu trữ một cặp năm và tháng, ví dụ như "2007-12".

```java
YearMonth yearMonth = YearMonth.of(year, month)
```

- Tạo một năm và tháng cụ thể

```java
YearMonth yearMonth = YearMonth.of(2023, 8);
```

```diff
--- // Output: 2023-08
```

27. **MonthDay:**

- MonthDay lưu trữ một cặp tháng và ngày, ví dụ như "--12-03" (ngày 3 tháng 12).

```java
MonthDay monthDay = MonthDay.of(Month.MONTH_CONSTANT, DAY);
```

-

```java

```

```diff
---
```

28. **OffsetTime:**

- OffsetTime lưu trữ thời gian và chênh lệch múi giờ từ UTC mà không kèm theo ngày, ví dụ như "11:30+01:00".

```java
OffsetTime offsetTime = OffsetTime.of(hour, minute, second, nanosecond, ZoneOffset.ofHours(offsetHours));
```

- Tạo **thời gian** và độ lệch múi giờ

```
OffsetTime offsetTime = OffsetTime.of(8, 16, 26, 957, ZoneOffset.ofHours(-7));
```

```diff
--- // Output: 08:16:26.957-07:00
```

29. **OffsetDateTime:**

- OffsetDateTime lưu trữ ngày, thời gian, và chênh lệch múi giờ từ UTC, ví dụ như "2010-12-03T11. 30+01. 00".

```java
OffsetDateTime offsetDateTime = OffsetDateTime.of(year, month, day, hour, minute, second, nanosecond, ZoneOffset.ofHours(offsetHours));
```

- Tạo **ngày**, thời gian và độ lệch múi giờ

```
OffsetDateTime offsetDateTime = OffsetDateTime.of(2023, 8, 20, 8, 16, 26, 954, ZoneOffset.ofHours(-7));
```

```diff
--- // Output: 2023-08-20T08:16:26.954-07:00
```

### 3.2 **Method Naming Conventions**

> Table of Method Naming Conventions

| No. | Prefix | Method Type        | USE                                                                                                                                                                                                                                                 |
| :-- | :----- | :----------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | of     | **static factory** | Phương thức tạo ra một phiên bản khi nhà máy chủ yếu đang xác nhận thông số đầu vào, không phải là chuyển đổi chúng._Xác thực phương thức đầu vào_                                                                                                  |
| 2   | from   | **static factory** | Phương thức tạo ra một phiên bản bằng cách chuyển đổi thông số đầu vào thành một phiên bản của lớp mục tiêu, có thể liên quan đến việc mất thông tin từ đầu vào. _Không xác thực phương thức đầu vào_                                               |
| 3   | parse  | **static factory** | Phương thức tạo ra một phiên bản bằng cách phân tích chuỗi đầu vào để tạo ra một phiên bản của lớp mục tiêu.                                                                                                                                        |
| 4   | format | **instance**       | Phương thức tạo ra một phiên bản bằng cách phân tích chuỗi đầu vào để tạo ra một phiên bản của lớp mục tiêu._(Nó được sử dụng để định dạng các giá trị trong đối tượng thời gian thành một chuỗi)_                                                  |
| 5   | get    | **instance**       | Nó được sử dụng để lấy một phần trạng thái của đối tượng đích. _[phương thức thể hiện trả về một phần của trạng thái của đối tượng mục tiêu.]_                                                                                                      |
| 6   | is     | **instance**       | phương thức thể hiện truy vấn trạng thái của đối tượng mục tiêu. _(phương thức thể hiện truy vấn trạng thái của đối tượng mục tiêu.)_                                                                                                               |
| 7   | with   | **instance**       | phương thức thể hiện trả về một bản sao của đối tượng mục tiêu với một phần tử đã thay đổi; đây là sự tương đương bất biến với phương thức set trên JavaBean. _[Nó được sử dụng để tạo một bản sao của đối tượng đích với một phần tử bị thay đổi]_ |
| 8   | plus   | **instance**       | Nó được sử dụng để tạo một bản sao của đối tượng đích với một khoảng thời gian được thêm vào. _[phương thức thể hiện trả về một bản sao của đối tượng mục tiêu với một khoản thời gian được thêm vào.]_                                             |
| 9   | minus  | **instance**       | Nó được sử dụng để tạo một bản sao của đối tượng đích với một khoảng thời gian bị trừ đi._[phương thức thể hiện trả về một bản sao của đối tượng mục tiêu với một khoản thời gian được trừ đi]_                                                     |
| 10  | to     | **instance**       | Phương thức thể hiện chuyển đối tượng này thành một kiểu khác. _[Nó được sử dụng để chuyển đổi đối tượng đích thành một loại khác]_                                                                                                                 |
| 11  | at     | **instance**       | Nó được sử dụng để kết hợp đối tượng đích với một đối tượng khác. _[phương thức thể hiện kết hợp đối tượng này với một đối tượng khác.]_                                                                                                            |

> Static Factory :

> Instance :

## 4. java.time.chrono:

- Chứa API để biểu diễn các hệ thống lịch khác với lịch ISO mặc định. Cho phép làm việc với các hệ thống lịch như + **Hijrah (Hồi giáo)** + **Minguo (Đài Loan)** + **Japanese (Nhật Bản)** + **ThaiBuddhist (Thái Lan)**
  Cũng cho phép tạo ra các hệ thống lịch tùy chỉnh.

```java
import java.time.chrono;
```

## 5. java.time.format:

Chứa các lớp để định dạng và phân tích các chuỗi ngày-thời gian, để chuyển đổi giữa các đối tượng ngày-thời gian và chuỗi.

```java
import java.time.format;
```

## 6. java.time.temporal:

Mở rộng PI cho việc tương tác giữa các lớp ngày-thời gian, cho phép truy vấn và điều chỉnh trường thời gian (TemporalField và ChronoField) và đơn vị thời gian (TemporalUnit và ChronoUnit).

```java
import java.time.temporal;
```

## 7. java.time.zone:

Cung cấp các lớp cho múi giờ và giờ mùa hè.

```java
import java.time.zone;
```

## 8. Phương Thức NOW()

> Phương thức **now()** trà về một đối tượng Object đại diện cho thời gian hiện tại

- Cú pháp now() không có tham số, đối tượng trả về tính bằng mili giây bắt đầu từ 01/01/1970, 00:00:00 GMT

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

public class Example {

    public static void main(String[] args) {
        // Get the current date.
        LocalDate today = LocalDate.now();

        // Format the date in a human-readable format.
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");
        String formattedDate = formatter.format(today);

        // Print the formatted date to the console.
        System.out.println(formattedDate);
    }
}
```

```diff
*** Đoạn mã này sẽ in ra ngày hôm nay ở định dạng dd-MM-yyyy. Ví dụ, nếu ngày hôm nay là ngày 15 tháng 3 năm 2023, đoạn mã sẽ in ra 15-03-2023
```

# B. Standard Calendar

## 1. Tổng quan

1. Có 2 cách để biểu diễn thời gian
   - Cách của con người hiểu (năm, tháng, ngày, giờ, phút và giây)
   - Thời gian của máy móc:
     - Đo thời gian liên tục một điểm phân giải nanosecon
     - xác định thông tin biểu diễn: múi giờ, ngày tháng, thời gian, ngày.
2. Bảng tóm tắt các CLASS dưới đây dựa trên cột thời gian [temporal-based] cho phép lưu trữ thông tin ngày/giờ hoặc đo lường thời gian.

   - Dấu ✅ trong bảng là loại dữ liệu cụ thể mà CLASS đó sử dụng.
   - Cột _toString_ được hiển thị một phiên bản của lớp được in ra sử dụng của class đó với lớp được thể hiện

> Bảng tổng hợp về temporal-based [lớp thời gian]

| No. | Class or Enum  | Year | Month | Day  | Hours | Minutes | Seconds\* | Zone Offset | Zone ID | toString Output                           | Tìm hiểu thêm         |
| :-- | :------------- | :--- | :---- | :--- | :---- | :------ | :-------- | :---------- | :------ | :---------------------------------------- | :-------------------- |
| 1   | Instant        |      |       |      |       |         | ✓         |             |         | 2023-08-20T15:16:26.355Z                  | #6. [InstClass]       |
| 2   | LocalDate      | ✓    | ✓     | ✓    |       |         |           |             |         | 2023-08-20                                | #3. [DC]              |
| 3   | LocalDateTime  | ✓    | ✓     | ✓    | ✓     | ✓       | ✓         |             |         | 2023-08-20T08:16:26.937                   | #4. [Date&TimeCls]    |
| 4   | LocalTime      |      |       |      | ✓     | ✓       | ✓         |             |         | 08:16:26.943                              | #4. [Date&TimeCls]    |
| 5   | MonthDay       |      | ✓     | ✓    |       |         |           |             |         | --08-20                                   | #3. [DC]              |
| 6   | Year           | ✓    |       |      |       |         |           |             |         | 2023                                      | #3. [DC]              |
| 7   | YearMonth      | ✓    | ✓     |      |       |         |           |             |         | 2023-08                                   | #3. [DC]              |
| 8   | Month          |      | ✓     |      |       |         |           |             |         | DECEMBER                                  | #2. [ENUM_DoW_&_M]    |
| 9   | OffsetDateTime | ✓    | ✓     | ✓    | ✓     | ✓       | ✓         | ✓           |         | 2023-08-20T08:16:26.954-07:00             | #5. [TZone&OffsetC]   |
| 10  | OffsetTime     |      |       |      | ✓     | ✓       | ✓         | ✓           |         | 08:16:26.957-07:00                        | #5. [TZone&OffsetC]   |
| 11  | Duration       |      |       | \*\* | \*\*  | \*\*    | ✓         |             |         | PT20H (20 hours)                          | #9. [Period&Duration] |
| 12  | Period         | ✓    | ✓     | ✓    |       |         |           | \*\*\*      | \*\*\*  | P10D (10 days)                            | #9. [Period&Duration] |
| 13  | ZoneDateTime   | ✓    | ✓     | ✓    | ✓     | ✓       | ✓         | ✓           | ✓       | 2023-08-21T00:16:26.941+09:00[Asia/Tokyo] | #5. [TZone&OffsetC]   |

> \* Giây được ghi lại với độ chính xác đến nanosecond.

> \*\* Lớp này không lưu trữ thông tin này, nhưng có các phương thức để cung cấp thời gian trong các đơn vị này.

> \*\*\* Khi phương thúc (Period) được thêm vào method ZonedDateTime, việc các múi giờ sáng (daylight saving time) hoặc các khác biệt về múi giờ cục bộ được quan sát.

- Các phần của nội dung 2 được liệt kê 5 cái, dưới đây là 5 từ khoá để _Search_ , các #num là các section được viết ở dưới
  > 1. [ENUM_DoW_&_M]
  > 2. [DC]
  > 3. [Date&TimeCls]
  > 4. [TZone&OffsetC]
  > 5. [InstClass]
  > 6. [Period&Duration]

## 2. ENum cho DayOfWeek và Month Enums [ENUM_DoW_&_M]

1. **DayOfWeek** [24_ENUM]

- ENum DayOfWeek gồm 7 ngày, 7 ngày này là hằng số [CONSTANT] mô tả các ngày trong tuần từ thứ 2 (MONDAY) đến chủ nhật (SUNDAY).
- Các hằng số CONSTANT này có giá trị nguyên từ [1] {Thứ 2} đến [7] {Chủ Nhật}.
- Sử dụng dòng cođe HẰNG SỐ [CONSTANT] đã được package java.time định nghĩa (**DayOfWeek.DAY_CONSTANT**)

- Code ví dụ:

```java
System.out.printf("%s%n", DayOfWeek.MONDAY.plus(3));
```

```diff
--- // Output: "THURSDAY"
```

```diff
*** Đoạn code trên có hằng số định nghĩa thứ 2
      >  DayOfWeek.MONDAY
--- Dùng phương thức plus để thêm số ngày từ ngày cố định là 3
      > Thứ 2 + 3 ngày = thứ 5
```

- Phương thức lấy chuỗi đại diện cho ngày trong tuần theo ngôn ngữ người dùng.

```java
getDisplayName(TextStyle style, Locale locale)
```

```java
DayOfWeek dow = DayOfWeek.MONDAY;
Locale locale = Locale.getDefault();
System.out.println("1. TextStyle.FULL:" + dow.getDisplayName(TextStyle.FULL, locale));
System.out.println("2. TextStyle.NARROW:" + dow.getDisplayName(TextStyle.NARROW, locale));
System.out.println("3. TextStyle.SHORT:" + dow.getDisplayName(TextStyle.SHORT, locale));
```

```diff
--- // Output: "1. TextStyle.FULL: Monday"
--- // Output: "2. TextStyle.NARROW: M"
--- // Output: "3. TextStyle.SHORT: Mon"
```

> ENUM CONSTANT của DayOfWeek phải viết bằng dấu viết hoa [CAPLOCKS]

2. **Month** [23_ENUM]

- ENUM Months bao gồm các giá trị hằng số [CONSTANT] 12 tháng trong năm: _JANUARY_ đến _DECEMBER_
- Giá trị số nguyên bao gồm 12 số từ 1(_January_) đến 12(_December_)
- Sử dụng các hằng số đã định nghĩa để có thể dễ đọc hơn [**Month.Month_CONSTANT**]

--> In số ngày trong tháng

```java
System.out.printf("%d%n", Month.FEBRUARY.maxLength());
```

```diff
--- // Output: "29"
```

- Lấy kiểu giá trị

```java
Month month = Month.AUGUST;
Locale locale = Locale.getDefault();
System.out.println(month.getDisplayName(TextStyle.FULL, locale));
System.out.println(month.getDisplayName(TextStyle.NARROW, locale));
System.out.println(month.getDisplayName(TextStyle.SHORT, locale));
```

```diff
--- // Output: "August"
--- // Output: "A"
--- // Output: "Aug"
```

## 3. Date Classes [DC]

**Các CLASS liên quan đến DAYS trong java.time**

- Có 4 lớp xử lý thông tin chính về ngày và không liên quan đến thời gian hay múi giờ. Như bảng tóm tắt đã đề cập thì có tận 4 CLASS liên quan là
  - LocalDate (No.2)
  - YearMonth (No.5)
  - MonthDay (No.6)
  - Year (No.7)

1.  Class **LocalDate**

```java
import java.time.LocalDate
```

```diff
import java.time.LocalDate;

public class Example {

     public static void main(String[] args) {
---    LocalDate localDate = LocalDate.of(2023, 8, 20);
       System.out.println(localDate); // 2023-08-20
  }
}
```

```diff
---> Dùng method of để gán cho một ngày cụ thể để lấy giá trị về ngày tháng năm
--- // Output: 2023-08-20
--->  20 Aug 2023
```

Ngoài phương thức thường, LocalDate còn cung cấp các phương thức getter để lấy thông tin về một ngày cụ thể, dựa vào thời gian đã được cung cấp

```java
DayOfWeek dotw = LocalDate.of(2023, Month.SEPTEMBER, 2).getDayOfWeek();
```

```diff
---> Output: THURSDAY
```

```
-> getDayOfWeek()
```

2. Class **YearMonth**

   YearMonth sẽ biểu diễn tháng của một năm cụ thể. Ta có thể dùng YearMonth để:

   - Kiểm tra xem 2 năm có bằng nhau không
   - Tính toán khoảng cách giữa 2 năm, tháng
   - Lấy tháng đầu tiên và tháng cuối cùng trong năm
   - So sánh năm tháng với một năm tháng cụ thể.

```java
YearMonth yearMonth1 = YearMonth.of(2023, 2);
YearMonth yearMonth2 = YearMonth.of(2025, 2);

System.out.println(yearMonth1 == yearMonth2);
```

```diff
---> Output: false
mặc dù là cùng tháng 2 nhưng nằm ở 2 năm khác nhau nên 'False'
```

3. Class **MonthDay**

MonthDay biểu diễn ngày của một tháng cụ thể, ví dụ 'Tết Dương Lịch' vào ngày 01 tháng 01.

> Method: Checks if the year is valid for this month-day.

```java
isValidYear(int year)
```

- Xác định năm nhuận bằng ngày 29 của tháng 2

```java
MonthDay date = MonthDay.of(Month.FEBRUARY, 29);
boolean validLeapYear = date.isValidYear(2023);
```

```diff
---> Output: false
```

4. Class **Year**

Biểu diễn một năm cụ thể. Ví dụ: kiểm tra một năm có phải năm nhuận hay không ?

> Method: isLeap();

```java
Year year = Year.of(2023);
System.out.println(year.isLeap());

year = Year.of(2024);
System.out.println(year.isLeap());
```

```diff
---> Output: False
---> Output: True
```

## 4. Date & Time Classes [Date&TimeCls]

1. Class **LocalTime**

Giống như những Class khác, đại diện cho thời gian trong ngày, không bao gồm ngày, múi giờ. Chỉ bao gồm giờ , phút, giây và mili giây.

LocalTime được sử dụng để thực hiện nhiều nhiệm vụ khác nhau như tính toán thời gian, so sánh và định dạng.

```java
import java.time.LocalTime;
```

```java
LocalTime specificTime = LocalTime.of(14, 30, 45);
System.out.println("Thời gian cụ thể: " + specificTime);
```

```java
// Output: Thời gian cụ thể: 14:30:45
```

- Ví dụ về các đồng hồ điện tử

```java
LocalTime thisSec;

for (;;) {
    thisSec = LocalTime.now();

    // Hiện thực mã hiển thị được để lại cho người đọc thực hiện
    display(thisSec.getHour(), thisSec.getMinute(), thisSec.getSecond());
}
```

```diff
---> LocalTime thisSec;:
 Khai báo một biến thisSec kiểu LocalTime để lưu trữ thời gian hiện tại.

---> for (;;)
Bắt đầu vòng lặp vô hạn.
---> thisSec = LocalTime.now();:

Gán giá trị của biến thisSec bằng thời gian hiện tại sử dụng phương thức now() của lớp LocalTime.

---> display(thisSec.getHour(), thisSec.getMinute(), thisSec.getSecond());:
Gọi hàm display để hiển thị thông tin về giờ, phút và giây từ biến thisSec.
```

2. class **LocalDateTime**

- Class này xử lý _day_ và _time_, không có _zone time_, _zone id_. **LocalDateTime** là một trong các lớp đại diện cho cả _YYYY::mm::dd_ cùng với thời gian _HH::mm::ss::nanosecond_ và **LocalDateTime** = **LocalTime** + **LocalDate**.

- LocalDateTime là một Class thường được sử dụng để đại diện cho một sự kiện cụ thể.

  - Lưu trữ ngày và thời gian một sự kiện
  - So sánh hai ngày và thời gian
  - Tính khoảng thời gian giữa hai ngày và thời gian
  - Định dạng một ngày và thời gian thành một chuỗi văn bản
  - Phân tích một chuỗi văn bản thành một ngày và thời gian

- Lữu trữ ngày và thời gian của một sự kiện

```java
LocalDateTime eventDate = LocalDateTime.of(2023, 3, 8, 10, 00, 00);
```

```diff
---> Output: 2023-03-08T10:00:00
```

- SS Khoảng thời gian giữa hai ngày

```java
LocalDateTime startDateTime = LocalDateTime.of(2023, 3, 8, 10, 00, 00);
LocalDateTime endDateTime = LocalDateTime.of(2023, 3, 8, 11, 00, 00);

if (startDateTime.isBefore(endDateTime)) {
  System.out.println("Start date is before end date");
} else {
  System.out.println("Start date is after end date");
}
```

```diff
---> Output: Start date is before end date
```

- Tính khoản thời gian giữa hai ngày

```java
LocalDateTime startDateTime = LocalDateTime.of(2023, 3, 8, 10, 00, 00);
LocalDateTime endDateTime = LocalDateTime.of(2023, 3, 8, 11, 00, 00);

Duration duration = Duration.between(startDateTime, endDateTime);

System.out.println("The duration between the two dates is " + duration);
```

```diff
---> Output: PT1H (1Hours)
```

> Phân đoạn thời gian bằng KeyWord <PT#H>

- P is the _duration_ designator (for **period**) placed at the start of the duration representation.
  - Y is the **_year_** designator that follows the value for the number of calendar years.
  - M is the **_month_** designator that follows the value for the number of calendar months.
  - W is the **_*week*_** designator that follows the value for the number of weeks.
  - D is the **_*day*_** designator that follows the value for the number of calendar days.
- T is the **_*time*_** designator that precedes the time components of the representation.
  - H is the **_*hour*_** designator that follows the value for the number of hours.
  - M is the **_*minute*_** designator that follows the value for the number of minutes.
  - S is the **_*second*_** designator that follows the value for the number of seconds.

## 5. **Time Zone & Offset Classes** [TZone&OffsetC]

1. ZoneID && ZoneOffSet

   Time Zone hay còn gọi là múi giờ, múi giờ là thời gian chuẩn. Mỗi múi giờ được mô tả bằng một định danh và thông thường có định dạng [Region/City](Asia/Tokyo)(HoChiMinh/VietNam)

Có 2 lớp Time API được sử dụng để xác định múi giờ hoặc offset

- **ZoneId**: Xác định một định danh múi giờ và cung cấp các quy tắc để chuyển đổi giữa Instant và LocalDateTime
- **ZoneOffSet** Xác định độ lệch múi giờ từ thời gian chuẩn, múi giờ quốc tế. (Greenwich/UTC).

                                | Zone ID       | Zone Offset |
                                | :------------ | :---------- |
                                | UTC           | +00:00      |
                                | GMT           | +00:00      |
                                | EST           | -05:00      |
                                | CST           | -06:00      |
                                | MST           | -07:00      |
                                | PST           | -08:00      |
                                | AEST          | +10:00      |
                                | AEDT          | +11:00      |
                                | AWST          | +08:00      |
                                | CDT           | -06:00      |
                                | MDT           | -07:00      |
                                | PDT           | -08:00      |
                                | AEST (Mùa hè) | +11:00      |
                                | AEDT (Mùa hè) | +12:00      |
                                | AWST (Mùa hè) | +09:00      |

1. GMT là viết tắt của Greenwich Mean Time. Đây là múi giờ quốc tế, được sử dụng như một điểm chuẩn cho việc tính giờ ở các múi giờ khác nhau trên thế giới.
2. EST là viết tắt của Eastern Standard Time. Đây là múi giờ ở Hoa Kỳ và Canada, phía đông của đường đổi ngày quốc tế.
3. CST là viết tắt của Central Standard Time. Đây là múi giờ ở Hoa Kỳ và Canada, phía tây của múi giờ EST.
4. MST là viết tắt của Mountain Standard Time. Đây là múi giờ ở Hoa Kỳ và Canada, phía tây của múi giờ CST.
5. PST là viết tắt của Pacific Standard Time. Đây là múi giờ ở Hoa Kỳ và Canada, phía tây của múi giờ MST.
6. AEST là viết tắt của Australian Eastern Standard Time. Đây là múi giờ ở Úc, phía đông của đường đổi ngày quốc tế.
7. AEDT là viết tắt của Australian Eastern Daylight Time. Đây là múi giờ ở Úc, phía đông của đường đổi ngày quốc tế và sử dụng giờ tiết kiệm ánh sáng.
8. AWST là viết tắt của Australian Western Standard Time. Đây là múi giờ ở Úc, phía tây của đường đổi ngày quốc tế.
9. CDT là viết tắt của Central Daylight Time. Đây là múi giờ ở Hoa Kỳ và Canada, phía tây của múi giờ EST và sử dụng giờ tiết kiệm ánh sáng.
10. MDT là viết tắt của Mountain Daylight Time. Đây là múi giờ ở Hoa Kỳ và Canada, phía tây của múi giờ CST và sử dụng giờ tiết kiệm ánh sáng.
11. PDT là viết tắt của Pacific Daylight Time. Đây là múi giờ ở Hoa Kỳ và Canada, phía tây của múi giờ MST và sử dụng giờ tiết kiệm ánh sáng.

> Lưu ý: Mỗi khu vực, mỗi vùng có múi giờ riêng

2. **API Date-Time Class of ZoneTime && ZoneOffSet**

```java
import java.time.ZonedDateTime;
import java.time.OffsetDateTime;
import java.time.OffsetTime;
```

- **ZoneDateTime** xử lý một ngày và thời gian kèm theo múi giờ tương ứng và độ lệch múi giờ từ thời gian gốc quốc tế Greenwich/UTC

```java
import java.time.ZonedDateTime;
ZonedDateTime zonedDateTime = ZonedDateTime.now(ZoneId.of("Asia/Ho_Chi_Minh"));
System.out.println(zonedDateTime);
```

```java
// 2023-08-24T07:29:28+07:00
```

- **OffsetDateTime** xử lý một ngày và thời gian kèm theo độ lệch múi giờ từ thời gian Greenwich/UTC, không có ID múi giờ

```java
OffsetDateTime offsetDateTime = OffsetDateTime.now(ZoneOffset.UTC);
System.out.println(offsetDateTime);
```

```java
// 2023-08-24T07:35:29+00:00
```

- **OffSetTime** xử lý thời gian(giờ, phút, giây, nanosecond) kèm theo độ lệch múi giờ từ thời gian Greenwich/UTC, không có ID múi giờ.

```java
OffsetTime offsetTime = OffsetTime.now();
System.out.println(offsetTime);
```

```java
// 07:35:29+00:00
```

> Khi nào sử dụng **ZonedDateTime**, **OffsetDateTime**, **OffsetTime** ?

- Ứng dụng cần biết múi giờ của một ngày và thời gian. Trong trường hợp này, ta sẽ sử dụng hàm **ZonedDateTime**.
- Ứng dụng cần biết độ lệch múi giờ của một ngày và thời gian, nhưng không cần biết múi giờ cụ thể. Trong trường hợp này, ta sẽ sử dụng hàm **OffsetDateTime**.
- Ứng dụng cần biết thời gian của một ngày, nhưng không cần biết múi giờ. Trong trường hợp này, ta sẽ sử dụng hàm **OffsetTime**.

## 6. Instant Class [InstClass]

```java
import java.time.Instant;

Instant timestamp = Instant.now();
```

- Lớp cốt lõi trong API Date-Time là Class Instant, đại diện cho thời điểm bắt đầu một nanosecond trên dòng thời gian (time-line).
- Lớp Instant không liên quan đến múi giờ.
- Một giá trị trả về lớp **INSTANT** đến từ thời gian bắt đầu từ ngày đầu tiên của **ngày 1 tháng 1 năm 1970 (1970-01-01T00:00:00Z)**, còn được gọi là **EPOCH**.

```java
public static final Instant EPOCH
// Constant for the 1970-01-01T00:00:00Z epoch instant.
```

- Các hằng số khác được cung cấp bởi lớp Instant là **MIN**, đại diện cho khoảnh khắc nhỏ nhất có thể (rất xa về quá khứ), và **MAX** đại diện cho khoảnh khắc lớn nhất (rất xa về tương lai).

```java
public static final Instant MAX
// Khoảng tối đa Instant hỗ trợ: '1000000000-12-31T23:59:59.999999999Z'.

public static final Instant MIN
// Khoảng tối thiểu Instant hỗ trợ: '-1000000000-01-01T00:00Z'.
```

```java
import java.time.Instant;

public class Main {

    public static void main(String[] args) {
        Instant timestamp = Instant.now();

        //1. Trừ một giờ từ timestamp
        Instant minusOneHour = timestamp.minus(1, ChronoUnit.HOURS);
        System.out.println(minusOneHour);

        // 2023-03-09T15:00:00Z

        //2. Cộng một giờ vào timestamp
        Instant plusOneHour = timestamp.plus(1, ChronoUnit.HOURS);
        System.out.println(plusOneHour);

        // 2023-03-09T16:00:00Z

        //3. Kiểm tra xem timestamp đầu tiên có sau timestamp thứ hai hay không
        boolean isAfter = timestamp.isAfter(minusOneHour);
        System.out.println(isAfter);

        // true

        //4. Kiểm tra xem timestamp đầu tiên có trước timestamp thứ hai hay không
        boolean isBefore = timestamp.isBefore(plusOneHour);
        System.out.println(isBefore);

        // false

        //5. Chuyển đổi timestamp thành số mili giây kể từ Epoch
        long epochMilli = timestamp.toEpochMilli();
        System.out.println(epochMilli);

        // 1647608000000L

        //6. Tạo một đối tượng Instant từ số mili giây kể từ Epoch
        Instant timestampFromEpochMilli = Instant.fromEpochMilli(epochMilli);
        System.out.println(timestampFromEpochMilli);

        // 2023-03-09T16:00:00Z
    }
}
```

```java
// Output:
1. 2023-03-09T15:00:00Z
2. 2023-03-09T16:00:00Z
3. true
4. false
5. 1647608000000L
6. 2023-03-09T16:00:00Z
```

3. Chuyển đổi INSTANT thành các class khác để thực hiện múi giờ

Instant không chứa thông tin về múi giờ. Nếu muốn thực hiện tính toán các đơn vị thời gian như ngày, tháng, năm thì cần chuyển đổi INSTANT sang một lớp khác như việc chuyển qua LocalDAteTime hay là ZoneDateTime.

> Chuyển đổi INSTANT qua **LocalDateTime**

Ta phải thực hiện phương thức **ofInstant()** có chứa 2 tham số là: Đối tượng Instant và múi giờ.

```java
ofInstant(Instant Object, Zone ID);
```

```java
Instant timestamp = Instant.now();
LocalDateTime localDateTime = LocalDateTime.ofInstant(timestamp, ZoneId.systemDefault());
```

=> Đoạn mã trên sẽ chuyển đổi timestamp thành LocalDateTime tại múi giờ hiện tại được truyền tham số vào. Sau khi chuyển đổi sang LocalDateTime thì ta có thể dùng các phương thức GETTER như là:

- getYear(), getMonth(), getDayOfMonth(), getHour(), getMinute(), getSecond(), getNano()

> Chuyển đổi Instant sang **ZoneDateTime**

Ta vẫn sử dụng các phương thức ofInstant(). Phương thức này cũng có 2 tham số: Đối tượng INSTANT và múi giờ.

```java
Instant timestamp = Instant.now();
ZonedDateTime zonedDateTime = ZonedDateTime.ofInstant(timestamp, ZoneId.systemDefault());
```

Đoạn code sẽ chuyển đổi timestamp thành **ZonedDateTime**. Và ta có thể gọi các **method GETTER** của ZonedDateTime để sử dụng, và sử dụng các thuộc tính như:

- getYear(), getMonth(), getDayOfMonth(), getHour(), getMinute(), getSecond(), getNano(), getZone() và getOffset().

> Lưu ý rằng quá trình chuyển đổi ngược không đúng. Điều này có nghĩa là ta không thể chuyển đổi một **LocalDateTime** hoặc **ZonedDateTime** thành **Instant** nếu bạn không biết múi giờ. Nếu bạn không biết múi giờ, bạn cần chuyển đổi **LocalDateTime** hoặc **ZonedDateTime** thành một định dạng thời gian có múi giờ, chẳng hạn như **OffsetDateTime** hoặc **ZonedDateTime**.

## 7. Parsing and Formatting

Trong DateTimeFormatter của API Date-Time trong JAVA thì có 2 phương thức là
PARSE và FORMATTING

1. **Parse**
   Phương thức parse(CharSequence)có một đối số trong lớp LocalDate sử dụng một bộ định dạng ISO_LOCAL_DATE. Để chỉ định một định dạng khác, ta có thể sử dụng phương thức PARSE với 2 đối số (arg).

```java
parse(CharSequence, DateTimeFormatter)
```

> VD: Định dạng ofPattern() trong DateTimeFormatter được định nghĩa sẵn và dùng định dạng MMM d yyyy

```java
String in = "Jan 03 2003";
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MMM d yyyy");
LocalDate date = LocalDate.parse(in, formatter);
System.out.printf("%s%n", date);
```

```diff
---> Output: 01-03-2003
```

> Ví dụ dưới đây sử dụng bộ định dạng **BASIC_ISO_DATE** được định nghĩa sẵn, sử dụng định dạng 19750430 cho ngày 30 tháng 04 năm 1975.

```java
String in = "19750430";
LocalDate date = LocalDate.parse(in, DateTimeFormatter.BASIC_ISO_DATE);
```

```diff
---> Output: 1975-04-30
```

> Phương thức parse(CharSequence) trong lớp DateTimeFormatter được sử dụng để phân tích một chuỗi chứa thông tin về ngày và giờ. Trong trường hợp này, chuỗi in có định dạng 19750430, là định dạng ISO 8601 cho ngày 30 tháng 04 năm 1975. Phương thức parse() sẽ phân tích chuỗi này và tạo ra một đối tượng LocalDate đại diện cho ngày đó.

2. **Formatting**

   Phương thức **format(DateTimeFormatter)** chuyển đổi một đối tượng dựa trên thời gian trở thành một buổi biểu diễn chuỗi bằng cách sử dụng các định dạng đã chỉ định.

```java
ZoneId leavingZone = ZoneId.of("America/Los_Angeles");
ZonedDateTime departure = ZonedDateTime.of(2013, 7, 20, 19, 30, 0, 0, leavingZone);

try {
DateTimeFormatter format = DateTimeFormatter.ofPattern("MMM d yyyy hh:mm a");
String out = departure.format(format);
System.out.printf("LEAVING: %s (%s)%n", out, leavingZone);
}
catch (DateTimeException exc) {
System.out.printf("%s can't be formatted!%n", departure);
throw exc;
}
```

```diff
---> LEAVING: Jul 20 2013 07:30 PM (America/Los_Angeles)
```

1. Đoạn code trên tạo một đối tượng ZoneId đại diện cho múi giờ của nơi khởi hành

2. Một đối tượng ZoneDateTime đại diện cho thời gian khởi hành, sử dụng múi giờ của nơi khởi hành

3. Tạo một đối tượng DateTimeFormatter có định dạng 'MMMM d yyyy hh:mm a'

4. Định dạng đối tượng ZoneDateTime thành một chuỗi bằng cách sử dụng đối tượgn DateTimeFormatter.

## 8. The Temporal Package

Temporal Package gọi là gói thời gian cung cấp INTERFACE , Enum và các mã nguồn hỗ trợ liên quan đến ngày và thời gian, tính toán ngày và thời gian để tính toán.

Các Interface được dùng ở mức thấp nhất (lowest key).

```java
import java.time.temporal

public interface TemporalAccessor {}
```

1. Interface Temporal cung cấp framework cho việc hoạt động và truy cập các đối tượng dựa vào thời gian và luôn được triển khai [implements] thông qua các lớp dựa trên thời gian, như là INSTANT, LocalDateTime và ZoneDateTime

2. Interface Temporal cung cấp các phương thức cộng trừ thêm bớt các đơn vị thời gian như ngày, các giờ khác nhau.

3. Interface TemporalAccessor cung cấp một phiên bản chỉ đọc (read-only version of the Temporal interface.) của Interface Temporal.

> Điều này có nghĩa là cung cấp các phương thức để truy cập các giá trị của đối tượng TEMPORAL, nhưng không cung cấp bất kỳ phương thức nào để thay đổi nó.

```java
get(TemporalField field)
// Gets the value of the specified field as an int.
getLong(TemporalField field)
// Gets the value of the specified field as a long.
isSupported(TemporalField field)
// Checks if the specified field is supported.
query(TemporalQuery<R> query)
// Queries this date-time.
range(TemporalField field)
// Gets the range of valid values for the specified field.
```

4. Temporal && TemporalAccessor đều được định nghĩa dưới dạng các Field (trường dữ liệu).

#### **Enum ChronoField**

1. Enum triển khai giao diện TemporalField , cung cấp các lượng lớn hằng số để truy cập các giá trị ngày và giờ. Các hằng số này miêu tả các khái niệm của thời gian rõ ràng hơn.

> ChronoField định nghĩa các trường thời gian tiêu chuẩn

```Java
// Enum Constants(hằng số)

ALIGNED_DAY_OF_WEEK_IN_MONTH
// The aligned day-of-week within a month.
ALIGNED_DAY_OF_WEEK_IN_YEAR
// The aligned day-of-week within a year.
ALIGNED_WEEK_OF_MONTH
// The aligned week within a month.
ALIGNED_WEEK_OF_YEAR
// The aligned week within a year.
AMPM_OF_DAY
// The am-pm-of-day.
CLOCK_HOUR_OF_AMPM
// The clock-hour-of-am-pm.
CLOCK_HOUR_OF_DAY
// The clock-hour-of-day.
DAY_OF_MONTH
// The day-of-month.
DAY_OF_WEEK
// The day-of-week, such as Tuesday.
DAY_OF_YEAR
// The day-of-year.
EPOCH_DAY
// The epoch-day, based on the Java epoch of 1970-01-01 (ISO).
ERA
// The era.
HOUR_OF_AMPM
// The hour-of-am-pm.
HOUR_OF_DAY
// The hour-of-day.
INSTANT_SECONDS
// The instant epoch-seconds.
MICRO_OF_DAY
// The micro-of-day.
MICRO_OF_SECOND
// The micro-of-second.
MILLI_OF_DAY
// The milli-of-day.
MILLI_OF_SECOND
// The milli-of-second.
MINUTE_OF_DAY
// The minute-of-day.
MINUTE_OF_HOUR
// The minute-of-hour.
MONTH_OF_YEAR
// The month-of-year, such as March.
NANO_OF_DAY
// The nano-of-day.
NANO_OF_SECOND
// The nano-of-second.
OFFSET_SECONDS
// The offset from UTC/Greenwich.
PROLEPTIC_MONTH
// The proleptic-month based, counting months sequentially from year 0.
SECOND_OF_DAY
// The second-of-day.
SECOND_OF_MINUTE
//The second-of-minute.
YEAR
//The proleptic year, such as 2012.
YEAR_OF_ERA
//The year within the era.
```

- Ví dụ về ENUM

```java
LocalDate date = LocalDate.now();
int dayOfMonth = date.get(ChronoField.DAY_OF_MONTH);
System.out.println(dayOfMonth);
```

```java
// VD: hôm nay là ngày 25 tháng 07 2023
// Output: 25
```

#### **IsoFields**

1. IsoFields là một Enum định nghĩa các trường ISO-8601 khác nhau. Các trường (field) này được sử dụng để truy cập các giá trị của đối tượng Temporal.

> IsoField định nghĩa các trường thời gian

```java
DAY_OF_QUARTER
// là một trường xác định ngày trong quý. Giá trị của trường này có thể là từ 1 đến 90, 91 hoặc 92.

QUARTER_OF_YEAR
// là một trường xác định quý trong năm dựa trên tuần. Giá trị của trường này có thể là từ 1 đến 4.

YEAR
// là một trường xác định năm ISO tiêu chuẩn. Giá trị của trường này có thể là bất kỳ năm nào.

YEAR_OF_WEEK
// là một trường xác định năm dựa trên tuần. Giá trị của trường này có thể là bất kỳ năm nào.

WEEK_OF_WEEK_BASED_YEAR
// là một trường xác định tuần trong năm dựa trên tuần. Giá trị của trường này có thể là từ 1 đến 52 hoặc 53.

WEEK_BASED_YEAR
// là một trường xác định năm dựa trên tuần. Giá trị của trường này có thể là bất kỳ năm nào.
```

- Tuần đầu tiên của năm dựa trên tuần là tuần đầu tiên dựa trên thứ Hai của năm ISO tiêu chuẩn có ít nhất 4 ngày trong năm mới.

1. Nếu ngày 1 tháng 1 là Thứ Hai thì tuần 1 bắt đầu từ ngày 1 tháng 1
2. Nếu ngày 1 tháng 1 là Thứ Ba thì tuần 1 bắt đầu từ ngày 31 tháng 12 của năm tiêu chuẩn trước đó
3. Nếu ngày 1 tháng 1 là Thứ Tư thì tuần 1 bắt đầu từ ngày 30 tháng 12 của năm tiêu chuẩn trước đó
4. Nếu ngày 1 tháng 1 là Thứ Năm thì tuần 1 bắt đầu từ ngày 29 tháng 12 của năm tiêu chuẩn trước đó
5. Nếu ngày 1 tháng 1 là Thứ Sáu thì tuần 1 bắt đầu từ ngày 4 tháng 1
6. Nếu ngày 1 tháng 1 là Thứ Bảy thì tuần 1 bắt đầu từ ngày 3 tháng 1
7. Nếu ngày 1 tháng 1 là Chủ Nhật thì tuần 1 bắt đầu từ ngày 2 tháng 1

- Hầu hết các năm dựa trên tuần có 52 tuần, tuy nhiên đôi khi có 53 tuần.

```java
LocalDate date = LocalDate.now();

int dayOfMonth = date.get(ChronoField.DAY_OF_MONTH);
int monthOfYear = date.get(ChronoField.MONTH_OF_YEAR);
int year = date.get(ChronoField.YEAR);

System.out.println("Day of month: " + dayOfMonth);
System.out.println("Month of year: " + monthOfYear);
System.out.println("Year: " + year);
```

```java
Day of month: 23
Month of year: 8
Year: 2023
```

#### **ChronoUnit**

- **ChronoUnit** định nghĩa các đơn vị thời gian bằng các HẰNG SỐ. ChronoUnits là các Enum và có thể tính toán các khoảng thời gian với nhau.

> ChronoUnit khác ChornoFields

```java
CENTURIES
  // Đơn vị đại diện cho khái niệm một thế kỷ.
DAYS
  // Đơn vị đại diện cho khái niệm một ngày.
DECADES
  // Đơn vị đại diện cho khái niệm một thập kỷ.
ERAS
  // Đơn vị đại diện cho khái niệm một thời đại.
FOREVER
  // Đơn vị nhân tạo đại diện cho khái niệm mãi mãi.
HALF_DAYS
  // Đơn vị đại diện cho khái niệm một nửa ngày, được sử dụng trong AM/PM.
HOURS
  // Đơn vị đại diện cho khái niệm một giờ.
MICROS
  // Đơn vị đại diện cho khái niệm một micro giây.
MILLENNIA
  // Đơn vị đại diện cho khái niệm một thiên niên kỷ.
MILLIS
  // Đơn vị đại diện cho khái niệm một mili giây.
MINUTES
  //Đơn vị đại diện cho khái niệm một phút.
MONTHS
  //Đơn vị đại diện cho khái niệm một tháng.
NANOS
  //Đơn vị đại diện cho khái niệm một nano giây, đơn vị thời gian nhỏ nhất được hỗ trợ.
SECONDS
  // Đơn vị đại diện cho khái niệm một giây.
WEEKS
  //Đơn vị đại diện cho khái niệm một tuần.
YEARS
  //Đơn vị đại diện cho khái niệm một năm.
```

- Ví dụ về ChronoUnit

```java
LocalDate start = LocalDate.of(2023, 8, 1);
LocalDate end = LocalDate.of(2023, 8, 23);

long days = ChronoUnit.DAYS.between(start, end);

System.out.println(days);
```

```java
//Output: 22
```

#### 8.1 **Temporal Adjuster**

1. **Adjuster** là công cụ quan trọng để thay đổi các đối tượng thời gian. Chúng tồn tại để bên ngoài quá trình điều chỉnh, cho phép các phương pháp khác nhau, theo mẫu thiết kế chiến lược. Ví dụ có thể là adjuster thiết lập ngày tránh cuối tuần, hoặc thiết lập ngày cuối cùng của tháng.

2. Có hai cách tương đương để sử dụng TemporalAdjuster. Cách thứ nhất là gọi phương thức trực tiếp trên giao diện này.

   Cách thứ hai là sử dụng Temporal.with(TemporalAdjuster):

   Hai dòng mã này tương đương nhau, nhưng cách tiếp cận thứ hai được đề xuất

```java
 temporal = thisAdjuster.adjustInto(temporal);
 temporal = temporal.with(thisAdjuster);
```

Nên sử dụng cách thứ 2, với (TemporalAdjuster), vì nó dễ đọc hơn rất nhiều trong mã.

Lớp TemporalAdjusters chứa một tập hợp tiêu chuẩn của các adjuster, có sẵn như các phương thức tĩnh.

Các ví dụ bao gồm:

- Tìm ngày đầu tiên hoặc cuối cùng của tháng
- Tìm ngày đầu tiên của tháng kế tiếp
- Tìm ngày đầu tiên hoặc cuối cùng của năm
- Tìm ngày đầu tiên của năm kế tiếp
- Tìm ngày đầu tiên hoặc cuối cùng của tuần trong một tháng, chẳng hạn như "Thứ Tư đầu tiên trong tháng Sáu"
- Tìm ngày-of-week tiếp theo hoặc trước đó, chẳng hạn như "Thứ Năm kế tiếp"

> Enum TemporalAdjuster

```java
dayOfWeekInMonth(int ordinal, DayOfWeek dayOfWeek)
// Trả về bộ điều chỉnh ngày trong tuần trong tháng, tạo ra một ngày mới trong cùng tháng với ngày trong tuần ở vị trí xác định.

firstDayOfMonth()
// Trả về bộ điều chỉnh "ngày đầu tiên của tháng", tạo ra một ngày mới được đặt vào ngày đầu tiên của tháng hiện tại.

firstDayOfNextMonth()
// Trả về bộ điều chỉnh "ngày đầu tiên của tháng sau", tạo ra một ngày mới được đặt vào ngày đầu tiên của tháng sau.

firstDayOfNextYear()
// Trả về bộ điều chỉnh "ngày đầu tiên của năm sau", tạo ra một ngày mới được đặt vào ngày đầu tiên của năm sau.

firstDayOfYear()
// Trả về bộ điều chỉnh "ngày đầu tiên của năm", tạo ra một ngày mới được đặt vào ngày đầu tiên của năm hiện tại.

firstInMonth(DayOfWeek dayOfWeek)
// Trả về bộ điều chỉnh đầu tiên trong tháng, tạo ra một ngày mới trong cùng tháng với ngày trong tuần khớp đầu tiên.

lastDayOfMonth()
// Trả về bộ điều chỉnh "ngày cuối cùng của tháng", tạo ra một ngày mới được đặt vào ngày cuối cùng của tháng hiện tại.

lastDayOfYear()
// Trả về bộ điều chỉnh "ngày cuối cùng của năm", tạo ra một ngày mới được đặt vào ngày cuối cùng của năm hiện tại.

lastInMonth(DayOfWeek dayOfWeek)
// Trả về bộ điều chỉnh cuối cùng trong tháng, tạo ra một ngày mới trong cùng tháng với ngày trong tuần khớp cuối cùng.

next(DayOfWeek dayOfWeek)
// Trả về bộ điều chỉnh ngày trong tuần tiếp theo, điều chỉnh ngày đến ngày đầu tiên của ngày trong tuần được xác định sau ngày đang được điều chỉnh.

nextOrSame(DayOfWeek dayOfWeek)
// Trả về bộ điều chỉnh ngày trong tuần kế tiếp hoặc giống nhau, điều chỉnh ngày đến ngày đầu tiên của ngày trong tuần được xác định sau ngày đang được điều chỉnh, trừ khi nó đã ở trên ngày đó, trong trường hợp đó, đối tượng giống như ban đầu được trả về.

ofDateAdjuster(UnaryOperator<LocalDate> dateBasedAdjuster)
// Lấy một bộ điều chỉnh thời gian (TemporalAdjuster) bao bọc bởi bộ điều chỉnh ngày.

previous(DayOfWeek dayOfWeek)
// Trả về bộ điều chỉnh ngày trong tuần trước đó, điều chỉnh ngày đến ngày đầu tiên của ngày trong tuần được xác định trước ngày đang được điều chỉnh.

previousOrSame(DayOfWeek dayOfWeek)
// Trả về bộ điều chỉnh ngày trong tuần trước hoặc giống như cùng, điều chỉnh ngày đến ngày đầu tiên của ngày trong tuần được xác định trước ngày đang được điều chỉnh, trừ khi nó đã ở trên ngày đó, trong trường hợp đó, đối tượng giống như ban đầu được trả về.

```

#### 8.2 **Temporal Query**

1. Predefined Queries - Truy vấn định sẵn

Lớp TemporalQueries cung cấp một số query (truy vấn) được định sẵn (several predefined queries), bao gồm nhiều phương thức hữu ích khi sử dụng, không thể xác định loại đối tượng dựa trên thời gian. Tương tự các bộ điều chỉnh (adjusters), các truy vấn được định sẵn được sử dụng như một câu lệnh tĩnh (input static).

```java
import java.time.LocalDate;
import java.time.temporal.TemporalQueries;
import java.time.temporal.TemporalQuery;
import java.time.temporal.ChronoUnit;

public class PredefinedTemporalQueriesExample {
    public static void main(String[] args) {
        LocalDate date = LocalDate.of(2023, 8, 20);

        // Sử dụng truy vấn precision để xác định đơn vị ChronoUnit nhỏ nhất
        ChronoUnit smallestUnit = date.query(TemporalQueries.precision());
        System.out.println("Smallest precision unit: " + smallestUnit);

        // Sử dụng truy vấn local date để trích xuất LocalDate từ LocalDateTime
        LocalDate extractedDate = date.atTime(15, 30).query(TemporalQueries.localDate());
        System.out.println("Extracted LocalDate: " + extractedDate);
    }
}
```

```
Smallest precision unit: Days
Extracted LocalDate: 2023-08-20
```

2. Custom Queries - Truy vấn tuỳ chỉnh

Ta có thể tuỳ chỉnh, tuỳ ý tạo một lớp truy vấn của riêng mình. Bằng cách tạo một lớp thực thi INTERFACE TemporalQuery với phương thức queryFrom (TemporalAccessor).

```java
import java.time.LocalDate;
import java.time.Month;
import java.time.temporal.TemporalAccessor;
import java.time.temporal.TemporalQuery;

public class CustomTemporalQueryExample {
    public static void main(String[] args) {
        LocalDate currentDate = LocalDate.of(2023, Month.AUGUST, 20);

        // Tạo một truy vấn tùy chỉnh để kiểm tra xem ngày có phải là ngày nghỉ hay không
        TemporalQuery<Boolean> vacationQuery = new VacationCheckQuery();

        // Kiểm tra xem ngày hiện tại có phải là ngày nghỉ hay không
        boolean isVacationDay = currentDate.query(vacationQuery);
        System.out.println("Is it a vacation day? " + isVacationDay);
    }
}

class VacationCheckQuery implements TemporalQuery<Boolean> {
    @Override
    public Boolean queryFrom(TemporalAccessor temporal) {
        int month = temporal.get(java.time.temporal.ChronoField.MONTH_OF_YEAR);
        int dayOfMonth = temporal.get(java.time.temporal.ChronoField.DAY_OF_MONTH);

        // Giả sử ngày nghỉ là tháng 8 và ngày 20
        return (month == 8 && dayOfMonth == 20);
    }
}
```

```OUTPUT
Is it a vacation day? true
```

## 9.Period & Duration [Period&Duration]

- **Period** đại diện cho khoảng thời gian nhưng bằng các đơn vị dựa trên ngày,tháng năm
- **Duration** đại diện cho khoảng thời gian nhưng lại khác với Period, bằng các đơn vvị như giờ, phút, giây

| Tính năng        | Period                                            | Duration                    |
| :--------------- | :------------------------------------------------ | --------------------------- |
| Đơn vị thời gian | Năm Tháng Ngày                                    | Giờ phút giây               |
|                  | YYYY:mm:dd                                        | HH:mm:ss                    |
| Độ chính xác     | Có thể không chính xác do khác biệt múi giờ       | Chính xác                   |
| Phạm vi          | Đại diện cho thời gian dài                        | Cho khoảng thời gian ngắn   |
| Ví dụ sử dụng    | Tuổi tác, thời gian làm việc, thời gian nghỉ phép | Phạm vi thực thi một tác vụ |

> Phân đoạn thời gian bằng KeyWord <PT#H>

- P is the _duration_ designator (for **period**) placed at the start of the duration representation.
  - Y is the **_year_** designator that follows the value for the number of calendar years.
  - M is the **_month_** designator that follows the value for the number of calendar months.
  - W is the **_*week*_** designator that follows the value for the number of weeks.
  - D is the **_*day*_** designator that follows the value for the number of calendar days.
- T is the **_*time*_** designator that precedes the time components of the representation.

  - H is the **_*hour*_** designator that follows the value for the number of hours.
  - M is the **_*minute*_** designator that follows the value for the number of minutes.
  - S is the **_*second*_** designator that follows the value for the number of seconds.

- PERIOD: tính toán tuổi 1 người

```java
import java.time.LocalDate;
import java.time.Period;

public class AgeCalculator {

    public static void main(String[] args) {
        LocalDate birthDate = LocalDate.of(1980, 1, 1);
        LocalDate today = LocalDate.now();

        Period period = Period.between(birthDate, today);
        int years = period.getYears();
        int months = period.getMonths();
        int days = period.getDays();

        System.out.println("Bạn đã " + years + " tuổi, " + months + " tháng và " + days + " ngày.");
    }
}
```

```java
Bạn đã 43 tuổi, 1 tháng và 22 ngày.
```

- DURATION: Tính toán khoảng thực thi một tác vụ

```java
import java.time.Instant;
import java.time.Duration;

public class TaskTimer {

    public static void main(String[] args) {
        Instant start = Instant.now();

        // Thực hiện tác vụ

        Instant end = Instant.now();

        Duration duration = Duration.between(start, end);

        System.out.println("Tác vụ đã thực thi trong " + duration.toMillis() + " mili giây.");
    }
}
```

```java
Tác vụ đã thực thi trong 1000 mili giây.
```

@@ END

```markdown
Dang Dai 'Ocean' Dang © 2023
Topic: Data-Time API Java
✆ 0966 614 097
✉️ oceanwork2820@gmail.com
```
