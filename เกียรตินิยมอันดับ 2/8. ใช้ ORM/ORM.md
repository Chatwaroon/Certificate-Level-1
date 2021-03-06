# ORM (Object Relational Mapping) คืออะไร?  
## ORM คืออะไร   
ORM หรือ Object Relational Mapping  ถ้าจะว่าไปมันก็คือการเขียนโปรแกรมอย่างหนึ่ง ไม่ว่าจะเขียนด้วยภาษาโปรแกรมมิ่งอะไรก็ตาม  จุดประสงค์ก็เพื่อแปลงจาก Object ไปเป็น Database หรือแปลงจาก Database กลับมาเป็น Object ครับ   concept มีแค่นี้     

เราไม่จำเป็นต้องยุ่งในส่วนของ SQL (SELECT, INSERT, UPDATE, DELETE) เลย  แต่เราจะใช้ framework มาช่วยจัดการแปลงจากภาษาโปรแกรมมิ่งที่เราเขียน ไปเป็น SQL หรือ database ให้เราแทน  
  
ขอยกตัวอย่างเช่น ภาษา java  ซึ่งก็มี framework ช่วยอยู่หลายตัว  แต่ที่ดังๆ ก็จะมี EclipseLink และ Hibernate   เวลาที่เราต้องการจะสร้าง database table ขึ้นมา table นึง  เราไม่จำเป็นต้องเขียน SQL เพื่อ create table ขึ้นมาเลย  เราแค่เขียน  java class ขึ้นมา  ซึ่ง java class นี้จะถูกเรียกว่า Entity Class จากนั้นก็กำหนด attribute ต่างๆ  ตามที่ต้องการลงไป  attribute นี้เราอาจจะมองว่ามันคือ column ของ table ก็ได้  ทีนี้ framework  มันก็จะเอา  entity class ที่เราเขียนไว้ไปแปลงเป็น table ให้เราเองครับ   
 การ map relation ต่างๆ เช่น One to One, One to Many หรือ Many to May  เราอยากได้แบบไหน  เราก็เขียนลงไปใน  entity class นั้น  framework มันก็จะเอาไป map ให้เราเอง  มันจะสร้าง foreign key, primary key  ซึ่งเป็นความสัมพันธ์ต่างๆ ของ table ให้เองโดยอัตโนมัติ  

 การอ่านค่าจาก table ขึ้นมาใช้   มันก็จะแปลงจากข้อมูลที่อยู่ในรูปของ row ไปเป็น object ของ row นั้นให้  ซึ่งไม่เหมือนกับการเขียน code แบบเดิมๆ  ที่ต้องเขียน code เพื่ออ่านค่ามาจาก database  และก็ค่อยจับค่าที่อ่านมาได้นั้นยัดเข้าไปใน object class เอง  ซึ่งมันก็ค่อนข้างลำบากอยู่เหมือนกันครับ  ถ้าระบบเราเป็นระบบที่ใหญ่มากๆ  การดูแลรักษา  หรือการแก้ไข code ก็จะเกิดความยุ่งยากขึ้นได้  เพราะ code ที่เราเขียนมันผูกกันไปมาเต็มไปหมด  ยิ่งถ้าแก้ attribute ใน table หรือเปลี่ยนแปลงความสัมพันธ์ของ table ที  ก็ต้องมาตามแก้  Class  ที่อ้างไปถึง table นั้นๆ อีก เรียกว่าเหนื่อยกันหลายต่อเลยครับ  

 พอเราหันมาใช้ ORM  มันก็จะช่วยให้งานเราสบายขึ้นเยอะ  เวลาแก้ attribute หรือความสัมพันธ์ใน Entity Class  ตัว attribute หรือความสัมพันธ์ของ table ก็จะเปลี่ยนแปลงตามไปด้วย   เราอาจจะมองว่า entity class กับ database table มันคือตัวเดียวกันก็ได้ครับ  เพราะ framework  มันจะจัดการทำ mapping ให้เรา    

 ## องค์ประกอบที่สำคัญของ ORM ต้องมีคือ  
 - 1.API กลางที่ช่วยทำหน้าที่ในการแปลงข้อมูลระหว่างฐานข้อมูลและ object รวมถึงคำสั่งพื้นฐานของการจัดการข้อมูลไม่ว่าจะเป็นการ Select,Insert,Update,Delete  
 - 2.ภาษาที่ใช้ในการเรียกใช้งานตัว ORM พูดง่าย ๆ คือภาษาที่ใช้ในการคิวรี่ข้อมูลภายใน object  
   
แต่ข้อเสียที่จะเกิดตามมาเมื่อมีการนำ ORM มาใช้งานคือต้องมีการเรียนรู้ถึงภาษาของการคิวรี่ข้อมูลในแต่ละ ORM และต้องเรียนรู้ถึงวิธีการปรับแต่งความสามารถของ ORM เพิ่มเติมเนื่องจากบางครั้งความสามารถพื้นฐานที่ ORM ทำมาให้อาจจะไม่รองรับกับความต้องการที่โปรแกรมเมอร์ต้องการ ซึ่ง ORM ในปัจจุบันที่ได้รับความนิยมเช่น Hibernate, NHibernate, LINQ,SubSonic, Entity Framework, Active Record, Enterprise Library
  






