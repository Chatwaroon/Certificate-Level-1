# การใช้ Jest เพื่อทดสอบ TDD ใน Angular  
TDD สำคัญอย่างไร?? และทำไมเราต้องใช้ Jest?!?  

## TDD คืออะไร?  
### ก่อนที่เราจะมาทำความรู้จักกับ TDD ว่ามันคืออะไร…เรามาดูรูปข้างล่างนี้กันก่อนดีกว่า  
![](https://miro.medium.com/max/465/1*EHtjk4fxo79-gfUj7vIhRg.png)    
วิธีการวัดคุณภาพ Software ที่ดีที่สุด คือ การนับว่ามีคำอุทานหลุดออกมาจากปาก Developer จำนวนเท่าไรต่อนาที
เรื่องนี้มันเป็นเรื่องจริงมากๆ ที่บ่อยครั้งเหล่า Developer มักจะพูดคำอุทานออกมาดังๆ เพราะต้องเจอกับโค้ดที่ห่วย และมักมีความรู้สึกแบบนี้กับมันในทุกๆครั้ง(WTF) ซึ่งคุณสมบัติของการเขียนโค้ดที่ดีมันก็คือการเขียนอย่างไรให้มันเรียบง่ายที่สุด ซึ่งความเรียบง่ายนี่แหละมันทำยาก!!!  
![](https://miro.medium.com/max/500/1*YFmliZo9tgsC2By1IqCU8g.jpeg)  
ยกตัวอย่างในกรณีของบ้านก็เช่นกัน ตอนใหม่ๆมันก็ดูดี ทนทาน และแข็งแรง แต่พอเริ่มมีรอยร้าวของกำแพง เจ้าของบ้านกลับไม่ได้ใส่ใจหรือดูแลมัน ซึ่งไม่นานมันก็ค่อยๆมีส่วนอื่นของบ้านเสียหาย และทรุดโทรมลงไปเรื่อยๆ จนในที่สุดก็กลายเป็นเหมือนกับบ้านร้าง ซึ่งถ้าจะซ่อมแซมก็คงซ่อมไม่ไหว…มันตลกตรง Software ก็เป็นแบบนั้นเหมือนกัน Developer หลายคนถูกมอบหมายหน้าที่ให้ดูแลระบบที่เราไม่ได้เป็นคนเขียนมันขึ้นมา ซึ่งในโค้ดชุดนั้นก็อาจจะถูกเขียนมาดีบ้างหรือแย่บ้าง พอมี requirement ใหม่ๆเข้ามา แทนที่จะ refactor code เพื่อที่จะซ่อมแซมมัน แต่ก็เลือกที่จะปะผุพอให้มันใช้งานได้ เพื่อให้มันผ่านๆไป มันเลยกลายเป็นความใส่ใจในงานใหม่ๆมากกว่างานที่ต้องไปยุ่งกับโค้ดเก่าๆ พอเราทำแบบนั้นงานที่เราทำมันก็กลายเป็นเหมือนสัตว์ประหลาดที่เราสร้างมันขึ้นมา และส่งต่อไปให้คนดูแลคนต่อไป (legacy code)    
### เราจะแก้ปัญหาของการปะผุเหล่านี้ได้อย่างไร?  
เราสามารถใช้หลักการของการทำ Test Driven Development(TDD) ในการแก้ปัญหาเหล่านั้นได้ ซึ่งมันมีหลักการง่ายๆอยู่ประมาณ 3 ขั้นตอน
  
  ![](https://miro.medium.com/max/489/1*jFw7ZZMoVcsEYM_fS33DBA.gif)   
 ###  เริ่มต้นด้วยการเขียน Failing test…  
 เราจะยังไม่มี production code ซึ่งเราจะเริ่มจากการเขียน test ก่อน เพื่อพิสูจน์ให้มัน fail ตาม test ที่เราคิดไว้ว่ามันต้อง fail ซึ่งการเขียน test เราไม่จำเป็นที่จะต้องดักในทุกกรณี เพียงแต่เราเขียนให้มันพอเพียง และเพียงพอกับชิ้นงานในแต่ละชิ้นของเราก็พอ  
 ### เขียน Production code…  
 ขั้นตอนนี้เราจะเริ่มเขียน production code ซึ่งจะต้องทำให้ส่วนที่เราเขียน test ไว้ผ่านทั้งหมด โดยที่เราไม่จำเป็นที่จะต้องเขียน code ให้มันสวยหรูหรือดีเด่อะไรมากมาย ขอแค่ให้ test มันผ่านเท่านั้นก่อน  
 ### จัดการ Refactor code…  
 พอมาถึงขั้นตอนสุดท้ายก็จะง่าย เพราะโค้ดที่เราเขียนไว้ก่อนหน้านั้นเพื่อที่ให้มันรัน test ผ่าน ซึ่งมันจะเป็นโค้ดที่สั้นและง่ายพอที่เราจะนำเอาโค้ดตรงส่วนนั้นมาทำการจัดเรียงใหม่ ลดความซ้ำซ้อนลง หรือปรับ performance ของแอป หรือแม้แต่ปรับแต่ง UI
จาก 3 ขั้นตอนที่กล่าวมา มันจะเกิดการทำงานซ้ำๆ ก็คือ lifecycle ของ TDD นั่นเอง ซึ่งมันจะทำงานจบเป็นสัดส่วนตามชิ้นงาน และทำให้เรามองเห็น code ของเรานั้นเป็นกลุ่มก้อนซึ่งเรียกว่า modular มันทำให้เรามองดู code ได้สะอาดตา และตราบใดที่เรายังทำ test อยู่เราก็ไม่ต้องกลัวการแก้งานจากโค้ดเก่าอีกต่อไป…  
## TDD มีข้อดีอย่างไร?  
### ทำให้เราเขียนโค้ดที่จำเป็นเท่านั้น…  
เราจะเห็นว่าหลักการเขียนโค้ดของ TDD แค่ต้องการให้เราเขียนเพื่อให้รัน test ผ่าน และถ้าต้องการเพิ่ม feature หรืองานใหม่เข้าไป เราก็จะต้องเริ่มจากการเขียน test ก่อนเสมอ  

### การแก้ไขชิ้นงานจะทำได้ง่ายขึ้น…  
ทุกครั้งที่มีการเขียนโค้ดใหม่เข้าไป เราจะมั่นใจได้ว่าจะไม่กระทบกับงานเก่าหรือโค้ดเก่า เพราะมี test ที่ทำหน้าเป็นชุดทดสอบคอยตรวจเช็คความถูกต้องของระบบอยู่เสมอ ซึ่งจะช่วยลดความเสี่ยงของความผิดพลาดที่อาจเกิดขึ้นได้อย่างมากมายเลยทีเดียว  
###  ง่ายต่อการ Refactor Code…  
การเขียน test ก็เปรียบเสมือนกับเรามี document อยู่ในตัวระบบ ซึ่งถ้าเราต้องการที่จะ refactor code ตรงส่วนไหน ก็สามารถดูได้จาก test ที่สร้างไว้ ซึ่งจะทำให้เราเข้าใจระบบได้อย่างถ่องแท้มากขึ้น  
### เพิ่ม Test Coverage สูงขึ้น…  
ซึ่งเรามั่นใจได้ว่า test ที่เราเขียนนั้นมันครอบคลุมกรณีใดบ้าง และไม่ครอบคลุมกรณีใดบ้าง  
### Debug ง่ายแบบสุดๆ…  
เวลาที่เรารัน test ไม่ผ่าน เราจะสามารถรู้ได้ทันทีว่าส่วนไหนที่มันไม่ผ่าน โดยที่เราไม่ต้องมาเสียเวลากับการนั่งไล่โค้ดทั้งหมดเพื่อหาจุดบกพร่อง  
### ทำงานตาม Requirement…  
หัวใจของการทำ TDD อีกอย่างหนึ่ง คือ การให้ความสำคัญกับ requirement ของชิ้นงานเป็นพิเศษ ซึ่งจะทำให้การเขียนโค้ดของเรามีจุดยืนที่ชัดเจน เพราะถ้าเราเขียนโค้ดไม่ตรงตาม spec ที่กำหนด ก็จะรัน test ไม่ผ่าน  

## แล้วข้อเสียของ TDD ละมีบ้างไหม?  
ในช่วงแรกๆของการทำ TDD จะค่อนข้างช้า เนื่องจากเรายังไม่ชินกับความคิดที่ต้องคิดว่า “จะทำอะไร?…แล้วแก้ปัญหามันอย่างไร?…และจะเขียนมันอย่างไร?” ในบางครั้งเราอาจจะต้องใช้เวลาเพิ่มมากขึ้นกับงานที่เคยทำโดยใช้เวลาเพียงไม่นาน และบ่อยครั้งที่เราไม่เข้าใจปัญหาและเขียน test ทั้งๆที่ไม่เข้าใจ ส่งผลให้มันแทบไม่ได้ช่วยอะไรเราเลย แถมอาจจะส่งผลกับ production code ให้ผิดตามไปด้วยซะอีก…
สรุป…การทำงานแบบ TDD คือ การทำงานที่ต้องเริ่มจากการเขียน Specification ก่อนการเขียนโค้ดเสมอ แล้วเราค่อยมาโค้ดตาม spec ที่วางไว้ให้ผ่านก็ถือว่าจบ คิดง่ายๆการทำงานถ้าเราไม่ถาม requirement ของลูกค้า แล้วเราจะรู้ได้อย่างไรว่าเราควรทำงานอะไรส่งให้ลูกค้า….เหมือนกันกับ TDD ถ้าเราไม่กำหนด spec แล้วเราจะรู้ได้อย่างไรว่าโค้ดจริงๆที่เราควรเขียนต้องเขียนอะไร? แล้วมันเพียงพอต่อความต้องการของลูกค้าแล้วหรือยัง? …  
## TDD (Test Driven Development)  
เป็นแนวทางหนึ่งของการเขียนโค้ด นั่นคือคุณต้องเขียน test ก่อน ให้มัน Fail จากนั้นก็มาเขียนโค้ดให้ Pass ซึ่งในภาษาอังกฤษจะเรียกว่า the red-green approach  
## TDD จำเป็นจริงมั๊ย?   
   ข้อดีของ TDD คือ    

   * เขียนโค้ดเท่าที่จำเป็น เมื่อคุณเขียน Test ตามความต้องการหลักของงานแล้ว หน้าที่ของคุณคือทำ test ให้ผ่าน ไม่ต้องมาคิดว่าต้องเพิ่มอะไรรึเปล่า  
   * แก้งานได้ง่ายขึ้น ทำไมงานใช้ไม่ได้แล้วนะ มันผิดตรงไหนกัน??? ลองกลับไปดูที่ test กันอ๋อออออออ ผิดตรงนี้นี่เอง  
   * เพิ่ม test coverage การเขียน TDD ทำให้เรารู้ว่าเขียนครอบคลุมตรงไหนบ้าง รึขาดไปตรงไหน และ Jest ที่เราจะใช้ยังช่วยบอก test coverage ได้อย่างมีประสิทธิภาพด้วยน้าาา   
   * YAGNI หรือ You Are Not Gonna Need It เป็นแนวปฏิบัติที่จะนักพัฒนาจะไม่เพิ่มอะไรเข้าไปจนกว่ามันจะจำเป็นจริง ๆ แน่นอนคุณจะไม่พลาดสิ่งนี้เพราะ TDD จัดให้  

 สรุปก็คือ ทำตัวทดสอบ (Test) ก่อนการเขียนโค้ด (Coding) ตามสเปค (Specification) ของงาน ซึ่งการทำงานแบบนี้จะได้งานที่ตอบสนองความต้องการของลูกค้ามากขึ้น
ยังไม่ได้เริ่มโค้ดเลย จะรู้ได้ไงว่าต้องเทสตัวไหน
นี่ล่ะค่ะ ความท้าทายของ TDD ที่เราต้องเข้าใจอย่างถ่องแท้ว่างานต้องการอะไร เพื่อนำมาเขียนตัวทดสอบก่อนเริ่มงานแต่ละส่วน และเมื่อคุณทดสอบงานของคุณอยู่เสมอ คุณก็จะรู้ว่าจุดผิดพลาดอยู่ตรงไหน (ไม่ต้องปวดหัว ตามไล่เช็คโค้ดแล้ววววววว ^^)
  
  # ทำไมต้อง Jest ?  
  ![](https://miro.medium.com/max/500/1*0PRZrTnYn5mPUmU1iWXZOw.png)  
  ## Jest คือ  
  เครื่องมือเขียนทดสอบ (Testing) JavaScript Framework โดยผู้พัฒนาคือ Facebook
ซึ่งสามารถทำงานกับโปรเจกต์เช่น Babel, TypeScript, Node, React, Angular, Vue และอีกมากมาย  
## Jest ดียังไง?  
* เร็ว และปลอดภัย  
* snapshots testing ตรวจให้ว่า UI ของเราจะไม่เปลี่ยนไปกะทันหัน   
* การทดสอบจะทำงานแบบขนาน (Parallelized) ทำให้เพิ่มความเร็วในการทำงานอย่างมาก ที่สำคัญไม่ต้องใช้ browser เหมือน Karma ด้วยนะ  
* สามารถดู CODE COVERAGE ได้โดยไม่ต้องติดตั้งเพิ่ม  
* great API: Jest มีเครื่องมือทุกอย่างในที่เดียว และมี Document ที่ดี จึงใช้งานได้ง่าย
  
## มาดูกันว่าถ้าใช้ Jest ใน Angular จะเป็นยังไง  
![](https://miro.medium.com/max/700/1*zOkh_rm0CLd0Or_yeGuDOw.png)  
สิ่งแรกที่ต้องทำคือ ตรวจว่าในเครื่องของเรามี environment เพียงพอในการพัฒนา Angular รึยัง  
## ติดตั้ง Angular  
### สิ่งที่ต้องมี  
* node.js  
* npm จะมาพร้อมกับการติดตั้ง node.js  
### Check version เพื่อตรวจสอบว่ามีอยู่ในเครื่องรึไม่  
### node.js :
        node -v  

npm :  

        npm -v  

## ถ้าพร้อมแล้ว Let’s go!!  
1. ติดตั้ง the Angular CLI แบบ globally    

        npm install @angular/cli -g  

2. สร้าง Angular Application    

        ng new my-app  

หลังใช้คำสั่ง จะมีคำถามว่าจะเพิ่ม Angular routing หรือไม่ และใช้ style sheet แบบไหน  

![](https://miro.medium.com/max/630/1*DE34gL1MrKERurP0MavciA.png)  
ซึ่งในโปรเจกต์ตัวอย่าง จะเพิ่ม routing และใช้ style sheet แบบ Less  
3. หลัง Angular CLI สร้างโปรเจกต์เรียบร้อย ดูซิว่าใช้ได้จริงไหม?   
  
    cd my-app    ng serve

![](https://miro.medium.com/max/700/1*j7wQod1WJJpZBRgHtlf8Jw.png)  
หลังจากนี้เราจะมาเพิ่ม Jest ลงไป  

## ติดตั้ง Jest  
1. ติดตั้ง jest แบบ globally  

        npm install -g jest
เพื่อให้ Jest เป็น test runner เราจะใช้ jest-preset-angular ในการติดตั้ง ซึ่งจำเป็นจะต้อง config ตามรายละเอียดใน README.md มาเริ่มไปพร้อมกันเลย!  
2. ลง dependencies ทั้งหมดที่จำเป็น (จะใช้ npm หรือ yarn ก็ได้)    

            yarn add -D jest jest-preset-angular @types/jest
            # or
            npm install -D jest jest-preset-angular @types/jest  



3. สร้างไฟล์ setupJest.ts ในโฟลเดอร์ my-app/src โดยมี code ตามข้างล่าง   

        import 'jest-preset-angular';
        import './jestGlobalMocks'; // browser mocks globally available for every test
 4. สร้างไฟล์ jestGlobalMocks.ts ในโฟลเดอร์เดียวกันกับไฟล์ setupJest.ts  

        Object.defineProperty(window, 'CSS', {value: null});
        Object.defineProperty(document, 'doctype', {
        value: '<!DOCTYPE html>'
        });
        Object.defineProperty(window, 'getComputedStyle', {
        value: () => {
            return {
            display: 'none',
            appearance: ['-webkit-appearance']
            };
        }
        });
        /**
        * ISSUE: https://github.com/angular/material2/issues/7101
        * Workaround for JSDOM missing transform property
        */
        Object.defineProperty(document.body.style, 'transform', {
        value: () => {
            return {
            enumerable: true,
            configurable: true,
            };
        },
        });  

5. และเพิ่ม code นี้ลงใน package.json  

        {
        "jest": {
            "preset": "jest-preset-angular",
            "setupFilesAfterEnv": ["<rootDir>/src/setupJest.ts"]
        }
        }  

6. เปลี่ยนชื่อไฟล์src/test.ts เป็น src/karmaTest.ts เพื่อไม่ให้ Karma กับ Jest ทำงานทับซ้อนกัน  
![](https://miro.medium.com/max/427/1*mDFCdCva8xHcp-AGPaDq6w.png)  

7. เมื่อเราทำตามขั้นตอนครบแล้ว มาลองกัน  
![](https://miro.medium.com/max/700/1*HjZKXKEcL6CmGxJPKyOa8w.png)  
หลังจากที่เราติดตั้ง Jest ให้ทำงานบน Angular project ได้แล้ว ไปที่หัวข้อถัดไป  

## จับมารวมกันนนนนน!! (TDD Jest Angular)  
หัวข้อสุดท้ายก่อนนำไปใช้จริง เรามาลองสร้าง TDD ของตัวเองกันค่า
ซึ่งในหัวข้อนี้ จะอธิบายเพียงหลักการทำงานของ TDD ดังนั้นจะไม่ลงรายละเอียดในส่วนของ test case นะคะ
เริ่มแรกสร้าง component ในโปรเจกต์ขึ้นมาใหม  
่  
        ng g c favorite-animals
หลังจากสร้าง component มาแล้ว จะมีไฟล์ถูกสร้างมาในโฟลเดอร์ชื่อ favorite-animals อยู่ 4 ไฟล์นั่นคือ  
![](https://miro.medium.com/max/432/1*c6Aqc0rYqGt-AU-0TEZZMg.png)  
* favorite-animals.component.html (ไฟล์ html ของ component)  
* favorite-animals.component.less(ไฟล์ less ของ component) ซึ่งเป็นไปตาม style sheet ที่เลือกในตอนสร้าง angular  
* favorite-animals.component.spec.ts (ไฟล์ test ของ component)  
* favorite-animals.component.ts (ไฟล์ component หลัก)  

หลังจากได้ component มาแล้ว สิ่งแรกที่เราต้องทำก็คือ……..
สร้าง title ตื้ดดดดดดดดดดดดด ❌
สร้าง navbar ตื้ดดดดดดดดดดดดด ❌   
ตามหลัก TDD ของเรา อย่าพึ่งลืมนะคะ ต้องสร้าง test ก่อนเริ่ม coding ค่า  
### มาที่ไฟล์ favorite-animals.component.spec.ts
  
        import { async, ComponentFixture, TestBed } from '@angular/core/testing';
        import { FavoriteAnimalsComponent } from './favorite-animals.component';
        import { By } from '@angular/platform-browser'; //import By for Test css

        describe('FavoriteAnimalsComponent', () => {
        let component: FavoriteAnimalsComponent;
        let fixture: ComponentFixture<FavoriteAnimalsComponent>;

        beforeEach(async(() => {
            TestBed.configureTestingModule({
            declarations: [ FavoriteAnimalsComponent ]
            })
            .compileComponents();
        }));

        beforeEach(() => {
            fixture = TestBed.createComponent(FavoriteAnimalsComponent);
            component = fixture.componentInstance;
            fixture.detectChanges();
        });

        it('should create', () => {
            expect(component).toBeTruthy();
        });
        //add below

        it('should have a title', () => {
            const titleElements = fixture.debugElement.query(By.css('h1'));
            expect(titleElements.nativeElement.innerHTML).toBe('favorite animals');
        });
        });
  
 บรรทัดที่ 3 : import { By } from ‘@angular/platform-browser’; เพื่อนำมาเขียนทดสอบในบรรทัดที่ 28
บรรทัดที่ 27 : เราจะเพิ่มตัวตรวจสอบว่า มี title อยู่ใน < h1 > และมี content ตามที่เขียนไว้หรือไม่    
![](https://miro.medium.com/max/357/1*k5ZtrT5HLfi02w3CRIekoQ.png)  
เจอ failed สีแดง ไม่ต้องตกใจกัน เราทำให้ pass ได้  
เรามาเขียนสิ่งที่ตัว test ต้องการกัน   

            <h1>favorite animals</h1>

![](https://miro.medium.com/max/280/1*ol9-ekYGrqeaXiCe0jRNjQ.png)  
ผ่านแล้วววววววว  
หลังจากที่เราเขียนโค้ดแบบ TDD ตัวแรกได้แล้ว มาลองเพิ่ม test case อีกตัวกัน    

        // test ว่าในหน้า มี span ที่เขียน Hello world หรือไม่
        it('should have a span display Hello world', () => {
            const spanElements = fixture.debugElement.query(By.css('span'));
            expect(spanElements.nativeElement.innerHTML).toBe('Hello world');
        });
![](https://miro.medium.com/max/365/1*gejV4afL1VBw8dkDlRqK8w.png)  ใช้คำสั่ง jest หลังเพิ่ม test case  
จาก test case ด้านบน ต้องการให้มี < span >ที่แสดงข้อความว่า Hello world
จัดไปเลยยยยยยยย    

            < h1 >favorite animals< /h1 >
            <  >Hello world</span >
![](https://miro.medium.com/max/466/1*YngpImzbjKXgGHtqpq6pcg.png)  
ใช้คำสั่ง jest หลังแก้ไขไฟล์ html  
มาถึงตรงนี้ ทุกคนคงเข้าใจหลักการทำงานของ TDD กันแล้ว ซึ่งก็คือ
เขียน test case →Fail ❌ →ทำตาม test case →Pass ✔️
เมื่อทำตาม process เหล่านี้ได้ งานของเราก็ไม่ต้องมาปวดหัวกับการไล่โค้ดแล้ว
(ปวดหัวตอนเขียน test case แทน ตึ่งโป๊ะ!)
ถึงอย่างนั้น ถ้าเรารู้สาเหตุของข้อผิดพลาดก็ย่อมแก้ปัญหาได้ง่าย และรวดเร็วกว่า
มาฝึกทำงานโดยใช้ TDD ให้คล่องกันเถอะค่ะ 😉😉
หากต้องการเข้าใจเรื่องการเขียน Test case มากขึ้น แนะนำบทความข้างล่างนี้นะคะ  




