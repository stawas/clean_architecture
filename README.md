# Flutter Clean architecture

## Description

โครงสร้าง Directory สำหรับ Flutter Clean Architecture

## Structure

- lip
  - core - เก็บ Constants, เก็บ interface ที่ใช้ implement มากกว่า 1 feature เช่น exception interface, failure interface, use case interface
  - features - แยก Feature ในนี้
    - login - 1 Feature
      - data - Data Layer
        - datasources - code ต่อ database, network datasource, Firebase database อยู่ที่นี่
        - models - code แปลงข้อมูลจาก datasource ให้เป็น entity เช่น แปลง json string เป็น user
        - repositories - implement repository interface ใช้เป็นทางเข้าเพื่อให้ domain มาเรียกใช้ (domain ไม่เรียกใช้ datasource โดยตรง) **ไม่ทำ Business Logicที่นี่**
      - domain - Domain Layer ต้องทำงานได้กับทุก library, **การเปลี่ยน library หรือ framework ต้องไม่ส่งผลกับ Domain Layer**
        - entities - หน้าตาของ entity ควรเป็นยังไง กำหนดที่นี่ เช่น User ประกอบด้วย name,age
        - repositories - เขียน interface สำหรับติดต่อ datasource
        - usecases - **code เพื่อทำ business logic (business logic หมายถึง เอา Method หลายๆ ตัว มาเรียกใช้เพื่อให้บรรลุจุดประสงค์ตาม requirement)** เพื่อเรียกใช้ repository ที่ implement แล้ว(อยู่ data) เพื่อทำคำสั่งที่ต้องการ เช่น เรียกข้อมูลจาก datasource โดยแยก usecase เป็นเรื่อง ๆ ไป
      - presentation - Presentation Layer, Bloc, ViewModel, ViewController เรียกใช้ usecase จากที่นี่
        - pages - UI แต่ละหน้า เช่น Login, Home, Setting
        - widgets - เก็บ widget component เพื่อ reuse ใน UI แต่ละหน้า ที่นี่
    - setting - โครงสร้างด้านในเหมือน login
  - l10n - เก็บภาษาของ App เช่น ภาษาไทย ภาษาอังกฤษ
  - res - Color, Theme, Font
  - util - common function เก็บ function ที่ใช้บ่อย ๆ
  - test - ใช้ test
    - fixtures - mock json ที่นี่
- assets - image

## Resources

- [Generate Dart File from Json Online](https://app.quicktype.io/?l=dart)

- [Flutter Clean Architecture Series](https://devmuaz.medium.com/flutter-clean-architecture-series-part-1-d2d4c2e75c47)

- [What is the difference between repositories and usecases?](https://stackoverflow.com/questions/43055247/what-is-the-difference-between-repositories-and-usecases)

- [Error Handling](https://levelup.gitconnected.com/error-handling-in-clean-architecture-9ff159a25d4a)