# system-analysis-and-design

## DFD LEVEL 0
```mermaid
flowchart LR
    %% External Entities
    Citizen([شهروندان / تماس‌گیرندگان])
    Municipality([شهرداری تبریز])
    Court([مراجع قضایی])
    Contractors([پیمانکاران و شرکتهای تجهیزات])
    Services([سازمان‌های خدمات شهری<br>اورژانس، پلیس، گاز، برق])
    Ministry([وزارت کشور])

    %% Main Process
    FireDept((سازمان آتش‌نشانی تبریز))

    %% Data Flows
    Citizen -->|گزارش حادثه / درخواست ایمنی| FireDept
    FireDept -->|اعزام نیرو، پاسخ‌دهی، نتیجه عملیات| Citizen

    Municipality -->|بودجه، مصوبات، ابلاغیه‌ها| FireDept
    FireDept -->|گزارش عملکرد / گزارش آماری| Municipality

    Court -->|استعلام علت حادثه| FireDept
    FireDept -->|گزارش کارشناسی علل حریق| Court

    Contractors -->|تجهیزات / قراردادها| FireDept
    FireDept -->|درخواست خرید، اسناد قرارداد| Contractors

    Services -->|هماهنگی عملیاتی| FireDept
    FireDept -->|اطلاع‌رسانی و درخواست پشتیبانی| Services

    Ministry -->|بخشنامه‌ها / مقررات ملی| FireDept
    FireDept -->|آمار و گزارش کشوری| Ministry
```
