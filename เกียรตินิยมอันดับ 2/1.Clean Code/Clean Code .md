# clean-code-javascript
## Table of Contents
* 1.[Introduction](#Introduction )
* 2.Variables  
* 3.Functions  
* 4.Objects and Data Structures
* 5.Classes  
* 6.SOLID  
* 7.Testing
* 8.Concurrency
* 9.Error Handling
* 10.Formatting
* 11.comments
* 12.Translation

# Introduction 
หลักการต่อไปนี้ไม่ต้องปฎิบัตอย่างเคร่งครัด เป็นเพียงแนวทางเพิ่มเติม โดยมีคนที่มีประสบการณ์ร่วมกันพัฒนาพัฒนา กลายเป็นclean-code-javascript  และอีกอย่างหนึ่ง: การรู้สิ่งเหล่านี้จะไม่ทำให้คุณเป็นนักพัฒนาซอฟต์แวร์ที่ดีขึ้นทันทีและการทำงานกับพวกเขาเป็นเวลาหลายปีไม่ได้หมายความว่าคุณจะไม่ทำผิดพลาด โค้ดทุกชิ้นเริ่มต้นเป็นร่างแรก ในที่สุดเราก็จะกำจัดความไม่สมบูรณ์โดยการกำจัดจุดออ่นของเราออกไป อย่าเอาชนะตัวเอง แต่เอาชนะรหัสแทน  

## ตัวแปร
### ใช้ชื่อตัวแปรที่มีความหมายและออกเสียงได้

#### ตัวอย่าง ตัวแปรที่ไม่ดี เช่น  
const yyyymmdstr = moment().format("YYYY/MM/DD");

#### ตัวอย่าง ตัวแปรที่ไม่ดี เช่น  
const currentDate = moment().format("YYYY/MM/DD");  

### ใช้คำศัพท์เดียวกันสำหรับตัวแปรประเภทเดียวกัน  
#### ตัวอย่างที่ไม่ดี  
getUserInfo ( ) ; 
getClientData ( ) ; 
getCustomerRecord ( ) ;

#### ตัวอย่างที่ดี  
getUser ( ) ;

## ใช้ชื่อที่ค้นหาได้  
เราจะอ่านโค้ดมากกว่าที่เราจะเขียน สิ่งสำคัญคือรหัสที่เราเขียนนั้นสามารถอ่านได้และค้นหาได้  
 #### ตัวอย่างในการค้นหาที่แย่  
 // heck คืออะไร 86400000 สำหรับ?  
setTimeout ( blastOff ,  86400000 ) ; 
#### ตัวอย่างในการค้นหาที่ดี  
  // ประกาศให้เป็นค่าคงที่ที่มีชื่อ  

const  MILLISECONDS_IN_A_DAY  =  86_400_000 ;  


setTimeout ( Blastoff ,  MILLISECONDS_IN_A_DAY ) ;  

## ใช้ตัวแปรอธิบาย  
#### ตัวอย่างที่ไม่ดี
const address = "One Infinite Loop, Cupertino 95014";
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
saveCityZipCode(
  address.match(cityZipCodeRegex)[1],
  address.match(cityZipCodeRegex)[2]
);  
#### ตัวอย่างที่ดี  
const address = "One Infinite Loop, Cupertino 95014";
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [_, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCode(city, zipCode);  
### Avoid Mental Mapping  
#### ตัวอย่างที่ไม่ดี  
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(l => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  // Wait, what is `l` for again?
  dispatch(l);
});  
#### ตัวอย่างที่ดี  
  const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(location => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  dispatch(location);
});  
###  อย่าเพิ่มบริบทที่ไม่จำเป็น  
หากชื่อคลาส / วัตถุของคุณบอกอะไรคุณอย่าทำซ้ำในชื่อตัวแปรของคุณ  
#### ตัวอย่างที่ไม่ดี  
 const Car = {
  carMake: "Honda",
  carModel: "Accord",
  carColor: "Blue"
};

function paintCar(car) {
  car.carColor = "Red";
}  
#### ตัวอย่างที่ดี  
  const Car = {
  make: "Honda",
  model: "Accord",
  color: "Blue"
};

function paintCar(car) {
  car.color = "Red";
}  
### ใช้อาร์กิวเมนต์เริ่มต้นแทนการลัดวงจรหรือเงื่อนไข  
อาร์กิวเมนต์เริ่มต้นมักจะสะอาดกว่าการลัดวงจร อาร์กิวเมนต์เริ่มต้นมักจะสะอาดกว่าการลัดวงจร ช่น'', "", false, null, 0และ NaNจะไม่ถูกแทนที่ด้วยค่าเริ่มต้น

### ตัวอย่างที่ไม่ดี  
  function createMicrobrewery(name) {
  const breweryName = name || "Hipster Brew Co.";
  // ...
}  
#### ตัวอย่างที่ดี  
 function createMicrobrewery(name = "Hipster Brew Co.") {
  // ...
}  


# Functions  
## อาร์กิวเมนต์ของฟังก์ชัน (2 หรือน้อยกว่า)  
การจำกัด จำนวนพารามิเตอร์ฟังก์ชั่นนั้นสำคัญอย่างไม่น่าเชื่อเพราะทำให้การทดสอบฟังก์ชั่นของคุณง่ายขึ้น ต้องทดสอบกรณีที่แตกต่างกันจำนวนหนึ่งโดยมีการโต้แย้งแยกกัน  
หนึ่งหรือสองอาร์กิวเมนต์เป็นกรณีในอุดมคติและสามควรหลีกเลี่ยงถ้าเป็นไปได้ อะไรที่มากกว่านั้นควรจะรวม เนื่องจาก JavaScript ช่วยให้คุณสามารถสร้างวัตถุได้ทันทีโดยไม่ต้องมีคลาสสำเร็จรูป คุณสามารถ ใช้วัตถุได้หากคุณพบว่าตัวเองต้องการอาร์กิวเมนต์จำนวนมาก  


### โครงสร้าง ES2015 / ES6 นี่มีข้อดีบางประการ:   
1เมื่อมีคนดูที่ลายเซ็นของฟังก์ชั่นมันจะชัดเจนทันทีว่ามีการใช้คุณสมบัติใด 
2มันสามารถใช้ในการจำลองพารามิเตอร์ที่มีชื่อ  3 วัตถุและอาร์เรย์ที่ถูกทำลายจากวัตถุอาร์กิวเมนต์จะไม่ถูกโคลน 4 Linters สามารถเตือนคุณเกี่ยวกับคุณสมบัติที่ไม่ได้ใช้ซึ่งจะเป็นไปไม่ได้หากไม่มีการทำลายล้าง    
#### ตัวอย่างที่ไม่ดี  
function createMenu(title, body, buttonText, cancellable) {
  // ...
}

createMenu("Foo", "Bar", "Baz", true);  

#### ตัวอย่างที่ไม่ดี  
function createMenu({ title, body, buttonText, cancellable }) {
  // ...
}

createMenu({
  title: "Foo",
  body: "Bar",
  buttonText: "Baz",
  cancellable: true
});   
#### ฟังก์ชั่นควรทำสิ่งหนึ่ง  
นี่เป็นกฎที่สำคัญที่สุดในวิศวกรรมซอฟต์แวร์ เมื่อฟังก์ชั่นทำมากกว่าหนึ่งอย่างมันยากที่จะเขียนทดสอบและหาเหตุผล เมื่อคุณสามารถแยกฟังก์ชั่นเป็นหนึ่งการกระทำก็สามารถปรับโครงสร้างได้อย่างง่ายดายและโค้ดของคุณจะอ่านสะอาดขึ้นมาก หากคุณไม่ทำอะไรนอกเหนือจากคู่มือนี้นอกเหนือจากนี้คุณจะเป็นผู้นำของนักพัฒนาหลายคน  
##### ตัวอย่างที่ไม่ดี  
function emailClients(clients) {
  clients.forEach(client => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}  
##### ตัวอย่างที่ดี  
function emailActiveClients(clients) {
  clients.filter(isActiveClient).forEach(email);
}

function isActiveClient(client) {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}  
### Function names should say what they do  
#### ตัวอย่างที่ไม่ดี  
function addToDate(date, month) {
  // ...
}

const date = new Date();

// It's hard to tell from the function name what is added
addToDate(date, 1);  
#### ตัวอย่างที่ดี  
function addMonthToDate(month, date) {
  // ...
}

const date = new Date();
addMonthToDate(1, date);  
### ฟังก์ชั่นควรเป็นระดับหนึ่งของนามธรรม  
เมื่อคุณมีสิ่งที่เป็นนามธรรมมากกว่าหนึ่งระดับฟังก์ชั่นของคุณมักจะทำมากเกินไป ฟังก์ชั่นการแยกจะทำให้สามารถนำมาใช้ซ้ำและทดสอบได้ง่ายขึ้น  
#### ตัวอย่างที่ไม่ดี  
function parseBetterJSAlternative(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(" ");
  const tokens = [];
  REGEXES.forEach(REGEX => {
    statements.forEach(statement => {
      // ...
    });
  });

  const ast = [];
  tokens.forEach(token => {
    // lex...
  });

  ast.forEach(node => {
    // parse...
  });
}  
  
#### ตัวอย่างที่ดี  
function parseBetterJSAlternative(code) {
  const tokens = tokenize(code);
  const syntaxTree = parse(tokens);
  syntaxTree.forEach(node => {
    // parse...
  });
}

function tokenize(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(" ");
  const tokens = [];
  REGEXES.forEach(REGEX => {
    statements.forEach(statement => {
      tokens.push(/* ... */);
    });
  });

  return tokens;
}

function parse(tokens) {
  const syntaxTree = [];
  tokens.forEach(token => {
    syntaxTree.push(/* ... */);
  });

  return syntaxTree;
}  
### ลบรหัสที่ซ้ำกัน  
 เพื่อหลีกเลี่ยงรหัสที่ซ้ำกัน รหัสซ้ำไม่ดีเพราะมันหมายความว่ามีมากกว่าหนึ่ง การลบรหัสที่ซ้ำกันหมายถึงการสร้างสิ่งที่เป็นนามธรรมซึ่งสามารถจัดการชุดต่าง ๆ ของสิ่งนี้ได้ด้วยฟังก์ชั่น / โมดูล / คลาสเดียว  การได้รับสิ่งที่ถูกต้องเป็นสิ่งสำคัญนั่นคือเหตุผลที่คุณควรปฏิบัติตามหลักการของ SOLID ที่ระบุไว้ในส่วนของคลาส abstractions ที่ไม่ถูกต้องอาจแย่กว่ารหัสที่ซ้ำกันดังนั้นโปรดระวัง!  
#### ตัวอย่างที่ไม่ดี  
function showDeveloperList(developers) {
  developers.forEach(developer => {
    const expectedSalary = developer.calculateExpectedSalary();
    const experience = developer.getExperience();
    const githubLink = developer.getGithubLink();
    const data = {
      expectedSalary,
      experience,
      githubLink
    };

    render(data);
  });
}

function showManagerList(managers) {
  managers.forEach(manager => {
    const expectedSalary = manager.calculateExpectedSalary();
    const experience = manager.getExperience();
    const portfolio = manager.getMBAProjects();
    const data = {
      expectedSalary,
      experience,
      portfolio
    };

    render(data);
  });
}  
#### ตัวอย่างที่ดี  
function showEmployeeList(employees) {
  employees.forEach(employee => {
    const expectedSalary = employee.calculateExpectedSalary();
    const experience = employee.getExperience();

    const data = {
      expectedSalary,
      experience
    };

    switch (employee.type) {
      case "manager":
        data.portfolio = employee.getMBAProjects();
        break;
      case "developer":
        data.githubLink = employee.getGithubLink();
        break;
    }

    render(data);
  });
}  
### ตั้งค่าวัตถุเริ่มต้นด้วย Object.assign  
const menuConfig = {
  title: null,
  body: "Bar",
  buttonText: null,
  cancellable: true
};

function createMenu(config) {
  config.title = config.title || "Foo";
  config.body = config.body || "Bar";
  config.buttonText = config.buttonText || "Baz";
  config.cancellable =
    config.cancellable !== undefined ? config.cancellable : true;
}

createMenu(menuConfig);  
#### ตัวอย่างที่ดี  
const menuConfig = {
  title: "Order",
  // User did not include 'body' key
  buttonText: "Send",
  cancellable: true
};

function createMenu(config) {
  config = Object.assign(
    {
      title: "Foo",
      body: "Bar",
      buttonText: "Baz",
      cancellable: true
    },
    config
  );

  // config now equals: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
  // ...
}

createMenu(menuConfig);  
### อย่าใช้ค่าสถานะเป็นพารามิเตอร์ฟังก์ชัน  
ฟังก์ชั่นควรทำสิ่งหนึ่ง แยกฟังก์ชั่นของคุณออก  
#### ตัวอย่างที่ไม่ดี  
  function createFile(name, temp) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}  
#### ตัวอย่างที่ดี  
function createFile(name) {
  fs.create(name);
}

function createTempFile(name) {
  createFile(`./temp/${name}`);
}  
 ### หลีกเลี่ยงผลข้างเคียง (ตอนที่ 1)  
 ฟังก์ชั่นสร้างผลข้างเคียงหากทำสิ่งอื่นนอกจากรับค่าและส่งคืนค่าหรือค่าอื่น ผลข้างเคียงในโปรแกรมในบางครั้ง สิ่งที่ต้องทำคือการรวมปัญหา ไม่มีฟังก์ชั่นและคลาสที่เขียนไปยังไฟล์เฉพาะ ประเด็นหลักคือการหลีกเลี่ยงข้อผิดพลาดทั่วไปเช่นการแชร์สถานะระหว่างวัตถุโดยไม่มีโครงสร้างใด ๆ ใช้ชนิดข้อมูลที่ไม่แน่นอนที่สามารถเขียนได้โดยอะไรและไม่รวมศูนย์ที่ผลข้างเคียงของคุณเกิดขึ้น หากคุณสามารถทำสิ่งนี้ได้คุณจะสะดวกมากกว่าโปรแกรมเมอร์คนอื่น ๆ  
 #### ตัวอย่างที่ไม่ดี  
 // Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
let name = "Ryan McDermott";

function splitIntoFirstAndLastName() {
  name = name.split(" ");
}

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];  
#### ตัวอย่างที่ดี  
function splitIntoFirstAndLastName(name) {
  return name.split(" ");
}

const name = "Ryan McDermott";
const newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];  
###  หลีกเลี่ยงผลข้างเคียง (ตอนที่ 2)  
ใน JavaScript การส่งผ่านดั้งเดิมจะมีค่าและวัตถุ / อาร์เรย์ถูกส่งผ่านโดยการอ้างอิง   ในกรณีของวัตถุและอาร์เรย์หากฟังก์ชั่นของคุณทำการเปลี่ยนแปลงในอาร์เรย์เช่นการเพิ่มฟังก์ที่ใช้ cart อาร์เรย์นั้นจะได้ผลกระทบจากการเพิ่มนี้  
คำเตือน2ข้อที่จะกล่าวถึง  
1.อาจมีบางกรณีที่คุณต้องปรับเปลี่ยนอินพุต    แต่เมื่อใช้การฝึกเขียนโปรแกรมนี้คุณจะพบว่ากรณีเหล่านี้ค่อนข้างหายาก สิ่งต่าง ๆ ส่วนใหญ่สามารถ refactored ไม่มีผลข้างเคียง!  
2.การโคลนวัตถุขนาดใหญ่อาจมีราคาแพงมากในแง่ของประสิทธิภาพ โชคดีที่นี่ไม่ใช่ปัญหาใหญ่ในทางปฏิบัติเพราะมี ไลบรารีที่ยอดเยี่ยมที่อนุญาตให้วิธีการเขียนโปรแกรมชนิดนี้รวดเร็วและไม่ได้ใช้หน่วยความจำมากเหมือนที่คุณใช้ในการโคลนวัตถุและอาร์เรย์ด้วยตนเอง  
  
#### ตัวอย่างที่ไม่ดี  
  const addItemToCart = (cart, item) => {
  cart.push({ item, date: Date.now() });
};  
#### ตัวอย่างที่ดี  
const addItemToCart = (cart, item) => {
  return [...cart, { item, date: Date.now() }];
};  
### อย่าเขียนฟังก์ชั่นระดับโลก  















  





































  