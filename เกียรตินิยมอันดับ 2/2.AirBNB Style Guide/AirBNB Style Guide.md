# Airbnb JavaScript
        หมายเหตุ:คู่มือนี้จะถือว่าใช้Babelและต้องการให้ใช้babel-preset-airbnbหรือเทียบเท่า นอกจากนี้ยังถือว่าคุณกำลังติดตั้ง shims / polyfills ในแอปของคุณด้วยairbnb-browser-shimsหรือเทียบเท่า  
## สารบัญ
1. ประเภท  
2. อ้างอิง  
3. Objects 
4. อาร์เรย์  
5. Destructuring  
6. เงื่อนไข  
7. ฟังก์ชั่น  
8. Arrow Functions
9. Classes & Constructors
10. โมดูล  
11. Iterators and Generators 
12. คุณสมบัติ  
13. ตัวแปร  
14. hoisting  
15. Comparison Operators & Equality  
16. บล็อก  
17. Control Statements
18. Comments
19. ช่องว่าง  
20. จุลภาค  
21. อัฒภาค  
22. Type Casting & Coercion
23. Naming Conventions  
24. Accessors  
25. เหตุการณ์ที่เกิดขึ้น  
26. JQuery  
27. ECMAScript 5 Compatibility  
28. ECMAScript 6+ (ES 2015+) Styles  
29. Standard Library  
30. Testing  
31. Performance  
32. Resources  
33. In the Wild  
34. Translation  
35. The JavaScript Style Guide Guide  
36. Chat With Us About JavaScript  
37. Contributors  
38. License  
39. Amendments  

# Types

* 1.1 Primitives : เมื่อคุณเข้าถึงชนิดดั้งเดิมที่คุณทำงานโดยตรงบนความคุ้มค่า  
    * string  
    * number  
    * boolean  
    * null  
    * undefined  
    * symbol  
    * bigint

            const foo = 1;
            let bar = foo;

            bar = 9;

            console.log(foo, bar); // => 1, 9  

    * ดังนั้นจึงไม่ควรใช้กำหนดเป้าหมายเบราว์เซอร์ / สภาพแวดล้อมที่ไม่สนับสนุนตั่งแต่แรก  

* คอมเพล็กซ์ : เมื่อคุณเข้าถึงประเภทที่ซับซ้อนคุณจะทำงานกับการอ้างอิงถึงค่าของมัน  
    * object  
    * array  
    * function

                const  foo  =  [ 1 ,  2 ] ; 
            const  bar  =  foo ; 
            bar [ 0 ]  =  9 ; 
            ปลอบใจ บันทึก( foo [ 0 ] , แถบ[ 0 ] ) ; // => 9, 9 

# อ้างอิง
* 2.1ใช้constสำหรับการอ้างอิงทั้งหมดของ varหลีกเลี่ยงการใช้ eslint: prefer-const,no-const-assign    

            // bad 
            var  a  =  1 ; 
            var  b  =  2 ; 

            // ดี
            const  a  =  1 ; 
            const  b  =  2 ;  

* 2.2ถ้าต้องโอนสิทธิการอ้างอิงใช้แทนlet vareslint:no-var    

            // bad
            var count = 1;
            if (true) {
            count += 1;
            }

            // good, use the let.
            let count = 1;
            if (true) {
            count += 1;
            }  
* 2.3โปรดทราบว่าทั้งสองletและconstถูกกำหนดขอบเขตแบบบล็อก

        // const and let only exist in the blocks they are defined in.
        {
        let a = 1;
        const b = 1;
        }
        console.log(a); // ReferenceError
        console.log(b); // ReferenceError
  
# Objects  
* 3.1ใช้ไวยากรณ์ตัวอักษรสำหรับการสร้างวัตถุ eslint:no-new-object  

        // bad
        const item = new Object();

        // good
        const item = {};  

* 3.2ใช้ชื่อคุณสมบัติที่คำนวณได้เมื่อสร้างวัตถุที่มีชื่อคุณสมบัติแบบไดนามิก  
   
        function getKey(k) { 
        return `a key named ${k}`;
        }

        // bad
        const obj = {
        id: 5,
        name: 'San Francisco',
        };
        obj[getKey('enabled')] = true;

        // good
        const obj = {
        id: 5,
        name: 'San Francisco',
        [getKey('enabled')]: true,
        };  

 *  3.3ใช้วิธีการจดชวเลขวัตถุ eslint:object-shorthand  
            // bad
            const atom = {
            value: 1,

            addValue: function (value) {
                return atom.value + value;
            },
            };

            // good
            const atom = {
            value: 1,

            addValue(value) {
                return atom.value + value;
            },
            };    

* 3.4ใช้ชวเลขค่าคุณสมบัติ eslint:object-shorthand  
 
            const lukeSkywalker = 'Luke Skywalker';

            // bad
            const obj = {
            lukeSkywalker: lukeSkywalker,
            };

            // good
            const obj = {
            lukeSkywalker,
            };  

* 3.5จัดกลุ่มคุณสมบัติชวเลขของคุณไว้ที่จุดเริ่มต้นของการประกาศวัตถุของคุณ  

        const anakinSkywalker = 'Anakin Skywalker';
        const lukeSkywalker = 'Luke Skywalker';

        // bad
        const obj = {
        episodeOne: 1,
        twoJediWalkIntoACantina: 2,
        lukeSkywalker,
        episodeThree: 3,
        mayTheFourth: 4,
        anakinSkywalker,
        };

        // good
        const obj = {
        lukeSkywalker,
        anakinSkywalker,
        episodeOne: 1,
        twoJediWalkIntoACantina: 2,
        episodeThree: 3,
        mayTheFourth: 4,
        };  

* 3.6อ้างเฉพาะคุณสมบัติที่เป็นตัวระบุที่ไม่ถูกต้อง eslint:quote-props  

        // bad
        const bad = {
        'foo': 3,
        'bar': 4,
        'data-blah': 5,
        };

        // good
        const good = {
        foo: 3,
        bar: 4,
        'data-blah': 5,
        };  

* 3.7ไม่เรียกObject.prototypeวิธีการโดยตรงเช่นhasOwnProperty, และpropertyIsEnumerable isPrototypeOfeslint:no-prototype-builtins  

            // bad
            console.log(object.hasOwnProperty(key));

            // good
            console.log(Object.prototype.hasOwnProperty.call(object, key));

            // best
            const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
            console.log(has.call(object, key));
            /* or */
            import has from 'has'; // https://www.npmjs.com/package/has
            console.log(has(object, key));

* 3.8ชอบโอเปอเรเตอร์การแพร่กระจายวัตถุไปObject.assignยังวัตถุที่คัดลอกตื้น ใช้ตัวดำเนินการส่วนที่เหลือของวัตถุเพื่อรับวัตถุใหม่ที่มีคุณสมบัติบางอย่างถูกละเว้น    

        // very bad
        const original = { a: 1, b: 2 };
        const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
        delete copy.a; // so does this

        // bad
        const original = { a: 1, b: 2 };
        const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

        // good
        const original = { a: 1, b: 2 };
        const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

        const { a, ...noA } = copy; // noA => { b: 2, c: 3 }  


# อาร์เรย์
* 4.1ใช้ไวยากรณ์ตัวอักษรสำหรับการสร้างอาร์เรย์ eslint:no-array-constructor  

        // bad
        const items = new Array();

        // good
        const items = [];  

* 4.2ใช้Array # pushแทนการกำหนดโดยตรงเพื่อเพิ่มรายการลงในอาร์เรย์  

        const someStack = [];

        // bad
        someStack[someStack.length] = 'abracadabra';

        // good
        someStack.push('abracadabra');

* 4.3ใช้อาร์เรย์แบบกระจาย...เพื่อคัดลอกอาร์เรย์  

        // bad
        const len = items.length;
        const itemsCopy = [];
        let i;

        for (i = 0; i < len; i += 1) {
        itemsCopy[i] = items[i];
        }

        // good
        const itemsCopy = [...items];  

* 4.4การแปลงวัตถุ iterable ไปยังอาร์เรย์ให้ใช้สเปรดแทน...Array.from  

        const foo = document.querySelectorAll('.foo');

        // good
        const nodes = Array.from(foo);

        // best
        const nodes = [...foo];  

* 4.5 Use Array.from for converting an array-like object to an array.  

        const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

        // bad
        const arr = Array.prototype.slice.call(arrLike);

        // good
        const arr = Array.from(arrLike);  

* 4.6ใช้Array.fromแทนการแพร่กระจาย...สำหรับการทำแผนที่ผ่าน iterables เพราะมันหลีกเลี่ยงการสร้างอาร์เรย์กลาง  

        // bad
        const baz = [...foo].map(bar);

        // good
        const baz = Array.from(foo, bar);  

* 4.7ใช้ข้อความสั่งคืนในการเรียกกลับด้วยวิธีอาร์เรย์ มันตกลงที่จะละเว้นการกลับมาถ้าร่างกายทำงานประกอบด้วยคำเดียวกลับแสดงออกโดยไม่มีผลข้างเคียงต่อไปนี้8.2 eslint:array-callback-return  

        // good
        [1, 2, 3].map((x) => {
        const y = x + 1;
        return x * y;
        });

        // good
        [1, 2, 3].map((x) => x + 1);

        // bad - no returned value means `acc` becomes undefined after the first iteration
        [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
        const flatten = acc.concat(item);
        });

        // good
        [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
        const flatten = acc.concat(item);
        return flatten;
        });

        // bad
        inbox.filter((msg) => {
        const { subject, author } = msg;
        if (subject === 'Mockingbird') {
            return author === 'Harper Lee';
        } else {
            return false;
        }
        });

        // good
        inbox.filter((msg) => {
        const { subject, author } = msg;
        if (subject === 'Mockingbird') {
            return author === 'Harper Lee';
        }

        return false;
        });  

* 4.8ใช้ตัวแบ่งบรรทัดหลังจากเปิดและก่อนวงเล็บปิดอาร์เรย์ถ้าอาร์เรย์มีหลายบรรทัด  

        // bad
        const arr = [
        [0, 1], [2, 3], [4, 5],
        ];

        const objectInArray = [{
        id: 1,
        }, {
        id: 2,
        }];

        const numberInArray = [
        1, 2,
        ];

        // good
        const arr = [[0, 1], [2, 3], [4, 5]];

        const objectInArray = [
        {
            id: 1,
        },
        {
            id: 2,
        },
        ];

        const numberInArray = [
        1,
        2,
        ];  


# Destructuring 
* 5.1ใช้การทำลายวัตถุเมื่อเข้าถึงและใช้คุณสมบัติหลายอย่างของวัตถุ eslint:prefer-destructuring  

        // bad
        function getFullName(user) {
        const firstName = user.firstName;
        const lastName = user.lastName;

        return `${firstName} ${lastName}`;
        }

        // good
        function getFullName(user) {
        const { firstName, lastName } = user;
        return `${firstName} ${lastName}`;
        }

        // best
        function getFullName({ firstName, lastName }) {
        return `${firstName} ${lastName}`;
        }  

* 5.2ใช้การทำลายอาร์เรย์ eslint:prefer-destructuring  

        const arr = [1, 2, 3, 4];

        // bad
        const first = arr[0];
        const second = arr[1];

        // good
        const [first, second] = arr;  

* 5.3ใช้การทำลายวัตถุสำหรับค่าส่งคืนหลายค่าไม่ใช่การทำลายอาร์เรย์  

        // bad
        function processInput(input) {
        // then a miracle occurs
        return [left, right, top, bottom];
        }

        // the caller needs to think about the order of return data
        const [left, __, top] = processInput(input);

        // good
        function processInput(input) {
        // then a miracle occurs
        return { left, right, top, bottom };
        }

        // the caller selects only the data they need
        const { left, top } = processInput(input);  

# Strings
* 6.1ใช้เครื่องหมายคำพูดเดี่ยว''สำหรับสตริง eslint:quotes  

        // bad
        const name = "Capt. Janeway";

        // bad - template literals should contain interpolation or newlines
        const name = `Capt. Janeway`;

        // good
        const name = 'Capt. Janeway';  

* 6.2สายอักขระที่ทำให้สายยาวเกิน 100 อักขระไม่ควรเขียนข้ามหลายบรรทัดโดยใช้การต่อสตริง  

        // bad
        const errorMessage = 'This is a super long error that was thrown because \
        of Batman. When you stop to think about how Batman had anything to do \
        with this, you would get nowhere \
        fast.';

        // bad
        const errorMessage = 'This is a super long error that was thrown because ' +
        'of Batman. When you stop to think about how Batman had anything to do ' +
        'with this, you would get nowhere fast.';

        // good
        const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';  

* 6.3เมื่อสร้างสตริงโดยทางโปรแกรมให้ใช้เท็มเพลตสตริงแทนการต่อข้อมูล eslint:prefer-template template-curly-spacing  

        // bad
        function sayHi(name) {
        return 'How are you, ' + name + '?';
        }

        // bad
        function sayHi(name) {
        return ['How are you, ', name, '?'].join();
        }

        // bad
        function sayHi(name) {
        return `How are you, ${ name }?`;
        }

        // good
        function sayHi(name) {
        return `How are you, ${name}?`;
        }  

* 6.4ไม่เคยใช้eval()กับสตริงมันเปิดช่องโหว่มากเกินไป eslint:no-eval

* 6.5อย่าใช้ตัวละครในสตริงที่ไม่จำเป็น eslint:no-useless-escape    

        // bad
        const foo = '\'this\' \i\s \"quoted\"';

        // good
        const foo = '\'this\' is "quoted"';
        const foo = `my name is '${name}'`;  

# ฟังก์ชั่น  
* 7.1ใช้นิพจน์ฟังก์ชันที่ระบุชื่อแทนการประกาศฟังก์ชัน eslint:func-style  

        // bad
        function foo() {
        // ...
        }

        // bad
        const foo = function () {
        // ...
        };

        // good
        // lexical name distinguished from the variable-referenced invocation(s)
        const short = function longUniqueMoreDescriptiveLexicalFoo() {
        // ...
        };  

* 7.2 การตัดการเรียกใช้ฟังก์ชันนิพจน์ในวงเล็บทันที eslint:wrap-iife  

        // immediately-invoked function expression (IIFE)
        (function () {
        console.log('Welcome to the Internet. Please follow me.');
        }());  

* 7.3ไม่เคยประกาศฟังก์ชั่นในบล็อกที่ไม่ใช่ฟังก์ชั่น ( if, whileฯลฯ ) กำหนดฟังก์ชันให้กับตัวแปรแทน เบราว์เซอร์จะอนุญาตให้คุณทำ แต่พวกเขาทั้งหมดตีความแตกต่างกันซึ่งเป็นข่าวร้าย eslint:no-loop-func

* 7.4 หมายเหตุ: ECMA-262 กำหนดblockเป็นรายการของคำสั่ง การประกาศฟังก์ชั่นไม่ใช่คำสั่ง  

        // bad
        if (currentUser) {
        function test() {
            console.log('Nope.');
        }
        }

        // good
        let test;
        if (currentUser) {
        test = () => {
            console.log('Yup.');
        };
        }  

* 7.5argumentsไม่เคยตั้งชื่อพารามิเตอร์ สิ่งนี้จะมีความสำคัญเหนือargumentsวัตถุที่มอบให้กับทุกขอบเขตของฟังก์ชัน  

        // bad
        function foo(name, options, arguments) {
        // ...
        }

        // good
        function foo(name, options, args) {
        // ...
        }  

* 7.6ห้ามใช้argumentsโปรดเลือกใช้ไวยากรณ์ที่เหลือ...แทน eslint:prefer-rest-params  

        // bad
        function concatenateAll() {
        const args = Array.prototype.slice.call(arguments);
        return args.join('');
        }

        // good
        function concatenateAll(...args) {
        return args.join('');
        }  

* 7.7ใช้ไวยากรณ์ของพารามิเตอร์เริ่มต้นแทนที่จะกลายพันธุ์ฟังก์ชันอาร์กิวเมนต์  

        // really bad
        function handleThings(opts) {
        // No! We shouldn’t mutate function arguments.
        // Double bad: if opts is falsy it'll be set to an object which may
        // be what you want but it can introduce subtle bugs.
        opts = opts || {};
        // ...
        }

        // still bad
        function handleThings(opts) {
        if (opts === void 0) {
            opts = {};
        }
        // ...
        }

        // good
        function handleThings(opts = {}) {
        // ...
        }  

* 7.8หลีกเลี่ยงผลข้างเคียงด้วยพารามิเตอร์เริ่มต้น  

        var b = 1;
        // bad
        function count(a = b++) {
        console.log(a);
        }
        count();  // 1
        count();  // 2
        count(3); // 3
        count();  // 3  

* 7.9ใส่พารามิเตอร์เริ่มต้นเสมอ  

        // bad
        function handleThings(opts = {}, name) {
        // ...
        }

        // good
        function handleThings(name, opts = {}) {
        // ...
        }  

* 7.10ห้ามใช้ตัวสร้างฟังก์ชั่นเพื่อสร้างฟังก์ชั่นใหม่ eslint:no-new-func  

        // bad
        var add = new Function('a', 'b', 'return a + b');

        // still bad
        var subtract = Function('a', 'b', 'return a - b');  

* 7.11 การเว้นวรรคในลายเซ็นฟังก์ชัน eslint:space-before-function-paren space-before-blocks  

        // bad
        const f = function(){};
        const g = function (){};
        const h = function() {};

        // good
        const x = function () {};
        const y = function a() {};  

* 7.12ห้ามทำการเปลี่ยนแปลงพารามิเตอร์ eslint:no-param-reassign  

        // bad
        function f1(obj) {
        obj.key = 1;
        }

        // good
        function f2(obj) {
        const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
        }  

* 7.13ห้ามกำหนดพารามิเตอร์อีกครั้ง eslint:no-param-reassign  

        // 
        ฟังก์ชั่นที่ ไม่ดีf1 ( a )  { 
        a  =  1 ; 
        // ... 
        }

        ฟังก์ชั่น f2 ( a )  { 
        if  ( ! a )  {  a  =  1 ;  } 
        // ... 
        }

        // 
        ฟังก์ชั่น ที่ดีf3 ( a )  { 
        const  b  =  a  ||  1 ; 
        // ... 
        }

        ฟังก์ชัน f4 ( a =  1 )  { 
        // ... 
        }  

* 7.14ชอบการใช้งานของโอเปอเรเตอร์การแพร่กระจาย...เพื่อเรียกใช้ฟังก์ชั่น Variadic eslint:prefer-spread  

        // bad
        const x = [1, 2, 3, 4, 5];
        console.log.apply(console, x);

        // good
        const x = [1, 2, 3, 4, 5];
        console.log(...x);

        // bad
        new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

        // good
        new Date(...[2016, 8, 5]);  

* 7.15ฟังก์ชั่นที่มีลายเซ็นหลายบรรทัดหรือการเรียกใช้ควรเยื้องเหมือนกับรายการหลายบรรทัดอื่น ๆ ในคู่มือนี้: ด้วยแต่ละรายการในบรรทัดด้วยตัวเองพร้อมกับจุลภาคต่อท้ายในรายการสุดท้าย eslint:function-paren-newline  

        // bad
        function foo(bar,
                    baz,
                    quux) {
        // ...
        }

        // good
        function foo(
        bar,
        baz,
        quux,
        ) {
        // ...
        }

        // bad
        console.log(foo,
        bar,
        baz);

        // good
        console.log(
        foo,
        bar,
        baz,
        );  

# Arrow Functions  

* 8.1เมื่อคุณต้องใช้ฟังก์ชันที่ไม่ระบุชื่อ (เช่นเมื่อผ่านการโทรกลับแบบอินไลน์) ให้ใช้สัญกรณ์ลูกศร eslint: prefer-arrow-callback,arrow-spacing  

        // bad
        [1, 2, 3].map(function (x) {
        const y = x + 1;
        return x * y;
        });

        // good
        [1, 2, 3].map((x) => {
        const y = x + 1;
        return x * y;
        });  

* 8.2ถ้าฟังก์ชั่นของร่างกายประกอบด้วยคำสั่งเดียวที่ส่งคืนนิพจน์โดยไม่มีผลข้างเคียงให้ละเว้นวงเล็บปีกกาและใช้การส่งคืนโดยนัย มิฉะนั้นให้จัดฟันและใช้returnคำสั่ง eslint: arrow-parens,arrow-body-style  

        // bad
        [1, 2, 3].map((number) => {
        const nextNumber = number + 1;
        `A string containing the ${nextNumber}.`;
        });

        // good
        [1, 2, 3].map((number) => `A string containing the ${number + 1}.`);

        // good
        [1, 2, 3].map((number) => {
        const nextNumber = number + 1;
        return `A string containing the ${nextNumber}.`;
        });

        // good
        [1, 2, 3].map((number, index) => ({
        [index]: number,
        }));

        // No implicit return with side effects
        function foo(callback) {
        const val = callback();
        if (val === true) {
            // Do something if callback returns true
        }
        }

        let bool = false;

        // bad
        foo(() => bool = true);

        // good
        foo(() => {
        bool = true;
        });  

* 8.3ในกรณีที่นิพจน์ยาวเกินหลายบรรทัดให้ห่อในวงเล็บเพื่อให้อ่านได้ง่ายขึ้น  

        // bad
        ['get', 'post', 'put'].map((httpMethod) => Object.prototype.hasOwnProperty.call(
            httpMagicObjectWithAVeryLongName,
            httpMethod,
        )
        );

        // good
        ['get', 'post', 'put'].map((httpMethod) => (
        Object.prototype.hasOwnProperty.call(
            httpMagicObjectWithAVeryLongName,
            httpMethod,
        )
        ));  

* 8.4รวมวงเล็บไว้รอบ ๆ ข้อโต้แย้งเสมอเพื่อความชัดเจนและสม่ำเสมอ eslint:arrow-parens  

        // bad
        [1, 2, 3].map(x => x * x);

        // good
        [1, 2, 3].map((x) => x * x);

        // bad
        [1, 2, 3].map(number => (
        `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
        ));

        // good
        [1, 2, 3].map((number) => (
        `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
        ));

        // bad
        [1, 2, 3].map(x => {
        const y = x + 1;
        return x * y;
        });

        // good
        [1, 2, 3].map((x) => {
        const y = x + 1;
        return x * y;
        });  

* 8.5หลีกเลี่ยงไวยากรณ์ของฟังก์ชันลูกศรที่สับสน ( =>) กับตัวดำเนินการเปรียบเทียบ ( <=, >=) eslint:no-confusing-arrow  

        // bad
        const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

        // bad
        const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

        // good
        const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);

        // good
        const itemHeight = (item) => {
        const { height, largeSize, smallSize } = item;
        return height <= 256 ? largeSize : smallSize;
        };  

* 8.6บังคับใช้สถานที่ตั้งของร่างกายฟังก์ชั่นลูกศรที่มีผลตอบแทนโดยนัย eslint:implicit-arrow-linebreak  

        // bad
        (foo) =>
        bar;

        (foo) =>
        (bar);

        // good
        (foo) => bar;
        (foo) => (bar);
        (foo) => (
        bar
        )  

# Classes & Constructors  
* 9.1classการใช้งานเสมอ หลีกเลี่ยงการจัดการprototypeโดยตรง   

        // bad
        function Queue(contents = []) {
        this.queue = [...contents];
        }
        Queue.prototype.pop = function () {
        const value = this.queue[0];
        this.queue.splice(0, 1);
        return value;
        };

        // good
        class Queue {
        constructor(contents = []) {
            this.queue = [...contents];
        }
        pop() {
            const value = this.queue[0];
            this.queue.splice(0, 1);
            return value;
        }
        }  

* 9.2ใช้extendsสำหรับการสืบทอด  

        // bad
        const inherits = require('inherits');
        function PeekableQueue(contents) {
        Queue.apply(this, contents);
        }
        inherits(PeekableQueue, Queue);
        PeekableQueue.prototype.peek = function () {
        return this.queue[0];
        };

        // good
        class PeekableQueue extends Queue {
        peek() {
            return this.queue[0];
        }
        }    

* 9.3วิธีการสามารถกลับthisไปช่วยด้วยวิธีการผูกมัด  

        // bad
        Jedi.prototype.jump = function () {
        this.jumping = true;
        return true;
        };

        Jedi.prototype.setHeight = function (height) {
        this.height = height;
        };

        const luke = new Jedi();
        luke.jump(); // => true
        luke.setHeight(20); // => undefined

        // good
        class Jedi {
        jump() {
            this.jumping = true;
            return this;
        }

        setHeight(height) {
            this.height = height;
            return this;
        }
        }

        const luke = new Jedi();

        luke.jump()
        .setHeight(20);    

* 9.4ไม่สามารถเขียนtoString()วิธีการที่กำหนดเองได้เพียงตรวจสอบให้แน่ใจว่าทำงานได้สำเร็จและไม่มีผลข้างเคียง  

        class Jedi {
        constructor(options = {}) {
            this.name = options.name || 'no name';
        }

        getName() {
            return this.name;
        }

        toString() {
            return `Jedi - ${this.getName()}`;
        }
        }  

* 9.5คลาสมีคอนสตรัคเตอร์เริ่มต้นหากไม่ได้ระบุไว้ ฟังก์ชัน Constructor ที่ว่างเปล่าหรืออันที่เพิ่งมอบหมายให้คลาสผู้ปกครองนั้นไม่จำเป็น eslint:no-useless-constructor  

        // bad
        class Jedi {
        constructor() {}

        getName() {
            return this.name;
        }
        }

        // bad
        class Rey extends Jedi {
        constructor(...args) {
            super(...args);
        }
        }

        // good
        class Rey extends Jedi {
        constructor(...args) {
            super(...args);
            this.name = 'Rey';
        }
        }  

* 9.6หลีกเลี่ยงสมาชิกชั้นเรียน  

        // bad
        class Foo {
        bar() { return 1; }
        bar() { return 2; }
        }

        // good
        class Foo {
        bar() { return 1; }
        }

        // good
        class Foo {
        bar() { return 2; }
        }  

* 9.7วิธีการเรียนควรใช้thisหรือทำเป็นวิธีการคงที่เว้นแต่ห้องสมุดหรือกรอบภายนอกต้องใช้วิธีการไม่คงที่เฉพาะ เป็นวิธีการอินสแตนซ์ควรระบุว่ามันทำงานแตกต่างกันไปตามคุณสมบัติของผู้รับ eslint:class-methods-use-this  

        // bad
        class Foo {
        bar() {
            console.log('bar');
        }
        }

        // good - this is used
        class Foo {
        bar() {
            console.log(this.bar);
        }
        }

        // good - constructor is exempt
        class Foo {
        constructor() {
            // ...
        }
        }

        // good - static methods aren't expected to use this
        class Foo {
        static bar() {
            console.log('bar');
        }
        }  


# Modules  
* 10.1ใช้โมดูล ( import/ export) บนระบบโมดูลที่ไม่ได้มาตรฐานเสมอ คุณสามารถ transpile ระบบโมดูลที่คุณต้องการได้ตลอดเวลา  

        // bad
        const AirbnbStyleGuide = require('./AirbnbStyleGuide');
        module.exports = AirbnbStyleGuide.es6;

        // ok
        import AirbnbStyleGuide from './AirbnbStyleGuide';
        export default AirbnbStyleGuide.es6;

        // best
        import { es6 } from './AirbnbStyleGuide';
        export default es6;  

* 10.2อย่าใช้สัญลักษณ์แทนการนำเข้า  

        // bad
        import * as AirbnbStyleGuide from './AirbnbStyleGuide';

        // good
        import AirbnbStyleGuide from './AirbnbStyleGuide';  

* 10.3และอย่าส่งออกโดยตรงจากการนำเข้า  

        // bad
        // filename es6.js
        export { es6 as default } from './AirbnbStyleGuide';

        // good
        // filename es6.js
        import { es6 } from './AirbnbStyleGuide';
        export default es6;  

* 10.4นำเข้าจากเส้นทางในที่เดียวเท่านั้น eslint:no-duplicate-imports  

        // bad
        import foo from 'foo';
        // … some other imports … //
        import { named1, named2 } from 'foo';

        // good
        import foo, { named1, named2 } from 'foo';

        // good
        import foo, {
        named1,
        named2,
        } from 'foo';  

* 10.5อย่าส่งออกการผูกรวมที่ไม่แน่นอน eslint:import/no-mutable-exports  

        // bad
        let foo = 3;
        export { foo };

        // good
        const foo = 3;
        export { foo };  

* 10.6ในโมดูลที่มีการเอ็กซ์ปอร์ตเดี่ยวให้เลือกเอ็กซ์ปอร์ตดีฟอลต์มากกว่าการเอ็กซ์พอร์ตแบบมีชื่อ eslint:import/prefer-default-export  

        // bad
        export function foo() {}

        // good
        export default function foo() {}  

* 10.7ใส่ข้อความimportข้างต้นที่ไม่นำเข้าทั้งหมด eslint:import/first  

        // bad
        import foo from 'foo';
        foo.init();

        import bar from 'bar';

        // good
        import foo from 'foo';
        import bar from 'bar';

        foo.init();  

* 10.8การนำเข้าหลายบรรทัดควรได้รับการเยื้องเช่นอาร์เรย์หลายแถวและตัวอักษรของวัตถุ eslint:object-curly-newline  


        // bad
        import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

        // good
        import { 
        longNameA,
        longNameB,
        longNameC,
        longNameD,
        longNameE,
        } from 'path';  

* 10.9ไม่อนุญาตให้ใช้ไวยากรณ์ตัวโหลดของ Webpack ในคำสั่งการนำเข้าโมดูล eslint:import/no-webpack-loader-syntax  

        // bad
        import fooSass from 'css!sass!foo.scss';
        import barCss from 'style!css!bar.css';

        // good
        import fooSass from 'foo.scss';
        import barCss from 'bar.css';  

* 10.10อย่ารวมนามสกุลไฟล์ JavaScript ของ eslint:import/extensions  

        // bad
        import foo from './foo.js';
        import bar from './bar.jsx';
        import baz from './baz/index.jsx';

        // good
        import foo from './foo';
        import bar from './bar';
        import baz from './baz';  

# Iterators and Generators  
* 11.1อย่าใช้ตัววนซ้ำ ต้องการฟังก์ชั่นที่สูงกว่าของ JavaScript แทนการวนซ้ำเช่นfor-inหรือ for-ofeslint:no-iterator no-restricted-syntax    

    * ทำไม? สิ่งนี้บังคับใช้กฎที่ไม่เปลี่ยนรูปแบบของเรา การจัดการกับฟังก์ชั่นแท้ ๆ ที่ให้ผลตอบแทนนั้นง่ายกว่าที่จะให้เหตุผลมากกว่าผลข้างเคียง

     * ใช้map()/ every()/ filter()/ find()/ findIndex()/ reduce()/ some()/ ... เพื่อวนซ้ำอาร์เรย์และObject.keys()/ Object.values()/ Object.entries()เพื่อสร้างอาร์เรย์เพื่อให้คุณสามารถวนซ้ำวัตถุได้  

        const numbers = [1, 2, 3, 4, 5];

        // bad
        let sum = 0;
        for (let num of numbers) {
        sum += num;
        }
        sum === 15;

        // good
        let sum = 0;
        numbers.forEach((num) => {
        sum += num;
        });
        sum === 15;

        // best (use the functional force)
        const sum = numbers.reduce((total, num) => total + num, 0);
        sum === 15;

        // bad
        const increasedByOne = [];
        for (let i = 0; i < numbers.length; i++) {
        increasedByOne.push(numbers[i] + 1);
        }

        // good
        const increasedByOne = [];
        numbers.forEach((num) => {
        increasedByOne.push(num + 1);
        });

        // best (keeping it functional)
        const increasedByOne = numbers.map((num) => num + 1);  
* 11.2อย่าใช้เครื่องกำเนิดไฟฟ้าในตอนนี้

ทำไม? พวกมันไม่สามารถส่งผ่านไปยัง ES5 ได้ดี


* 11.3หากคุณต้องใช้เครื่องกำเนิดไฟฟ้าหรือหากคุณไม่สนใจคำแนะนำของเราตรวจสอบให้แน่ใจว่ามีการเว้นระยะลายเซ็นของฟังก์ชันอย่างเหมาะสม eslint:generator-star-spacing
     * ทำไม? functionและ*เป็นส่วนหนึ่งของคำหลักแนวคิดเดียวกัน - *ไม่ปรับปรุงสำหรับfunction, เป็นโครงสร้างที่ไม่ซ้ำกันที่แตกต่างจากfunction*function   


            // bad
            function * foo() {
            // ...
            }

            // bad
            const bar = function * () {
            // ...
            };

            // bad
            const baz = function *() {
            // ...
            };

            // bad
            const quux = function*() {
            // ...
            };

            // bad
            function*foo() {
            // ...
            }

            // bad
            function *foo() {
            // ...
            }

            // very bad
            function
            *
            foo() {
            // ...
            }

            // very bad
            const wat = function
            *
            () {
            // ...
            };

            // good
            function* foo() {
            // ...
            }

            // good
            const foo = function* () {
            // ...
            };  

# Properties  
* 12.1ใช้เครื่องหมายจุดเมื่อเข้าถึงคุณสมบัติ eslint:dot-notation  

        const luke = {
        jedi: true,
        age: 28,
        };

        // bad
        const isJedi = luke['jedi'];

        // good
        const isJedi = luke.jedi;  

*  12.2ใช้เครื่องหมายวงเล็บ[]เมื่อเข้าถึงคุณสมบัติที่มีตัวแปร  

        const luke = {
        jedi: true,
        age: 28,
        };

        function getProp(prop) {
        return luke[prop]; 
        }

        const isJedi = getProp('jedi');  

* 12.3ใช้ตัวดำเนินการการยกกำลัง**เมื่อคำนวณการยกกำลัง no-restricted-propertieseslint:  

        // bad
        const binary = Math.pow(2, 10);

        // good
        const binary = 2 ** 10;  

# Variables  
* 13.1ใช้constหรือletประกาศตัวแปรเสมอ การไม่ทำเช่นนั้นจะส่งผลให้เกิดตัวแปรส่วนกลาง เราต้องการหลีกเลี่ยงการสร้างเนมสเปซส่วนกลาง กัปตันแพลนเตือนเราว่า eslint:no-undef prefer-const  

        // bad
        superPower = new SuperPower();

        // good
        const superPower = new SuperPower();  

* 13.2ใช้หนึ่งconstหรือletประกาศต่อตัวแปรหรือการกำหนด eslint:one-var  

        // bad
        const items = getItems(),
            goSportsTeam = true,
            dragonball = 'z';

        // bad
        // (compare to above, and try to spot the mistake)
        const items = getItems(),
            goSportsTeam = true;
            dragonball = 'z';

        // good
        const items = getItems();
        const goSportsTeam = true;
        const dragonball = 'z';  

* 13.3กลุ่มของคุณทั้งหมดconstและกลุ่มแล้วทั้งหมดของคุณlets  

        // bad
        let i, len, dragonball,
            items = getItems(),
            goSportsTeam = true;

        // bad
        let i;
        const items = getItems();
        let dragonball;
        const goSportsTeam = true;
        let len;

        // good
        const goSportsTeam = true;
        const items = getItems();
        let dragonball;
        let i;
        let length;  

* 13.4กำหนดตัวแปรที่คุณต้องการ แต่วางไว้ในที่ที่เหมาะสม  

        // bad - unnecessary function call
        function checkName(hasName) {
        const name = getName();

        if (hasName === 'test') {
            return false;
        }

        if (name === 'test') {
            this.setName('');
            return false;
        }

        return name;
        }

        // good
        function checkName(hasName) {
        if (hasName === 'test') {
            return false;
        }

        const name = getName();

        if (name === 'test') {
            this.setName('');
            return false;
        }

        return name;
        }    

* 13.5ไม่ต้องกำหนดค่าลูกโซ่ eslint:no-multi-assign  

        // bad
        (function example() {
        // JavaScript interprets this as
        // let a = ( b = ( c = 1 ) );
        // The let keyword only applies to variable a; variables b and c become
        // global variables.
        let a = b = c = 1;
        }());

        console.log(a); // throws ReferenceError
        console.log(b); // 1
        console.log(c); // 1

        // good
        (function example() {
        let a = 1;
        let b = a;
        let c = a;
        }());

        console.log(a); // throws ReferenceError
        console.log(b); // throws ReferenceError
        console.log(c); // throws ReferenceError

        // the same applies for `const`  

* 13.6หลีกเลี่ยงการใช้การเพิ่มขึ้นและลดลงแบบไม่รวม ( ++, --) eslintno-plusplus  

        // bad

        const array = [1, 2, 3];
        let num = 1;
        num++;
        --num;

        let sum = 0;
        let truthyCount = 0;
        for (let i = 0; i < array.length; i++) {
        let value = array[i];
        sum += value;
        if (value) {
            truthyCount++;
        }
        }

        // good

        const array = [1, 2, 3];
        let num = 1;
        num += 1;
        num -= 1;

        const sum = array.reduce((a, b) => a + b, 0);
        const truthyCount = array.filter(Boolean).length;  

* 13.7หลีกเลี่ยงการแพร่กระจายก่อนหรือหลัง=ในการมอบหมาย หากการมอบหมายของคุณละเมิดmax-lenล้อมค่าใน parens operator-linebreakeslint  

        // bad
        const foo =
        superLongLongLongLongLongLongLongLongFunctionName();

        // bad
        const foo
        = 'superLongLongLongLongLongLongLongLongString';

        // good
        const foo = (
        superLongLongLongLongLongLongLongLongFunctionName()
        );

        // good
        const foo = 'superLongLongLongLongLongLongLongLongString';  

* 13.8ไม่อนุญาตให้ใช้ตัวแปรที่ไม่ได้ใช้ eslint:no-unused-vars  

        // bad

        var some_unused_var = 42;

        // Write-only variables are not considered as used.
        var y = 10;
        y = 5;

        // A read for a modification of itself is not considered as used.
        var z = 0;
        z = z + 1;

        // Unused function arguments.
        function getX(x, y) {
            return x;
        }

        // good

        function getXPlusY(x, y) {
        return x + y;
        }

        var x = 1;
        var y = a + 2;

        alert(getXPlusY(x, y));

        // 'type' is ignored even if unused because it has a rest property sibling.
        // This is a form of extracting an object that omits the specified keys.
        var { type, ...coords } = data;
        // 'coords' is now the 'data' object without its 'type' property.  

 # Hoisting  
 * 14.1 varการประกาศได้รับการยกขึ้นไปด้านบนของขอบเขตฟังก์ชั่นการปิดล้อมที่ใกล้เคียงที่สุด constและletการประกาศมีความสุขกับแนวคิดใหม่ที่เรียกว่าชั่วโซนตาย (TDZ) มันเป็นสิ่งสำคัญที่จะรู้ว่าทำไมtypeof ไม่มีความปลอดภัยอีกต่อไป  

        // we know this wouldn’t work (assuming there
        // is no notDefined global variable)
        function example() {
        console.log(notDefined); // => throws a ReferenceError
        }

        // creating a variable declaration after you
        // reference the variable will work due to
        // variable hoisting. Note: the assignment
        // value of `true` is not hoisted.
        function example() {
        console.log(declaredButNotAssigned); // => undefined
        var declaredButNotAssigned = true;
        }

        // the interpreter is hoisting the variable
        // declaration to the top of the scope,
        // which means our example could be rewritten as:
        function example() {
        let declaredButNotAssigned;
        console.log(declaredButNotAssigned); // => undefined
        declaredButNotAssigned = true;
        }

        // using const and let
        function example() {
        console.log(declaredButNotAssigned); // => throws a ReferenceError
        console.log(typeof declaredButNotAssigned); // => throws a ReferenceError
        const declaredButNotAssigned = true;
        }  

* 14.2การแสดงออกของฟังก์ชั่นไม่ระบุชื่อยกชื่อตัวแปรของพวกเขา แต่ไม่ใช่การกำหนดฟังก์ชั่น  

        function example() {
        console.log(anonymous); // => undefined

        anonymous(); // => TypeError anonymous is not a function

        var anonymous = function () {
            console.log('anonymous function expression');
        };
        }  

* 14.3การแสดงออกของฟังก์ชั่นที่มีชื่อยกชื่อตัวแปรไม่ใช่ชื่อฟังก์ชั่นหรือร่างกายฟังก์ชั่น  

        function example() {
        console.log(named); // => undefined

        named(); // => TypeError named is not a function

        superPower(); // => ReferenceError superPower is not defined

        var named = function superPower() {
            console.log('Flying');
        };
        }

        // the same is true when the function name
        // is the same as the variable name.
        function example() {
        console.log(named); // => undefined

        named(); // => TypeError named is not a function

        var named = function named() {
            console.log('named');
        };
        }  
* 14.4การประกาศฟังก์ชั่นยกชื่อและร่างกายของฟังก์ชั่น  

        function example() {
        superPower(); // => Flying

        function superPower() {
            console.log('Flying');
        }
        }  

# Comparison Operators & Equality  
  * 15.1การใช้===และ!==มากกว่าและ== !=eslint:eqeqeq

* 15.2คำสั่งแบบมีเงื่อนไขเช่นifคำสั่งประเมินการแสดงออกโดยใช้การข่มขู่ด้วยToBooleanวิธีนามธรรมและปฏิบัติตามกฎง่าย ๆ เหล่านี้เสมอ:

  * วัตถุประเมินเป็นจริง  
  * ไม่ได้กำหนดประเมินเป็นเท็จ  
  * Nullประเมินว่าเป็นเท็จ  
  * บูลีนประเมินมูลค่าของบูลีน  
  * ตัวเลขประเมินว่าเป็นเท็จถ้า+0, -0 หรือ NaNไม่เช่นนั้นจะเป็นจริง  
  * สตริงจะประเมินเป็น falseหากสตริงว่าง''มิฉะนั้นเป็นจริง  

        if ([0] && []) {
        // true
        // an array (even an empty one) is an object, objects will evaluate to true
        }  

* 15.3 ใช้ทางลัดสำหรับ booleans แต่เป็นการเปรียบเทียบสตริงและตัวเลขอย่างชัดเจน  


// เลว 

        // bad
        if (isValid === true) {
        // ...
        }

        // good
        if (isValid) {
        // ...
        }

        // bad
        if (name) {
        // ...
        }

        // good
        if (name !== '') {
        // ...
        }

        // bad
        if (collection.length) {
        // ...
        }

        // good
        if (collection.length > 0) {
        // ...
        }    

* 15.4สำหรับข้อมูลเพิ่มเติมดูความจริงที่เท่าเทียมกันและ JavaScriptโดย Angus Croll

* 15.5การใช้เครื่องหมายวงเล็บในการสร้างบล็อกในcaseและdefaultข้อที่มีการประกาศคำศัพท์ (เช่นlet, const, functionและclass) eslint:no-case-declarations  

        // bad
        switch (foo) {
        case 1:
            let x = 1;
            break;
        case 2:
            const y = 2;
            break;
        case 3:
            function f() {
            // ...
            }
            break;
        default:
            class C {}
        }

        // good
        switch (foo) {
        case 1: {
            let x = 1;
            break;
        }
        case 2: {
            const y = 2;
            break;
        }
        case 3: {
            function f() {
            // ...
            }
            break;
        }
        case 4:
            bar();
            break;
        default: {
            class C {}
        }
        }  

* 15.6 Ternaries ไม่ควรซ้อนกันและโดยทั่วไปจะเป็นนิพจน์บรรทัดเดียว eslint:no-nested-ternary  

        // bad
        const foo = maybe1 > maybe2
        ? "bar"
        : value1 > value2 ? "baz" : null;

        // split into 2 separated ternary expressions
        const maybeNull = value1 > value2 ? 'baz' : null;

        // better
        const foo = maybe1 > maybe2
        ? 'bar'
        : maybeNull;

        // best
        const foo = maybe1 > maybe2 ? 'bar' : maybeNull;  

* 15.7หลีกเลี่ยงคำที่ไม่จำเป็นแบบไตรภาค eslint:no-unneeded-ternary  

        // bad
        const foo = a ? a : b;
        const bar = c ? true : false;
        const baz = c ? false : true;

        // good
        const foo = a || b;
        const bar = !!c;
        const baz = !c;  

* 15.8เมื่อผสมตัวดำเนินการให้ใส่ไว้ในวงเล็บ ยกเว้นอย่างเดียวคือผู้ประกอบการทางคณิตศาสตร์มาตรฐาน+, -และ**เนื่องจากความสำคัญของพวกเขาเป็นที่เข้าใจกันในวงกว้าง เราแนะนำให้ปิด/และ*ในวงเล็บเพราะลำดับก่อนหน้าอาจคลุมเครือเมื่อผสม eslint:no-mixed-operators  

        // bad
        const foo = a && b < 0 || c > 0 || d + 1 === 0;

        // bad
        const bar = a ** b - 5 % d;

        // bad
        // one may be confused into thinking (a || b) && c
        if (a || b && c) {
        return d;
        }

        // bad
        const bar = a + b / c * d;

        // good
        const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

        // good
        const bar = a ** b - (5 % d);

        // good
        if (a || (b && c)) {
        return d;
        }

        // good
        const bar = a + (b / c) * d;  

# Blocks  
* 16.1ใช้เครื่องมือจัดฟันพร้อมกับบล็อกหลายเส้น eslint:nonblock-statement-body-position  

        // bad
        if (test)
        return false;

        // good
        if (test) return false;

        // good
        if (test) {
        return false;
        }

        // bad
        function foo() { return false; }

        // good
        function bar() {
        return false;
        }  

* 16.2หากคุณกำลังใช้บล็อกหลายเส้นด้วยifและelseให้วางelseบรรทัดเดียวกันกับifวงเล็บปีกกาปิดของบล็อก eslint:brace-style  

        // bad
        if (test) {
        thing1();
        thing2();
        }
        else {
        thing3();
        }

        // good
        if (test) {
        thing1();
        thing2();
        } else {
        thing3();
        }  

* 16.3หากifบล็อกเรียกใช้returnคำสั่งเสมอบล็อกที่ตามมาelseไม่จำเป็น A returnในelse ifบล็อกที่ตามหลังifบล็อกที่มี a returnสามารถแยกออกเป็นหลาย ๆifบล็อกได้ eslint:no-else-return  
  
        // bad
        function foo() {
        if (x) {
            return x;
        } else {
            return y;
        }
        }

        // bad
        function cats() {
        if (x) {
            return x;
        } else if (y) {
            return y;
        }
        }

        // bad
        function dogs() {
        if (x) {
            return x;
        } else {
            if (y) {
            return y;
            }
        }
        }

        // good
        function foo() {
        if (x) {
            return x;
        }

        return y;
        }

        // good
        function cats() {
        if (x) {
            return x;
        }

        if (y) {
            return y;
        }
        }

        // good
        function dogs(x) {
        if (x) {
            if (z) {
            return y;
            }
        } else {
            return z;
        }
        }  

# Control Statements  
* 17.1ในกรณีที่คำสั่งการควบคุมของคุณ ( if, whileฯลฯ ) ได้รับนานเกินไปหรือเกินกว่าความยาวสายสูงสุดที่แต่ละคน (จัดกลุ่ม) เงื่อนไขอาจจะใส่ลงไปในบรรทัดใหม่ ผู้ประกอบการตรรกะควรเริ่มต้นบรรทัด  

        // bad
        if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
        thing1();
        }

        // bad
        if (foo === 123 &&
        bar === 'abc') {
        thing1();
        }

        // bad
        if (foo === 123
        && bar === 'abc') {
        thing1();
        }

        // bad
        if (
        foo === 123 &&
        bar === 'abc'
        ) {
        thing1();
        }

        // good
        if (
        foo === 123
        && bar === 'abc'
        ) {
        thing1();
        }

        // good
        if (
        (foo === 123 || bar === 'abc')
        && doesItLookGoodWhenItBecomesThatLong()
        && isThisReallyHappening()
        ) {
        thing1();
        }

        // good
        if (foo === 123 && bar === 'abc') {
        thing1();
        }  

* 17.2อย่าใช้ตัวดำเนินการเลือกแทนคำสั่งควบคุม  

        // bad
        !isRunning && startRunning();

        // good
        if (!isRunning) {
        startRunning();
        }  

# Comments  
* 18.1ใช้/** ... */สำหรับความคิดเห็นหลายบรรทัด  

        // bad
        // make() returns a new element
        // based on the passed in tag name
        //
        // @param {String} tag
        // @return {Element} element
        function make(tag) {

        // ...

        return element;
        }

        // good
        /**
        * make() returns a new element
        * based on the passed-in tag name
        */
        function make(tag) {

        // ...

        return element;
        }  

* 18.2ใช้//สำหรับความคิดเห็นบรรทัดเดียว วางความคิดเห็นบรรทัดเดียวในบรรทัดใหม่เหนือเรื่องของความคิดเห็น ใส่บรรทัดว่างข้างหน้าความคิดเห็นเว้นแต่ว่าจะอยู่ในบรรทัดแรกของบล็อก  

        // bad
        const active = true;  // is current tab

        // good
        // is current tab
        const active = true;

        // bad
        function getType() {
        console.log('fetching type...');
        // set the default type to 'no type'
        const type = this.type || 'no type';

        return type;
        }

        // good
        function getType() {
        console.log('fetching type...');

        // set the default type to 'no type'
        const type = this.type || 'no type';

        return type;
        }

        // also good
        function getType() {
        // set the default type to 'no type'
        const type = this.type || 'no type';

        return type;
        }  

* 18.3เริ่มความคิดเห็นทั้งหมดด้วยช่องว่างเพื่อให้อ่านง่ายขึ้น eslint:spaced-comment  

        // bad
        //is current tab
        const active = true;

        // good
        // is current tab
        const active = true;

        // bad
        /**
        *make() returns a new element
        *based on the passed-in tag name
        */
        function make(tag) {

        // ...

        return element;
        }

        // good
        /**
        * make() returns a new element
        * based on the passed-in tag name
        */
        function make(tag) {

        // ...

        return element;
        }  

* 18.4คำนำหน้าความคิดเห็นของคุณด้วยFIXMEหรือTODOช่วยให้ผู้พัฒนารายอื่นเข้าใจได้อย่างรวดเร็วว่าคุณกำลังชี้ให้เห็นปัญหาที่ต้องได้รับการแก้ไขอีกครั้งหรือหากคุณแนะนำวิธีแก้ไขปัญหาที่ต้องนำไปปฏิบัติ สิ่งเหล่านี้แตกต่างจากความคิดเห็นทั่วไปเนื่องจากสามารถดำเนินการได้ การกระทำที่มีหรือFIXME: -- need to figure this outTODO: -- need to implement  


* 18.5ใช้// FIXME:เพื่ออธิบายปัญหา  

        class Calculator extends Abacus {
        constructor() {
            super();

            // FIXME: shouldn’t use a global here
            total = 0;
        }
        }  

* 18.6ใช้// TODO:เพื่ออธิบายวิธีแก้ไขปัญหา    

        class Calculator extends Abacus {
        constructor() {
            super();

            // TODO: total should be configurable by an options param
            this.total = 0;
        }
        }  

# Whitespace  
* 19.1ใช้แท็บนุ่ม (อักขระเว้นวรรค) ตั้งค่าเป็น 2 ช่องว่าง eslint:indent  

        // bad
        function foo() {
        ∙∙∙∙let name;
        }

        // bad
        function bar() {
        ∙let name;
        }

        // good
        function baz() {
        ∙∙let name;
        }  

* 19.2 วาง 1 ช่องว่างไว้ข้างหน้ารั้ง eslint:space-before-blocks  

        // bad
        function test(){
        console.log('test');
        }

        // good
        function test() {
        console.log('test');
        }

        // bad
        dog.set('attr',{
        age: '1 year',
        breed: 'Bernese Mountain Dog',
        });

        // good
        dog.set('attr', {
        age: '1 year',
        breed: 'Bernese Mountain Dog',
        });      

* 19.3สถานที่ 1 พื้นที่ก่อนที่จะวงเล็บเปิดในงบการควบคุม ( if, whileฯลฯ ) ไม่มีที่ว่างระหว่างรายการอาร์กิวเมนต์และชื่อฟังก์ชันในการเรียกใช้ฟังก์ชันและการประกาศ eslint:keyword-spacing  

        // bad
        if(isJedi) {
        fight ();
        }

        // good
        if (isJedi) {
        fight();
        }

        // bad
        function fight () {
        console.log ('Swooosh!');
        }

        // good
        function fight() {
        console.log('Swooosh!');
        }  

* 19.4กำหนดตัวดำเนินการที่มีช่องว่าง eslint:space-infix-ops  

        // bad
        const x=y+5;

        // good
        const x = y + 5;  

* 19.5สิ้นสุดไฟล์ด้วยอักขระบรรทัดใหม่หนึ่งบรรทัด eslint:eol-last  

        // bad
        import { es6 } from './AirbnbStyleGuide';
        // ...
        export default es6;  

         // bad
        import { es6 } from './AirbnbStyleGuide';
        // ...
        export default es6;↵
        ↵  

        // good
        import { es6 } from './AirbnbStyleGuide';
        // ...
        export default es6;↵  

* 19.6ใช้การเยื้องเมื่อสร้างเชนเมธอดแบบยาว (เชนเมธอดมากกว่า 2 วิธี) ใช้จุดนำหน้าซึ่งเน้นว่าบรรทัดนั้นเป็นการเรียกเมธอดไม่ใช่ข้อความใหม่ eslint:newline-per-chained-call no-whitespace-before-property  

        // bad
        $('#items').find('.selected').highlight().end().find('.open').updateCount();

        // bad
        $('#items').
        find('.selected').
            highlight().
            end().
        find('.open').
            updateCount();

        // good
        $('#items')
        .find('.selected')
            .highlight()
            .end()
        .find('.open')
            .updateCount();

        // bad
        const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
            .attr('width', (radius + margin) * 2).append('svg:g')
            .attr('transform', `translate(${radius + margin},${radius + margin})`)
            .call(tron.led);

        // good
        const leds = stage.selectAll('.led')
            .data(data)
        .enter().append('svg:svg')
            .classed('led', true)
            .attr('width', (radius + margin) * 2)
        .append('svg:g')
            .attr('transform', `translate(${radius + margin},${radius + margin})`)
            .call(tron.led);

        // good
        const leds = stage.selectAll('.led').data(data);  


* 19.7ปล่อยให้บรรทัดว่างหลังบล็อกและก่อนหน้าคำสั่งถัดไป  

        // bad
        if (foo) {
        return bar;
        }
        return baz;

        // good
        if (foo) {
        return bar;
        }

        return baz;

        // bad
        const obj = {
        foo() {
        },
        bar() {
        },
        };
        return obj;

        // good
        const obj = {
        foo() {
        },

        bar() {
        },
        };

        return obj;

        // bad
        const arr = [
        function foo() {
        },
        function bar() {
        },
        ];
        return arr;

        // good
        const arr = [
        function foo() {
        },

        function bar() {
        },
        ];

        return arr;  

* 19.8ห้ามวางแผ่นบล็อกของคุณด้วยบรรทัดว่าง eslint:padded-blocks  

        // bad
        function bar() {

        console.log(foo);

        }

        // bad
        if (baz) {

        console.log(qux);
        } else {
        console.log(foo);

        }

        // bad
        class Foo {

        constructor(bar) {
            this.bar = bar;
        }
        }

        // good
        function bar() {
        console.log(foo);
        }

        // good
        if (baz) {
        console.log(qux);
        } else {
        console.log(foo);
        }  

* 19.9อย่าใช้ช่องว่างหลายบรรทัดเพื่อวางรหัสของคุณ eslint:no-multiple-empty-lines  

        // bad
        class Person {
        constructor(fullName, email, birthday) {
            this.fullName = fullName;


            this.email = email;


            this.setAge(birthday);
        }


        setAge(birthday) {
            const today = new Date();


            const age = this.getAge(today, birthday);


            this.age = age;
        }


        getAge(today, birthday) {
            // ..
        }
        }

        // good
        class Person {
        constructor(fullName, email, birthday) {
            this.fullName = fullName;
            this.email = email;
            this.setAge(birthday);
        }

        setAge(birthday) {
            const today = new Date();
            const age = getAge(today, birthday);
            this.age = age;
        }

        getAge(today, birthday) {
            // ..
        }
        }  

* 19.10อย่าเพิ่มช่องว่างภายในวงเล็บ eslint:space-in-parens  

        // bad
        function bar( foo ) {
        return foo;
        }

        // good
        function bar(foo) {
        return foo;
        }

        // bad
        if ( foo ) {
        console.log(foo);
        }

        // good
        if (foo) {
        console.log(foo);
        }  

* 19.11ห้ามเพิ่มช่องว่างในวงเล็บ eslint:array-bracket-spacing  

        // bad
        const foo = [ 1, 2, 3 ];
        console.log(foo[ 0 ]);

        // good
        const foo = [1, 2, 3];
        console.log(foo[0]);  

* 19.12เพิ่มช่องว่างภายในเครื่องหมายปีกกา eslint:object-curly-spacing  

        // bad
        const foo = {clark: 'kent'};

        // good
        const foo = { clark: 'kent' };  

* 19.13หลีกเลี่ยงบรรทัดของรหัสที่มีความยาวเกิน 100 อักขระ (รวมถึงช่องว่าง) หมายเหตุ: ต่อไปนี้สตริงที่ยาวได้รับการยกเว้นจากกฎนี้และไม่ควรทำลาย eslint:max-len  

        // bad
        const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

        // bad
        $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

        // good
        const foo = jsonData
        && jsonData.foo
        && jsonData.foo.bar
        && jsonData.foo.bar.baz
        && jsonData.foo.bar.baz.quux
        && jsonData.foo.bar.baz.quux.xyzzy;

        // good
        $.ajax({
        method: 'POST',
        url: 'https://airbnb.com/',
        data: { name: 'John' },
        })
        .done(() => console.log('Congratulations!'))
        .fail(() => console.log('You have failed this city.'));  

* 19.14ต้องใช้ระยะห่างที่สอดคล้องกันภายในโทเค็นบล็อกแบบเปิดและโทเค็นถัดไปในบรรทัดเดียวกัน กฎนี้ยังบังคับให้มีการเว้นวรรคที่สอดคล้องภายในโทเค็นปิดบล็อกและโทเค็นก่อนหน้าในบรรทัดเดียวกัน eslint:block-spacing    

        // bad
        function foo() {return true;}
        if (foo) { bar = 0;}

        // good
        function foo() { return true; }
        if (foo) { bar = 0; }  

* 19.15หลีกเลี่ยงช่องว่างก่อนเครื่องหมายจุลภาคและต้องเว้นวรรคหลังเครื่องหมายจุลภาค eslint:comma-spacing   

        // bad
        var foo = 1,bar = 2;
        var arr = [1 , 2];

        // good
        var foo = 1, bar = 2;
        var arr = [1, 2];  

* 19.16บังคับใช้ระยะห่างภายในวงเล็บเหลี่ยมที่คำนวณได้ eslint:computed-property-spacing  

        // bad
        obj[foo ]
        obj[ 'foo']
        var x = {[ b ]: a}
        obj[foo[ bar ]]

        // good
        obj[foo]
        obj['foo']
        var x = { [b]: a }
        obj[foo[bar]]  

* 19.17หลีกเลี่ยงช่องว่างระหว่างฟังก์ชั่นและการเรียกใช้ eslint:func-call-spacing  

        // bad
        func ();

        func
        ();

        // good
        func();  

* 19.18บังคับใช้ระยะห่างระหว่างคีย์และค่าในคุณสมบัติตามตัวอักษรของวัตถุ eslint:key-spacing  

        // bad
        var obj = { foo : 42 };
        var obj2 = { foo:42 };

        // good
        var obj = { foo: 42 };  

* 19.19หลีกเลี่ยงช่องว่างท้ายท้ายบรรทัด eslint:no-trailing-spaces  

* 19.20หลีกเลี่ยงบรรทัดว่างหลายบรรทัดอนุญาตหนึ่งบรรทัดใหม่ที่ส่วนท้ายของไฟล์และหลีกเลี่ยงบรรทัดใหม่ที่จุดเริ่มต้นของไฟล์ eslint:no-multiple-empty-lines

        // bad - multiple empty lines
        var x = 1;


        var y = 2;

        // bad - 2+ newlines at end of file
        var x = 1;
        var y = 2;


        // bad - 1+ newline(s) at beginning of file

        var x = 1;
        var y = 2;

        // good
        var x = 1;
        var y = 2;  

# Commas  
* 20.1จุลภาคชั้นนำ: ไม่ eslint:comma-style   

        // bad
        const story = [
            once
        , upon
        , aTime
        ];

        // good
        const story = [
        once,
        upon,
        aTime,
        ];

        // bad
        const hero = {
            firstName: 'Ada'
        , lastName: 'Lovelace'
        , birthYear: 1815
        , superPower: 'computers'
        };

        // good
        const hero = {
        firstName: 'Ada',
        lastName: 'Lovelace',
        birthYear: 1815,
        superPower: 'computers',
        };  

* 20.2จุลภาคต่อท้ายเพิ่มเติม: Yup eslint:comma-dangle 

                // bad - git diff without trailing comma
                const hero = {
                    firstName: 'Florence',
                -    lastName: 'Nightingale'
                +    lastName: 'Nightingale',
                +    inventorOf: ['coxcomb chart', 'modern nursing']
                };

                // good - git diff with trailing comma
                const hero = {
                    firstName: 'Florence',
                    lastName: 'Nightingale',
                +    inventorOf: ['coxcomb chart', 'modern nursing'],
                };   

        // bad
        const hero = {
        firstName: 'Dana',
        lastName: 'Scully'
        };

        const heroes = [
        'Batman',
        'Superman'
        ];

        // good
        const hero = {
        firstName: 'Dana',
        lastName: 'Scully',
        };

        const heroes = [
        'Batman',
        'Superman',
        ];

        // bad
        function createHero(
        firstName,
        lastName,
        inventorOf
        ) {
        // does nothing
        }

        // good
        function createHero(
        firstName,
        lastName,
        inventorOf,
        ) {
        // does nothing
        }

        // good (note that a comma must not appear after a "rest" element)
        function createHero(
        firstName,
        lastName,
        inventorOf,
        ...heroArgs
        ) {
        // does nothing
        }

        // bad
        createHero(
        firstName,
        lastName,
        inventorOf
        );

        // good
        createHero(
        firstName,
        lastName,
        inventorOf,
        );

        // good (note that a comma must not appear after a "rest" element)
        createHero(
        firstName,
        lastName,
        inventorOf,
        ...heroArgs
        );  

# Semicolons  
* 21.1 Yup. eslint:semi  
        // bad - raises exception
        const luke = {}
        const leia = {}
        [luke, leia].forEach((jedi) => jedi.father = 'vader')

        // bad - raises exception
        const reaction = "No! That’s impossible!"
        (async function meanwhileOnTheFalcon() {
        // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
        // ...
        }())

        // bad - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
        function foo() {
        return
            'search your feelings, you know it to be foo'
        }

        // good
        const luke = {};
        const leia = {};
        [luke, leia].forEach((jedi) => {
        jedi.father = 'vader';
        });

        // good
        const reaction = "No! That’s impossible!";
        (async function meanwhileOnTheFalcon() {
        // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
        // ...
        }());

        // good
        function foo() {
        return 'search your feelings, you know it to be foo';
        }  

# Type Casting & Coercion  
* 22.1ดำเนินการบังคับประเภทที่จุดเริ่มต้นของคำสั่ง

* 22.2สตริง: eslint:no-new-wrappers  

        // => this.reviewScore = 9;

        // bad
        const totalScore = new String(this.reviewScore); // typeof totalScore is "object" not "string"

        // bad
        const totalScore = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

        // bad
        const totalScore = this.reviewScore.toString(); // isn’t guaranteed to return a string

        // good
        const totalScore = String(this.reviewScore);  

* 22.3หมายเลข: ใช้NumberสำหรับการคัดเลือกนักแสดงประเภทและparseIntมักจะมี Radix สำหรับการแยกสตริง eslint:radix no-new-wrappers  

        const inputValue = '4';

        // bad
        const val = new Number(inputValue);

        // bad
        const val = +inputValue;

        // bad
        const val = inputValue >> 0;

        // bad
        const val = parseInt(inputValue);

        // good
        const val = Number(inputValue);

        // good
        const val = parseInt(inputValue, 10);  

* 22.4หากมีเหตุผลสิ่งที่คุณกำลังทำสิ่งที่ป่าและparseIntเป็นคอขวดและความจำเป็นที่จะใช้ Bitshift สำหรับเหตุผลประสิทธิภาพออกความคิดเห็นการอธิบายว่าทำไมและสิ่งที่คุณกำลังทำ  

        // good
        /**
        * parseInt was the reason my code was slow.
        * Bitshifting the String to coerce it to a
        * Number made it a lot faster.
        */
        const val = inputValue >> 0;  
* 22.5 หมายเหตุ:โปรดใช้ความระมัดระวังเมื่อใช้การดำเนินการ bitshift ตัวเลขถูกแสดงเป็นค่า64- บิตแต่การดำเนินการของ bithift จะส่งคืนจำนวนเต็ม 32- บิตเสมอ ( แหล่งที่มา ) Bitshift สามารถนำไปสู่พฤติกรรมที่ไม่คาดคิดสำหรับค่าจำนวนเต็มมากกว่า 32 บิต การสนทนา Int 32-bit ที่มีการลงชื่อมากที่สุดคือ 2,147,483,647:  

        2147483647 >> 0; // => 2147483647
        2147483648 >> 0; // => -2147483648
        2147483649 >> 0; // => -2147483647  

* 22.6 Booleans: eslint:no-new-wrappers  

        const age = 0;

        // bad
        const hasAge = new Boolean(age);

        // good
        const hasAge = Boolean(age);

        // best
        const hasAge = !!age;  

# Naming Conventions  
* 23.1หลีกเลี่ยงชื่อตัวอักษรเดียว อธิบายด้วยการตั้งชื่อของคุณ eslint:id-length  

        // bad
        function q() {
        // ...
        }

        // good
        function query() {
        // ...
        }   

* 23.2ใช้ camelCase เมื่อตั้งชื่อวัตถุฟังก์ชั่นและอินสแตนซ์ eslint:camelcase  

        // bad
        const OBJEcttsssss = {};
        const this_is_my_object = {};
        function c() {}

        // good
        const thisIsMyObject = {};
        function thisIsMyFunction() {}  

* 23.3ใช้ PascalCase เฉพาะเมื่อตั้งชื่อตัวสร้างหรือคลาส eslint:new-cap  

        // bad
        function user(options) {
        this.name = options.name;
        }

        const bad = new user({
        name: 'nope',
        });

        // good
        class User {
        constructor(options) {
            this.name = options.name;
        }
        }

        const good = new User({
        name: 'yup',
        });  

* 23.4อย่าใช้การต่อท้ายหรือขีดล่าง eslint:no-underscore-dangle  

        // bad
        this.__firstName__ = 'Panda';
        this.firstName_ = 'Panda';
        this._firstName = 'Panda';

        // good
        this.firstName = 'Panda';

        // good, in environments where WeakMaps are available
        // see https://kangax.github.io/compat-table/es6/#test-WeakMap
        const firstNames = new WeakMap();
        firstNames.set(this, 'Panda');  

* 23.5thisไม่ได้บันทึกการอ้างอิงถึง ใช้ลูกศรฟังก์ชั่นหรือฟังก์ชั่น # ผูก   

        // bad
        function foo() {
        const self = this;
        return function () {
            console.log(self);
        };
        }

        // bad
        function foo() {
        const that = this;
        return function () {
            console.log(that);
        };
        }

        // good
        function foo() {
        return () => {
            console.log(this);
        };
        }  

        * 23.6ชื่อไฟล์พื้นฐานควรตรงกับชื่อของการส่งออกเริ่มต้น  

        // file 1 contents
        class CheckBox {
        // ...
        }
        export default CheckBox;

        // file 2 contents
        export default function fortyTwo() { return 42; }

        // file 3 contents
        export default function insideDirectory() {}

        // in some other file
        // bad
        import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
        import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
        import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

        // bad
        import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
        import forty_two from './forty_two'; // snake_case import/filename, camelCase export
        import inside_directory from './inside_directory'; // snake_case import, camelCase export
        import index from './inside_directory/index'; // requiring the index file explicitly
        import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

        // good
        import CheckBox from './CheckBox'; // PascalCase export/import/filename
        import fortyTwo from './fortyTwo'; // camelCase export/import/filename
        import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
        // ^ supports both insideDirectory.js and insideDirectory/index.js  

* 23.7ใช้ camelCase เมื่อคุณส่งออกฟังก์ชั่นเริ่มต้น ชื่อไฟล์ของคุณควรเหมือนกับชื่อฟังก์ชันของคุณ  

        function makeStyleGuide() {
        // ...
        }

        export default makeStyleGuide;  

* 23.8ใช้ PascalCase เมื่อคุณส่งออก constructor / class / singleton / function library / วัตถุเปล่า  

        const AirbnbStyleGuide = {
        es6: {
        },
        };

        export default AirbnbStyleGuide;  

* 23.9 ตัวย่อและการเริ่มต้นควรเป็นตัวพิมพ์ใหญ่หรือตัวพิมพ์เล็กทั้งหมดเสมอ  

        // bad
        import SmsContainer from './containers/SmsContainer';

        // bad
        const HttpRequests = [
        // ...
        ];

        // good
        import SMSContainer from './containers/SMSContainer';

        // good
        const HTTPRequests = [
        // ...
        ];

        // also good
        const httpRequests = [
        // ...
        ];

        // best
        import TextMessageContainer from './containers/TextMessageContainer';

        // best
        const requests = [
        // ...
        ];
* 23.10คุณอาจเลือกตัวพิมพ์ใหญ่คงที่ก็ต่อเมื่อมัน (1) ถูกส่งออก (2) เป็นconst(มันไม่สามารถกำหนดใหม่ได้) และ (3) โปรแกรมเมอร์สามารถเชื่อถือได้ (และคุณสมบัติที่ซ้อนกัน) จะไม่เปลี่ยนแปลง  
    * constตัวแปรทั้งหมดเป็นอย่างไร? - สิ่งนี้ไม่จำเป็นดังนั้นจึงไม่ควรใช้ตัวพิมพ์ใหญ่สำหรับค่าคงที่ภายในไฟล์ ควรใช้สำหรับค่าคงที่ที่ส่งออกอย่างไรก็ตาม  
    * สิ่งที่เกี่ยวกับวัตถุที่ส่งออก? - ตัวพิมพ์ใหญ่ที่ระดับสูงสุดของการส่งออก (เช่นEXPORTED_OBJECT.key) และยืนยันว่าคุณสมบัติที่ซ้อนกันทั้งหมดจะไม่เปลี่ยนแปลง  

            // bad
            const PRIVATE_VARIABLE = 'should not be unnecessarily uppercased within a file';

            // bad
            export const THING_TO_BE_CHANGED = 'should obviously not be uppercased';

            // bad
            export let REASSIGNABLE_VARIABLE = 'do not use let with uppercase variables';

            // ---

            // allowed but does not supply semantic value
            export const apiKey = 'SOMEKEY';

            // better in most cases
            export const API_KEY = 'SOMEKEY';

            // ---

            // bad - unnecessarily uppercases key while adding no semantic value
            export const MAPPING = {
            KEY: 'value'
            };

            // good
            export const MAPPING = {
            key: 'value'
            };  

# accessors  
* 24.1ไม่จำเป็นต้องใช้ฟังก์ชั่น Accessor สำหรับคุณสมบัติ

* 24.2อย่าใช้ JavaScript getters / setters เพราะจะทำให้เกิดผลข้างเคียงที่ไม่คาดคิดและยากต่อการทดสอบบำรุงรักษาและเหตุผล แต่ถ้าคุณจะทำให้ฟังก์ชั่นการเข้าถึงการใช้งานและgetVal()setVal('hello')  

        // bad
        class Dragon {
        get age() {
            // ...
        }

        set age(value) {
            // ...
        }
        }

        // good
        class Dragon {
        getAge() {
            // ...
        }

        setAge(value) {
            // ...
        }
        }  




*  24.3ถ้าคุณสมบัติ / วิธีการคือbooleanใช้หรือisVal()hasVal()    

        // bad
        if (!dragon.age()) {
        return false;
        }

        // good
        if (!dragon.hasAge()) {
        return false;
        }  

* 24.4มันก็โอเคในการสร้างget()และset()ฟังก์ชั่น แต่ต้องสอดคล้องกัน    

        class Jedi {
        constructor(options = {}) {
            const lightsaber = options.lightsaber || 'blue';
            this.set('lightsaber', lightsaber);
        }

        set(key, val) {
            this[key] = val;
        }

        get(key) {
            return this[key];
        }
        }
# เหตุการณ์ที่เกิดขึ้น   
* 25.1เมื่อทำการแนบข้อมูลไปยังเหตุการณ์ (ไม่ว่าจะเป็นเหตุการณ์ DOM หรือบางอย่างที่เป็นกรรมสิทธิ์มากกว่าเช่นเหตุการณ์ Backbone) ให้ส่งวัตถุตามตัวอักษร (หรือที่เรียกว่า "แฮช") แทนค่าดิบ สิ่งนี้จะช่วยให้ผู้มีส่วนร่วมในภายหลังเพิ่มข้อมูลเพิ่มเติมให้กับส่วนของเหตุการณ์โดยไม่ต้องค้นหาและอัปเดตตัวจัดการทุกตัวสำหรับเหตุการณ์ ตัวอย่างเช่นแทนที่จะเป็น:  

        // bad
        $(this).trigger('listingUpdated', listing.id);

        // ...

        $(this).on('listingUpdated', (e, listingID) => {
        // do something with listingID
        });  

prefer:  

        // good
        $(this).trigger('listingUpdated', { listingID: listing.id });

        // ...

        $(this).on('listingUpdated', (e, data) => {
        // do something with data.listingID
        });  

# jQuery  
* 26.1ตัวแปรวัตถุคำนำหน้า $  

        // bad
        const sidebar = $('.sidebar');

        // good
        const $sidebar = $('.sidebar');

        // good
        const $sidebarBtn = $('.sidebar-btn');  

* 26.2 การค้นหาแคช jQuery  

        // bad
        function setSidebar() {
        $('.sidebar').hide();

        // ...

        $('.sidebar').css({
            'background-color': 'pink',
        });
        }

        // good
        function setSidebar() {
        const $sidebar = $('.sidebar');
        $sidebar.hide();

        // ...

        $sidebar.css({
            'background-color': 'pink',
        });
        }  

* 26.3สำหรับการค้นหา DOM ใช้ Cascading $('.sidebar ul')หรือผู้ปกครอง> $('.sidebar > ul')เด็ก jsPerf  


* 26.4ใช้findกับแบบสอบถามวัตถุ jQuery ที่มีการกำหนดขอบเขต  


        // bad
        $('ul', '.sidebar').hide();

        // bad
        $('.sidebar').find('ul').hide();

        // good
        $('.sidebar ul').hide();

        // good
        $('.sidebar > ul').hide();

        // good
        $sidebar.find('ul').hide();  

# ECMAScript 5 Compatibility  
* 27.1อ้างถึงKangax ES5 ‘s ตารางการทำงานร่วมกัน  
# ECMAScript 6+ (ES 2015+) Styles  

# Standard Library  
###  มาตรฐานห้องสมุด มีระบบสาธารณูปโภคที่จะแบ่งหน้าที่ แต่ยังคงด้วยเหตุผลมรดก  
* 29.1ใช้แทนทั่วโลกNumber.isNaN isNaNeslint:no-restricted-globals  

        // bad
        isNaN('1.2'); // false
        isNaN('1.2.3'); // true

        // good
        Number.isNaN('1.2.3'); // false
        Number.isNaN(Number('1.2.3')); // true  

* 29.2ใช้แทนทั่วโลกNumber.isFinite isFiniteeslint:no-restricted-globals  

        // bad
        isFinite('2e3'); // true

        // good
        Number.isFinite('2e3'); // false
        Number.isFinite(parseInt('2e3', 10)); // true  

# Testing  
* 30.2 No, but seriously:  
   * Whichever testing framework you use, you should be writing tests!  
   * Strive to write many small pure functions, and minimize where mutations occur.
Be cautious about stubs and mocks - they can make your tests more brittle.  
   * We primarily use mocha and jest at Airbnb. tape is also used occasionally for small, separate modules.  
   * 100% test coverage is a good goal to strive for, even if it’s not always practical to reach it.
   * Whenever you fix a bug, write a regression test. A bug fixed without a regression test is almost certainly going to break again in the future.  




















                                                                




