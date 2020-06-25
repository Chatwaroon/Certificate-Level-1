# JavaScript Clean Code
## บทนำ  
            หากคุณใส่ใจกับแนวทางปฎิบัติและวิธีการเขียน แทนที่จะกังวลว่าจะทำงานได้หรือไม่ คุณสามารถฝึกฝนและใส่ใจเกี่ยวกับ JavaScript Clean Code นักพัฒนามืออาชีพจะเขียนโค้ดสำหรับตัวเองจะทำให้เรามีความสะดวกในการใช้งาน   ขึ้นอยู่กับ JavaScript Clean Code สามารถเขียนให้เป็น Code ที่มนุษย์เข้าใจง่าย

### นี่คือภาพที่แสดงถึง JavaScript Clean Code   
![](data:image/jpeg;base64,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)  

        จากคุณโรเบิร์ตซีมาติน ได้ให้คำกล่าวว่า " แม้แต่รหัสที่ไม่ดีก็สามารถทำงานได้ แต่ถ้ารหัสที่ไม่สะอาดก็อาจพาองค์กรไปสู่จุดที่ต่ำลงได้ "  
 
 ## แนวทางปฎิบัติที่ดีที่สุดสำหรับรหัสที่สะอาด  
 # 1. การตรวจสอบประเภทที่แข็งแกร่ง 

            การใช้ === แทน ==  
            0 == false     //true  
            0 === false    //false  
            2 == "2"       //true  
            2 === "2"      //false  

 * #### ตัวอย่างเช่น  
            // example  
            const value = "500";  
            if (value === 500) {  
            console.log(value);  
            // it will not be reached  
            }  


            if (value === "500") {  
            console.log(value);  
            // it will be reached  
            }  

 
# 2.ตัวแปร 
 
ตั้งชื่อตัวแปรของคุณในแบบที่พวกเขาเปิดเผยความตั้งใจ วิธีนี้พวกเขาสามารถค้นหาได้และง่ายต่อการเข้าใจหลังจากที่บุคคลเห็น 

 #### ตัวอย่างที่ไม่ดี  
            let daysSLV = 10;  
            let y = new Date().getFullYear();  

            let ok;  
            if (user.age > 30) {  
            ok = true;  
            }  
 #### ตัวอย่างที่ดี  
            const MAX_AGE = 30;  
            let daysSinceLastVisit = 10;  
            let currentYear = new Date().getFullYear();  

            ...

            const isUserOlderThanAllowed = user.age > MAX_AGE;  

อย่าเพิ่มคำที่ไม่จำเป็นงในตัวแปร     

#### ตัวอย่างที่ไม่ดีเช่น  
            let nameValue;  
            let theProduct;   


#### ตัวอย่างที่ไม่ดีเช่น  
            let name;  
            let product;    


อย่าบังคับให้ต้องจำบริบทของตัวแปร   

#### ตัวอย่างที่ไม่ดีเช่น   

            const users = ["John", "Marco", "Peter"];  
            users.forEach(u => {  
            doSomething();  
            doSomethingElse();  
            // ...  
            // ...  
            // ...  
            // ...  
            // Here we have the WTF situation: WTF   is `u` for?  
            register(u);  
            });   

#### ตัวอย่างที่ดีเช่น  
            const users = ["John", "Marco", "Peter"];  
            users.forEach(user => {  
            doSomething();  
            doSomethingElse();  
            // ...  
            // ...  
            // ...  
            // ...  
            register(user);  
            });    


อย่าเพิ่มบริบทที่ไม่จำเป็น    

#### ตัวอย่างที่ไม่ดีเช่น   
            const user = {  
            userName: "John",  
            userSurname: "Doe",  
            userAge: "28"  
            };  


            ...  


            user.userName;    

#### ตัวอย่างที่ดีเช่น   
            const user = {  
            name: "John",  
            surname: "Doe",  
            age: "28"  
            };  

            ...  

            user.name;  

# 3.ฟังก์ชั่น    

ใช้ชื่อที่ยาวและเป็นคำอธิบาย เมื่อพิจารณาว่ามันแสดงถึงพฤติกรรมบางอย่างชื่อฟังก์ชั่นควรเป็นคำกริยาหรือวลีที่แสดงถึงเจตนาที่อยู่เบื้องหลังและเจตนาของข้อโต้แย้ง ชื่อของพวกเขาควรพูดในสิ่งที่พวกเขาทำ    

#### ตัวอย่างที่ไม่ดีเช่น   

            function notif(user) {  
            // implementation  
            }  
#### ตัวอย่างที่ดีเช่น   

            function notifyUser(emailAddress) {  
            // implementation  
            }    
            
หลีกเลี่ยงการโต้แย้งที่ยาวนาน ตามหลักการแล้วฟังก์ชันควรมีอาร์กิวเมนต์สองตัวหรือน้อยกว่าที่ระบุ ข้อโต้แย้งที่น้อยกว่านั้นง่ายขึ้นคือการทดสอบฟังก์ชั่น    

#### ตัวอย่างที่ไม่ดีเช่น    

            function getUsers(fields, fromDate, toDate) {  
            // implementation  
            }     

#### ตัวอย่างที่ดีเช่น  
            function getUsers({ fields, fromDate, toDate }) {  
            // implementation  
            }   

            getUsers({  
                fields: ['name', 'surname', 'email'],  
                fromDate: '2019-01-01',  
                toDate: '2019-01-18'  
            });     
            
ใช้อาร์กิวเมนต์เริ่มต้นแทนเงื่อนไข    

#### ตัวอย่างที่ไม่ดีเช่น    

            function createShape(type) {  
            const shapeType = type || "cube";  
            // ...  
            }   

#### ตัวอย่างที่ดีเช่น   

            function createShape(type = "cube") {  
            // ...  
            }    
ฟังก์ชั่นควรทำสิ่งหนึ่ง หลีกเลี่ยงการดำเนินการหลายการกระทำภายในฟังก์ชั่นเดียว    

#### ตัวอย่างที่ไม่ดีเช่น    

            function notifyUsers(users) {  
            users.forEach(user => {  
                const userRecord = database.lookup(user);  
                if (userRecord.isVerified()) {  
                notify(user);  
                }  
            });  
            }    


#### ตัวอย่างที่ดีเช่น    

            function notifyVerifiedUsers(users) {  
            users.filter(isUserVerified).forEach  (notify);  
            }  

            function isUserVerified(user) {  
            const userRecord = database.lookup(user);  
            return userRecord.isVerified();  
            }      

ใช้Object.assignเพื่อตั้งค่าวัตถุเริ่มต้น     

#### ตัวอย่างที่ไม่ดีเช่น   

            const shapeConfig = {  
            type: "cube",  
            width: 200,  
            height: null  
            };  


            function createShape(config) {  
            config.type = config.type || "cube";  
            config.width = config.width || 250;  
            config.height = config.height || 250;  
            }  
            createShape(shapeConfig);  

#### ตัวอย่างที่ดีเช่น  
            const shapeConfig = {  
            type: "cube",  
            width: 200  
            // Exclude the 'height' key  
            };  

            function createShape(config) {  
            config = Object.assign(  
                {  
                type: "cube",  
                width: 250,  
                height: 250  
                },  
                config  
            );  

            ...  
            }  
            createShape(shapeConfig);    


อย่าใช้แฟล็กเป็นพารามิเตอร์เพราะพวกเขากำลังบอกคุณว่าฟังก์ชั่นทำงานได้ดีเกินควร    

#### ตัวอย่างที่ไม่ดีเช่น     

            function createFile(name, isPublic) {  
            if (isPublic) {  
                fs.create(`./public/${name}`);  
            } else {  
                fs.create(name);  
            }  
            }    

#### ตัวอย่างที่ดีเช่น   

            function createFile(name) {  
            fs.create(name);  
            }  

            function createPublicFile(name) {  
            createFile(`./public/${name}`);  
            }     


หากคุณต้องการขยายวัตถุที่มีอยู่ ให้ใช้คลาส ES และการสร้างฟังก์ชันต้นแบบของวัตถุเดิม    

#### ตัวอย่างที่ไม่ดีเช่น    

            Array.prototype.myFunc = function myFunc() {  
            // implementation  
            };     

#### ตัวอย่างที่ดีเช่น    

            class SuperArray extends Array {  
            myFunc() {  
                // implementation  
            }  
            }    

# 4.เงื่อนไข    
หลีกเลี่ยงเงื่อนไขในเชิงลบ  
#### ตัวอย่างที่ไม่ดีเช่น   
            function isUserNotBlocked(user) {  
            // implementation  
            }  

            if (!isUserNotBlocked(user)) {  
            // implementation  
            }    

#### ตัวอย่างที่ดีเช่น   

            function isUserBlocked(user) {  
            // implementation  
            }  

            if (isUserBlocked(user)) {  
            // implementation  
            }   


ใช้เงื่อนไขอาจอาจเป็นเรื่องเล็กน้อย แต่คุ้มค่า ใช้วิธีการนี้เฉพาะสำหรับค่าบูลีนหรือUndefinenull  

#### ตัวอย่างที่ไม่ดีเช่น    

            if (isValid === true) {  
            // do something...  
            }  

            if (isValid === false) {  
            // do something...  
            }       

#### ตัวอย่างที่ดีเช่น     

            if (isValid) {  
            // do something...  
            }  

            if (!isValid) {  
            // do something...  
            }  


หลีกเลี่ยงการทำตามเงื่อนไขเมื่อทำได้ ใช้ความหลากหลายและการสืบทอดแทน  

#### ตัวอย่างที่ไม่ดีเช่น   

            class Car {  
            // ...  
            getMaximumSpeed() {  
                switch (this.type) {  
                case "Ford":  
                    return this.someFactor() + this.  anotherFactor();  
                case "Mazda":  
                    return this.someFactor();  
                case "McLaren":  
                    return this.someFactor() - this.  anotherFactor();  
                }  
            }  
            }    

#### ตัวอย่างที่ดีเช่น  

            class Car {  
            // ...  
            }  

            class Ford extends Car {  
            // ...  
            getMaximumSpeed() {  
                return this.someFactor() + this.  anotherFactor();  
            }  
            }  

            class Mazda extends Car {  
            // ...  
            getMaximumSpeed() {  
                return this.someFactor();  
            }  
            }  

            class McLaren extends Car {  
            // ...  
            getMaximumSpeed() {  
                return this.someFactor() - this.  anotherFactor();  
            }  
            }   
  

# 5.คลาส ES  

คลาสคือประโยคใหม่ใน JavaScript ทุกอย่างทำงานเหมือนเดิมกับต้นแบบเท่านั้น ตอนนี้มันดูแตกต่างและควรจะชอบฟังก์ชั่นธรรมดามากกว่า ES5   

#### ตัวอย่างที่ไม่ดีเช่น   

            const Person = function(name) {  
            if (!(this instanceof Person)) {  
                throw new Error("Instantiate Person   with `new` keyword");  
            }  


            this.name = name;  
            };  

            Person.prototype.sayHello = function   sayHello() { /**/ };    


            const Student = function(name, school) {  
            if (!(this instanceof Student)) {    
                throw new Error("Instantiate Student   with `new` keyword");    
            }  

            Person.call(this, name);
            this.school = school;
            };

            Student.prototype = Object.create(Person.prototype);  
            Student.prototype.constructor = Student;  
            Student.prototype.printSchoolName = function printSchoolName() { /**/ };  


#### ตัวอย่างที่ดีเช่น    

            class Person {  
            constructor(name) {  
                this.name = name;  
            }  


            sayHello() {  
                /* ... */  
            }  
            }  


            class Student extends Person {  
            constructor(name, school) {  
                super(name);  
                this.school = school;  
            }  

            printSchoolName() {  
                /* ... */  
            }  
            }   
  

ใช้วิธีการผูกมัด libraryหลายแห่งเช่น jQuery และ Lodash ใช้รูปแบบนี้ เป็นผลให้รหัสของคุณจะ verbose น้อยลง ในคลาสเพียงแค่กลับมาthisที่จุดสิ้นสุดของทุกฟังก์ชั่นและสามารถโยงวิธีการเรียนเพิ่มเติมเข้ากับมัน    

#### ตัวอย่างที่ไม่ดีเช่น    

            class Person {  
            constructor(name) {  
                this.name = name;  
            }  


            setSurname(surname) {  
                this.surname = surname;  
            }  

            setAge(age) {  
                this.age = age;  
            }  

            save() {  
                console.log(this.name, this.surname, this.age);  
            }  
            }  

            const person = new Person("John");  
            person.setSurname("Doe");  
            person.setAge(29);  
            person.save();  

#### ตัวอย่างที่ดีเช่น    

            class Person {  
            constructor(name) {  
                this.name = name;  
            }  


            setSurname(surname) {  
                this.surname = surname;  
                // Return this for chaining  
                return this;  
            }  


            setAge(age) {  
                this.age = age;  
                // Return this for chaining  
                return this;  
            }  
            
            save() {  
                console.log(this.name, this.surname, this.age);  
                // Return this for chaining  
                return this;  
            }  
            }  

            const person = new Person("John")  
                .setSurname("Doe")  
                .setAge(29)  
                .save();  

# 6.หลีกเลี่ยงโดยทั่วไป  
        โดยทั่วไปแล้วไม่ควรเขียนรหัสซ้ำและไม่ควรทิ้งฟังก์ชั่นที่ไม่ได้ใช้แล้วหรือรหัสที่ตายแล้ว  
        สามารถมีรหัสที่ซ้ำกันได้จากหายสาเหตุ เช่นสามารถมี2สิ่งที่แตกต่างกันเล็กน้อยซึ่งมีการใช้งานร่วมกันจำนวนมากและลักษณะของความแตกต่างหรือกำหนดเวลาทำให้ต้องสร้างฟังก์ชั่นแยกต่างหากที่มีรหัสเกือบเหมือนกัน  การลบรหัสที่ซ้ำกันในสถานการณ์นี้หมายถึงทำให้ความแตกต่างเป็นนามธรรมและจัดการกับมันในระดับนั้น และเกี่ยวกับรหัสที่ตายแล้วมันเป็นชื่อของมัน มันคือรหัสที่อยู่ในฐานรหัสของเราไม่ได้ทำอะไรเพราะในบางช่วงของการพัฒนาคุณได้ตัดสินใจแล้วว่ามันไม่มีจุดประสงค์อีกต่อไป ควรค้นหาฐานรหัสของสำหรับชิ้นส่วนเหล่านี้และลบฟังก์ชั่นและบล็อกโค้ดที่ไม่จำเป็นทั้งหมด คำแนะนำที่ฉันสามารถให้กับคุณได้คือในไม่ช้าคุณจะตัดสินใจว่าไม่จำเป็นต้องลบอีกต่อไป หลังจากนั้นคุณอาจลืมสิ่งที่ใช้

# ข้อสรุป  

        นี่เป็นเพียงเศษเสี้ยวของสิ่งที่สามารถทำได้เพื่อปรับปรุงรหัส หลักการที่กล่าวถึงในที่นี้คือหลักการที่ผู้คนมักไม่ปฏิบัติตาม พวกเขาพยายาม แต่ไม่ประสบความสำเร็จด้วยเหตุผลหลายประการ บางทีในช่วงเริ่มต้นของ javascript clean code แต่เมื่อมันมาถึงมักจะถูกละเลยและย้ายเข้าไปอยู่ใน"สิ่งที่ต้องทำ"หรือ"refactor"ส่วน ณ จุดนี้ลูกค้าของคุณต้องการให้คุณตรงตามกำหนดเวลาแทนที่จะเขียนjavascript clean code 























































