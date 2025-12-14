# system analysis and design

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
---
---

## DFD LEVEL 1

```mermaid
flowchart LR

    %% External Entities
    Citizen([شهروندان / تماس‌گیرندگان])
    Municipality([شهرداری تبریز])
    Court([مراجع قضایی])
    Suppliers([پیمانکاران / تامین‌کنندگان])
    Services([اورژانس / پلیس / گاز / برق])
    Ministry([وزارت کشور])
    Insurance([شرکت‌های بیمه])

    %% Main Organization Process
    subgraph FireDept[سازمان آتش‌نشانی تبریز]

        %% معاونت عملیات
        subgraph Op[1. معاونت عملیات]
            OpA[دریافت گزارش حادثه]
            OpB[اعزام نیرو]
            OpC[ثبت و گزارش عملیات]
        end

        %% معاونت پیشگیری
        subgraph Prev[2. معاونت پیشگیری]
            PrevA[بررسی ایمنی و نقشه‌ها]
            PrevB[بازدید و صدور گواهی]
            PrevC[علل حریق و کارشناسی]
        end

        %% معاونت مالی
        subgraph Fin[3. معاونت مالی و اقتصادی]
            FinA[اسناد مالی و حسابداری]
            FinB[تدارکات و خرید]
            FinC[درآمد و اقتصادی]
        end

        %% معاونت برنامه‌ریزی و منابع انسانی
        subgraph HR[4. برنامه‌ریزی و توسعه سرمایه انسانی]
            HR1[آموزش]
            HR2[منابع انسانی]
            HR3[فناوری اطلاعات و پروژه‌ها]
        end

        %% اداره حقوقی
        subgraph Legal[5. اداره حقوقی و امور پیمان‌ها]
            L1[بررسی حقوقی]
            L2[قراردادها]
        end

        %% حراست
        subgraph Sec[6. اداره حراست]
            S1[نظارت و کنترل امنیتی]
        end

        %% ایستگاه‌ها
        subgraph Stations[7. ایستگاه‌های عملیاتی]
            ST1[گزارش عملیات]
            ST2[نیروهای عملیاتی]
        end

    end


    %% ==== DATA FLOWS ====

    Citizen -->|گزارش حادثه 125| OpA
    OpB -->|اعزام نیرو| Stations
    Stations -->|گزارش عملیات| OpC
    OpC -->|گزارش عملکرد| Municipality

    PrevA -->|تأیید/عدم‌تأیید نقشه| Citizen
    Citizen -->|درخواست گواهی ایمنی| PrevB
    PrevC -->|گزارش کارشناسی حادثه| Court

    Municipality -->|بودجه / مصوبات| FinA
    FinC -->|گزارش درآمد| Municipality

    Suppliers -->|پیش‌فاکتور / پیشنهاد قیمت| FinB
    FinB -->|سفارش خرید| Suppliers

    Insurance -->|استعلام خسارت| PrevC
    PrevC -->|گزارش کارشناسی| Insurance

    Ministry -->|بخشنامه / مقررات| HR3
    HR3 -->|گزارش برنامه‌ریزی| Ministry

    UnitsA[معاونت‌ها و ایستگاه‌ها] -->|نیاز نیرو / اطلاعات پرسنلی| HR2

    Legal -->|پیگیری دعاوی| Court
    Court -->|دادخواست / مکاتبه| Legal

    S1 -->|گزارش نظارتی| FireDept
```
---
---

## DFD Level 1 معاونت امور مالی

```mermaid
flowchart LR

    %% External Entities
    Municipality([شهرداری / واحد مالی شهرداری])
    Suppliers([پیمانکاران / تامین‌کنندگان])
    Units([سایر معاونت‌ها و واحدهای سازمان])
    Warehouse([انبار مرکزی / اموال])

    %% Main Process
    subgraph FinanceDept[معاونت مالی و اقتصادی]
        
        subgraph A1[1. اداره مالی و حسابداری]
            A1a[ثبت اسناد مالی]
            A1b[حسابداری و حقوق]
            A1c[کنترل اموال و انبار]
        end

        subgraph A2[2. اداره درآمد و اقتصادی]
            A2a[ثبت درآمدها]
            A2b[گزارش درآمد به شهرداری]
        end

        subgraph A3[3. اداره تدارکات و کارپردازی]
            A3a[دریافت درخواست خرید]
            A3b[استعلام قیمت]
            A3c[صدور سفارش خرید]
        end

        subgraph A4[4. نگهداری و تعمیرات تجهیزات]
            A4a[ثبت درخواست تعمیر]
            A4b[برآورد هزینه تعمیر]
        end

    end

    %% Data Flows

    Units -->|درخواست خرید / درخواست هزینه| A3a
    Units -->|درخواست تعمیر تجهیزات| A4a

    A3b -->|استعلام قیمت| Suppliers
    Suppliers -->|پیشنهاد قیمت / پیش‌فاکتور| A3b

    A3c -->|سفارش خرید| Suppliers
    Suppliers -->|تحویل کالا| Warehouse

    Warehouse -->|تأیید دریافت کالا| A3c
    Warehouse -->|اطلاعات اموال| A1c

    Municipality -->|بودجه مصوب / تخصیص اعتبار| A1a
    A2b -->|گزارش درآمد| Municipality

    A1a -->|اسناد مالی| A2a
    A1b -->|پرداخت حقوق و هزینه‌ها| Units

    A4b -->|هزینه تعمیر| A1a
    A4b -->|اطلاع وضعیت تجهیزات| Units
```

---
---

## DFD Level 1 معاونت عملیات

```mermaid
flowchart LR
%% External entities
Citizen(["شهروند / تماس‌گیرنده ۱۲۵"])
Services(["اورژانس / پلیس / گاز / برق"])
Municipality(["شهرداری / واحد مدیریتی"])
Suppliers(["پیمانکاران / تعمیرات"])
Court(["مراجع قضایی / بیمه"])
%% Data stores
D1[["پرونده حوادث / Incident Records"]]
D2[["فهرست پرسنل و شیفت‌ها"]]
D3[["موجودی تجهیزات و آمادگی"]]
D4[["نقشه‌ها و اطلاعات ساختمان‌ها"]]
D5[["گزارشات عملکرد و آمار"]]
%% Operations sub-processes
subgraph Ops["معاونت عملیات"]
P1["1. دریافت و ثبت گزارش حادثه"]
P2["2. ارزیابی و اعزام (مرکز فرماندهی / Dispatch)"]
P3["3. اعزام و هدایت عملیات میدانی"]
P4["4. مدیریت ایستگاه‌ها و شیفت‌ها"]
P5["5. پشتیبانی تدارکاتی و نگهداری تجهیزات"]
P6["6. ثبت نهایی و گزارش‌دهی"]
end
%% Flows between external entities and processes
Citizen -->|"گزارش حادثه / جزئیات"| P1
P1 -->|"ثبت اولیه"| D1
P1 -->|"اطلاعات برای ارزیابی"| P2
P2 -->|"دستور اعزام (واحد/وسایل)"| P3
P2 -->|"درخواست هماهنگی"| Services
Services -->|"پاسخ هماهنگی"| P3
P3 -->|"درخواست تجهیزات/قطعات"| P5
P5 -->|"درخواست ارسال / پیش‌فاکتور"| Suppliers
Suppliers -->|"ارسال/تأیید"| P5
P3 -->|"گزارش میدانی (لحظه‌ای)"| D1
P3 -->|"اطلاع‌رسانی وضعیت"| P4
P4 -->|"به‌روزرسانی شیفت / نفرات"| D2
D2 -->|"اطلاعات شیفت"| P4
P5 -->|"وضعیت آماده‌باش تجهیزات"| D3
D3 -->|"اطلاعات موجودی"| P3
P6 -->|"گزارش نهایی و آمار"| D5
P6 -->|"ارسال گزارش عملکرد"| Municipality
P6 -->|"ارسال گزارش کارشناسی (در صورت نیاز)"| Court
D4 -->|"نقشه/اطلاعات ساختمان"| P2
P3 -->|"ثبت جزئیات حادثه"| D1
```

---
---

## ER DIAGRAM

```mermaid
erDiagram

    ORGANIZATION ||--|| OPERATIONS_DEPUTY : "دارای"
    ORGANIZATION ||--|| PREVENTION_DEPUTY : "دارای"
    ORGANIZATION ||--|| HR_DEVELOPMENT_DEPUTY : "دارای"
    ORGANIZATION ||--|| FINANCIAL_DEPUTY : "دارای"
    ORGANIZATION ||--|| LEGAL_DEPARTMENT : "شامل"
    ORGANIZATION ||--|| SECURITY_DEPARTMENT : "شامل"

    OPERATIONS_DEPUTY ||--|{ FIRE_STATIONS : "مدیریت"
    OPERATIONS_DEPUTY ||--|| COMMUNICATION_CENTER : "زیرمجموعه"

    PREVENTION_DEPUTY ||--|| SAFETY_ENGINEERING_UNIT : "زیرمجموعه"
    PREVENTION_DEPUTY ||--|| FIRE_CAUSE_ANALYSIS_UNIT : "زیرمجموعه"

    HR_DEVELOPMENT_DEPUTY ||--|| TRAINING_UNIT : "شامل"
    HR_DEVELOPMENT_DEPUTY ||--|| HUMAN_RESOURCES_UNIT : "شامل"
    HR_DEVELOPMENT_DEPUTY ||--|| PLANNING_UNIT : "شامل"

    FINANCIAL_DEPUTY ||--|| ACCOUNTING_UNIT : "شامل"
    FINANCIAL_DEPUTY ||--|| PROCUREMENT_UNIT : "شامل"
    FINANCIAL_DEPUTY ||--|| EQUIPMENT_MAINTENANCE_UNIT : "نظارت"

```
