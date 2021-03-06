# VS Code ESLint extension  
รวมESLintเข้ากับ VS Code ถ้าคุณยังใหม่กับ ESLint ตรวจสอบเอกสาร

ส่วนขยายใช้ไลบรารี ESLint ที่ติดตั้งในโฟลเดอร์เวิร์กสเปซที่เปิด หากโฟลเดอร์ไม่ได้จัดเตรียมไว้หนึ่งส่วนขยายจะค้นหารุ่นติดตั้งส่วนกลาง หากคุณยังไม่ได้ติดตั้ง ESLint แบบโลคัลหรือแบบโกลบอลทำได้โดยการรันnpm install eslintในโฟลเดอร์เวิร์กสเปซสำหรับการติดตั้งแบบโลคัลหรือnpm install -g eslintสำหรับการติดตั้งแบบโกลบอล

ในโฟลเดอร์ใหม่คุณอาจต้องสร้าง.eslintrcไฟล์กำหนดค่า คุณสามารถทำได้โดยใช้คำสั่ง VS Code Create ESLint configurationหรือโดยการรันeslintคำสั่งในเทอร์มินัล หากคุณติดตั้ง ESLint แบบโกลบอล (ดูด้านบน) ให้รันeslint --initในเทอร์มินัล หากคุณติดตั้ง ESLint ไว้ภายในเครื่องให้รัน.\node_modules\.bin\eslint --initภายใต้ Windows และ./node_modules/.bin/eslint --initภายใต้ Linux และ Mac  
## Release Notes  
ส่วนขยายเวอร์ชัน 2.0.4 มีการปรับปรุงที่สำคัญดังต่อไปนี้:  
* การตรวจสอบที่ดีขึ้น typescript - เร็วที่สุดเท่าที่ typescript มีการกำหนดค่าได้อย่างถูกต้องภายใน ESLint คุณไม่จำเป็นต้องกำหนดค่าเพิ่มเติมผ่าน VS รหัสของeslint.validateการตั้งค่า เช่นเดียวกับไฟล์ HTML และ Vue.js  
* การสนับสนุนไดเรกทอรีการทำงานของ Glob - โครงการที่มีโครงสร้างโฟลเดอร์ที่ซับซ้อนและจำเป็นต้องปรับแต่งไดเรกทอรีการทำงานผ่านeslint.workingDirectoriesตอนนี้สามารถใช้รูปแบบ glob แทนที่จะแสดงรายการทุกโฟลเดอร์โครงการ ยกตัวอย่างเช่นจะตรงกับโฟลเดอร์โครงการทั้งหมดที่เริ่มต้นด้วย{ "pattern": "code-*" } code-นอกจากนี้ส่วนขยายจะเปลี่ยนไดเรกทอรีทำงานตามค่าเริ่มต้น คุณสามารถปิดใช้งานคุณสมบัตินี้ได้ด้วย!cwdคุณสมบัติใหม่  
* การสนับสนุนฟอร์แมตเตอร์: ESLint สามารถใช้เป็นฟอร์แมตเตอร์ได้แล้ว หากต้องการเปิดใช้งานคุณสมบัตินี้ให้ใช้การeslint.format.enableตั้งค่า  
* mproved Auto Fix on Save - Auto Fix on Save ตอนนี้เป็นส่วนหนึ่งของ Code Code ของ VS Code บน Save โครงสร้างพื้นฐานและคำนวณการแก้ไขที่เป็นไปได้ทั้งหมดในรอบเดียว มันถูกปรับแต่งผ่านการeditor.codeActionsOnSaveตั้งค่า source.fixAll.eslintการตั้งค่าการสนับสนุนคุณสมบัติเฉพาะ ESLint source.fixAllนามสกุลยังเคารพทรัพย์สินทั่วไป  

การตั้งค่าด้านล่างเปิดการแก้ไขอัตโนมัติสำหรับผู้ให้บริการทั้งหมดรวมถึง ESLint:   

        "editor.codeActionsOnSave": {
                "source.fixAll": true
            }  
ในทางตรงกันข้ามการกำหนดค่านี้เปิดสำหรับ ESLint เท่านั้น:  

        "editor.codeActionsOnSave": {
                "source.fixAll.eslint": true
            }  
นอกจากนี้คุณยังสามารถเลือกปิดใช้งาน ESLint ผ่านทาง:  

        "editor.codeActionsOnSave": {
                "source.fixAll": true,
                "source.fixAll.eslint": false
            }  

นอกจากนี้โปรดทราบว่ามีงบประมาณเวลา 750ms ในการเรียกใช้การทำงานของรหัสในการบันทึกซึ่งอาจไม่เพียงพอสำหรับไฟล์ JavaScript / TypeScript ขนาดใหญ่ คุณสามารถเพิ่มงบประมาณเวลาโดยใช้การeditor.codeActionsOnSaveTimeoutตั้งค่า  

VS Code ESLint extension
สถานะการสร้าง

รวมESLintเข้ากับ VS Code ถ้าคุณยังใหม่กับ ESLint ตรวจสอบเอกสาร

ส่วนขยายใช้ไลบรารี ESLint ที่ติดตั้งในโฟลเดอร์เวิร์กสเปซที่เปิด หากโฟลเดอร์ไม่ได้จัดเตรียมไว้หนึ่งส่วนขยายจะค้นหารุ่นติดตั้งส่วนกลาง หากคุณยังไม่ได้ติดตั้ง ESLint แบบโลคัลหรือแบบโกลบอลทำได้โดยการรันnpm install eslintในโฟลเดอร์เวิร์กสเปซสำหรับการติดตั้งแบบโลคัลหรือnpm install -g eslintสำหรับการติดตั้งแบบโกลบอล

ในโฟลเดอร์ใหม่คุณอาจต้องสร้าง.eslintrcไฟล์กำหนดค่า คุณสามารถทำได้โดยใช้คำสั่ง VS Code Create ESLint configurationหรือโดยการรันeslintคำสั่งในเทอร์มินัล หากคุณติดตั้ง ESLint แบบโกลบอล (ดูด้านบน) ให้รันeslint --initในเทอร์มินัล หากคุณติดตั้ง ESLint ไว้ภายในเครื่องให้รัน.\node_modules\.bin\eslint --initภายใต้ Windows และ./node_modules/.bin/eslint --initภายใต้ Linux และ Mac

บันทึกย่อประจำรุ่น
ส่วนขยายเวอร์ชัน 2.0.4 มีการปรับปรุงที่สำคัญดังต่อไปนี้:

การตรวจสอบที่ดีขึ้น typescript - เร็วที่สุดเท่าที่ typescript มีการกำหนดค่าได้อย่างถูกต้องภายใน ESLint คุณไม่จำเป็นต้องกำหนดค่าเพิ่มเติมผ่าน VS รหัสของeslint.validateการตั้งค่า เช่นเดียวกับไฟล์ HTML และ Vue.js
การสนับสนุนไดเรกทอรีการทำงานของ Glob - โครงการที่มีโครงสร้างโฟลเดอร์ที่ซับซ้อนและจำเป็นต้องปรับแต่งไดเรกทอรีการทำงานผ่านeslint.workingDirectoriesตอนนี้สามารถใช้รูปแบบ glob แทนที่จะแสดงรายการทุกโฟลเดอร์โครงการ ยกตัวอย่างเช่นจะตรงกับโฟลเดอร์โครงการทั้งหมดที่เริ่มต้นด้วย{ "pattern": "code-*" } code-นอกจากนี้ส่วนขยายจะเปลี่ยนไดเรกทอรีทำงานตามค่าเริ่มต้น คุณสามารถปิดใช้งานคุณสมบัตินี้ได้ด้วย!cwdคุณสมบัติใหม่
การสนับสนุนฟอร์แมตเตอร์: ESLint สามารถใช้เป็นฟอร์แมตเตอร์ได้แล้ว หากต้องการเปิดใช้งานคุณสมบัตินี้ให้ใช้การeslint.format.enableตั้งค่า
Improved Auto Fix on Save - Auto Fix on Save ตอนนี้เป็นส่วนหนึ่งของ Code Code ของ VS Code บน Save โครงสร้างพื้นฐานและคำนวณการแก้ไขที่เป็นไปได้ทั้งหมดในรอบเดียว มันถูกปรับแต่งผ่านการeditor.codeActionsOnSaveตั้งค่า source.fixAll.eslintการตั้งค่าการสนับสนุนคุณสมบัติเฉพาะ ESLint source.fixAllนามสกุลยังเคารพทรัพย์สินทั่วไป
การตั้งค่าด้านล่างเปิดการแก้ไขอัตโนมัติสำหรับผู้ให้บริการทั้งหมดรวมถึง ESLint:

    "editor.codeActionsOnSave": {
        "source.fixAll": true
    }
ในทางตรงกันข้ามการกำหนดค่านี้เปิดสำหรับ ESLint เท่านั้น:

    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
นอกจากนี้คุณยังสามารถเลือกปิดใช้งาน ESLint ผ่านทาง:

    "editor.codeActionsOnSave": {
        "source.fixAll": true,
        "source.fixAll.eslint": false
    }
นอกจากนี้โปรดทราบว่ามีงบประมาณเวลา 750ms ในการเรียกใช้การทำงานของรหัสในการบันทึกซึ่งอาจไม่เพียงพอสำหรับไฟล์ JavaScript / TypeScript ขนาดใหญ่ คุณสามารถเพิ่มงบประมาณเวลาโดยใช้การeditor.codeActionsOnSaveTimeoutตั้งค่า

การeslint.autoFixOnSaveตั้งค่าเก่าเลิกใช้แล้วและสามารถลบได้อย่างปลอดภัย  

## ตัวเลือกการตั้งค่า   
 หากคุณกำลังใช้รุ่นขยาย ESLint <2.x แล้วโปรดดูที่การตั้งค่าตัวเลือกที่นี่ ส่วนขยายนี้ก่อให้เกิดตัวแปรต่อไปนี้กับการตั้งค่า :  
 * eslint.enable: เปิด / ปิดการใช้งาน ESLint ถูกเปิดใช้งานโดยค่าเริ่มต้น  
 * eslint.debug: เปิดใช้งานโหมดการดีบักของ ESLint (เช่นเดียวกับตัวเลือกบรรทัดคำสั่ง --debug) โปรดดูช่องสัญญาณเอาต์พุต ESLint สำหรับผลลัพธ์การดีบัก ตัวเลือกนี้มีประโยชน์มากในการติดตามปัญหาการกำหนดค่าและปัญหาการติดตั้งกับ ESLint เนื่องจากให้ข้อมูลอย่างละเอียดเกี่ยวกับวิธีการตรวจสอบความถูกต้องของไฟล์ของ ESLint    
 * eslint.lintTask.enable: ไม่ว่าจะเป็นส่วนขยายงานที่ขุยเพื่อขุยโฟลเดอร์พื้นที่ทำงานทั้งหมด  
 * eslint.lintTask.options: ตัวเลือกบรรทัดคำสั่งถูกนำไปใช้เมื่อเรียกใช้งานเพื่อขยิบพื้นที่ทำงานทั้งหมด ( https://eslint.org/docs/user-guide/command-line-interface ) ตัวอย่างการชี้ไปที่.eslintrc.jsonไฟล์ที่กำหนดเองและกำหนดเอง.eslintignoreคือ:  

        {
        "eslint.lintTask.options": "-c C:/mydirectory/.eslintrc.json --ignore-path C:/mydirectory/.eslintignore ."
        }    

* eslint.packageManager: ควบคุมเครื่องมือจัดการแพคเกจที่จะใช้แก้ไขไลบรารี ESLint สิ่งนี้มีอิทธิพลต่อถ้าไลบรารี ESLint ได้รับการแก้ไขแบบโกลบอล ค่าที่ถูกต้อง"npm"หรือหรือ"yarn""pnpm"  
* eslint.optionsตัวเลือกการกำหนดค่าวิธี ESLint จะเริ่มต้นใช้ESLint CLI เครื่องยนต์ API เริ่มต้นที่ถุงตัวเลือกที่ว่างเปล่า ตัวอย่างที่ชี้ไปยัง.eslintrc.jsonไฟล์ที่กำหนดเองคือ:  

        {
        "eslint.options": { "configFile": "C:/mydirectory/.eslintrc.json" }
        }    
        
* eslint.run- ทำงาน linter onSaveหรือเริ่มต้นคือonTypeonType   
*  eslint.quiet - ละเว้นคำเตือน    
* eslint.runtime - ใช้การตั้งค่านี้เพื่อตั้งค่าพา ธ ของโหนดรันไทม์เพื่อเรียกใช้ ESLint ภายใต้  
* eslint.nodePath- ใช้การตั้งค่านี้ถ้าแพคเกจ ESLint /myGlobalNodePackages/node_modulesติดตั้งไม่สามารถตรวจพบตัวอย่างเช่น  
* eslint.probe= อาร์เรย์สำหรับตัวระบุภาษาที่ควรเปิดใช้งานส่วนขยาย ESLint และควรพยายามตรวจสอบความถูกต้องของไฟล์ หากการตรวจสอบความถูกต้องล้มเหลวสำหรับภาษาที่ตรวจพบส่วนขยายจะบอกว่าเงียบ เริ่ม["javascript", "javascriptreact", "typescript", "typescriptreact", "html", "vue"]ต้นที่  
* eslint.validate- อาร์เรย์ของตัวระบุภาษาที่ระบุไฟล์ที่จะบังคับใช้การตรวจสอบความถูกต้อง นี่เป็นการตั้งค่าแบบเก่าและในกรณีปกติไม่จำเป็นอีกต่อไป เริ่ม["javascript", "javascriptreact"]ต้นที่  
* eslint.format.enable: เปิดใช้งาน ESLint เป็นตัวจัดรูปแบบสำหรับไฟล์ที่ตรวจสอบความถูกต้อง แม้ว่าคุณจะสามารถใช้ตัวจัดรูปแบบบนบันทึกโดยใช้การตั้งค่าeditor.formatOnSaveขอแนะนำให้ใช้editor.codeActionsOnSaveคุณลักษณะนี้เนื่องจากช่วยให้สามารถกำหนดค่าได้ดีขึ้น  
* eslint.workingDirectories- ระบุวิธีคำนวณไดเรกทอรีการทำงานที่ใช้ ESLint ESLint แก้ไขแฟ้มการกำหนดค่า (เช่นeslintrc, .eslintignore) เทียบกับไดเรกทอรีการทำงานจึงเป็นสิ่งสำคัญในการกำหนดค่านี้อย่างถูกต้อง หากเรียกใช้งาน ESLint ในเทอร์มินัลคุณต้องเปลี่ยนไดเรกทอรีการทำงานในเทอร์มินัลลงในโฟลเดอร์ย่อยโดยปกติแล้วจำเป็นต้องปรับแต่งการตั้งค่านี้ (ดูเพิ่มเติมที่CLIEngine options # cwd ) โปรดทราบว่า.eslintrc*ไฟล์นั้นได้รับการแก้ไขโดยพิจารณาถึงไดเรกทอรีหลักในขณะที่.eslintignoreไฟล์นั้นได้รับการยกย่องในไดเรกทอรีการทำงานปัจจุบันเท่านั้น ค่าต่อไปนี้สามารถใช้ได้:  
    * [{ "mode": "location" }](@since 2.0.0): สั่งให้ ESLint ใช้ตำแหน่งโฟลเดอร์เวิร์กสเปซหรือตำแหน่งไฟล์ (หากไม่มีโฟลเดอร์เวิร์กสเปซเปิดอยู่) เป็นไดเร็กทอรีการทำงาน นี่เป็นค่าเริ่มต้นและเป็นกลยุทธ์เดียวกับที่ใช้ในเวอร์ชันเก่าของส่วนขยาย ESLint (เวอร์ชัน 1.9.x)  
    * [{ "mode": "auto" }](@since 2.0.0): สั่ง ESLint เพื่อสรุปไดเรกทอรีทำงานตามสถานที่ตั้งของpackage.json, .eslintignoreและ.eslintrc*ไฟล์ สิ่งนี้อาจใช้งานได้ในหลายกรณี แต่อาจนำไปสู่ผลลัพธ์ที่ไม่คาดคิดเช่นกัน  
    * string[]: อาร์เรย์ของไดเรกทอรีทำงานที่จะใช้ พิจารณาเค้าโครงไดเรกทอรีดังต่อไปนี้:    


            root/
            client/
                .eslintrc.json
                client.js
            server/
                .eslintignore
                .eslintrc.json
                server.js
จากนั้นใช้การตั้งค่า:   

        "eslint.workingDirectories": [ "./client", "./server" ]   
        

จะตรวจสอบไฟล์ภายในไดเรกทอรีเซิร์ฟเวอร์กับไดเรกทอรีเซิร์ฟเวอร์เป็นไดเรกทอรีการทำงาน eslint ปัจจุบัน เช่นเดียวกับไฟล์ในไดเรกทอรีลูกค้า ส่วนขยาย ESLint จะเปลี่ยนไดเรกทอรีการทำงานของกระบวนการเป็นไดเรกทอรีที่ระบุ หากไม่ต้องการตัวอักษรที่มี!cwdคุณสมบัติสามารถใช้ได้ (เช่น{ "directory: "./client", "!cwd": true }) นี้จะใช้ไดเรกทอรีลูกค้าเป็นไดเรกทอรีทำงาน ESLint แต่จะไม่เปลี่ยนไดเรกทอรีการทำงานของกระบวนการ 

   * { "pattern": glob pattern }(@since 2.0.0): อนุญาตให้ระบุรูปแบบเพื่อตรวจจับไดเรกทอรีการทำงาน นี่เป็นทางลัดสำหรับการแสดงรายการทุกไดเรกทอรี หากคุณมีที่เก็บโมโนที่มีโปรเจ็กต์ทั้งหมดของคุณอยู่ด้านล่างโฟลเดอร์แพ็คเกจคุณสามารถใช้{ "pattern": "./packages/*/" }เพื่อทำให้โฟลเดอร์เหล่านี้ทำงานได้ไดเรกทอรี  

*  eslint.codeAction.disableRuleComment - วัตถุที่มีคุณสมบัติ:  
   * enable- แสดงกฎผ้าสำลีปิดการใช้งานในเมนูแก้ไขด่วน trueโดยค่าเริ่มต้น.
   *   location- เลือกที่จะเพิ่มeslint-disableความคิดเห็นในการหรือseparateLine เป็นค่าเริ่มต้น ตัวอย่าง:sameLineseparateLine  

            { "enable": true, "location": "sameLine" }  

* eslint.codeAction.showDocumentation - วัตถุที่มีคุณสมบัติ:  
   *  enable- แสดงหน้าเอกสารคู่มือกฎของขุยแบบเปิดในเมนูแก้ไขด่วน trueโดยค่าเริ่มต้น  

* eslint.codeActionsOnSave.mode (@since 2.0.12): ควบคุมว่าจะแก้ไขปัญหาใดบ้างเมื่อเรียกใช้การทำงานของรหัสในการบันทึก  
     *  all: แก้ไขปัญหาที่เป็นไปได้ทั้งหมดโดยการตรวจสอบความถูกต้องของเนื้อหาของไฟล์ สิ่งนี้เรียกใช้งานโค้ดพา ธ เดียวกันกับการเรียกใช้ eslint ด้วย--fixตัวเลือกในเทอร์มินัลและอาจใช้เวลาสักครู่ นี่เป็นค่าเริ่มต้น  
     * problems: แก้ไขเฉพาะปัญหาที่แก้ไขได้ที่รู้จักในปัจจุบันตราบใดที่การแก้ไขข้อความไม่ทับซ้อนกัน โหมดนี้เร็วขึ้นมาก แต่มีแนวโน้มมากที่จะแก้ไขปัญหาบางส่วนเท่านั้น  
* eslint.format.enable(@since 2.0.0): ใช้ ESlint เป็นฟอร์แมตเตอร์สำหรับไฟล์ที่ตรวจสอบโดย ESLint หากเปิดใช้งานโปรดตรวจสอบให้แน่ใจว่าได้ปิดใช้งานตัวจัดรูปแบบอื่น ๆ หากคุณต้องการให้เป็นค่าเริ่มต้น วิธีที่ดีในการทำเช่นนั้นคือเพิ่มการตั้งค่าต่อไปนี้"[javascript]": { "editor.defaultFormatter": "dbaeumer.vscode-eslint" }สำหรับ JavaScript สำหรับ typescript "[typescript]": { "editor.defaultFormatter": "dbaeumer.vscode-eslint" }คุณจะต้องเพิ่ม  
* eslint.onIgnoredFiles(@since 2.0.10): ใช้เพื่อควบคุมว่าควรสร้าง warings เมื่อพยายาม lint ไฟล์ที่ถูกละเว้นหรือไม่ offเริ่มต้นคือ warnสามารถตั้งค่าให้  
* editor.codeActionsOnSave(@since 2.0.0): source.fixAll.eslintการตั้งค่านี้ในขณะนี้สนับสนุนรายการ หากตั้งค่าเป็นจริงข้อผิดพลาด ESLint ที่แก้ไขได้ทั้งหมดจากปลั๊กอินทั้งหมดจะได้รับการแก้ไขเมื่อบันทึก นอกจากนี้คุณยังสามารถเลือกเปิดใช้งานและปิดการใช้งานภาษาเฉพาะโดยใช้การตั้งค่าขอบเขตภาษาของรหัส VS หากต้องการปิดใช้งานcodeActionsOnSaveสำหรับไฟล์ HTML ให้ใช้การตั้งค่าต่อไปนี้:  

        "[html]": {
            "editor.codeActionsOnSave": {
            "source.fixAll.eslint": false
            }
        }  

การeslint.autoFixOnSaveตั้งค่าเก่าเลิกใช้แล้วและสามารถลบได้อย่างปลอดภัย โปรดทราบว่าถ้าคุณใช้ ESLint เป็นค่าเริ่มต้นของการจัดรูปแบบที่คุณควรปิดเมื่อคุณได้เปิดใช้editor.formatOnSave editor.codeActionsOnSaveมิฉะนั้นคุณจะได้รับการแก้ไขสองครั้งซึ่งไม่จำเป็น  

## การตั้งค่าการโยกย้าย  
หากeslint.autoFixOnSaveตั้งค่าตัวเลือกเก่าเป็นจริง ESLint จะแจ้งให้แปลงเป็นeditor.codeActionsOnSaveรูปแบบใหม่ หากคุณต้องการหลีกเลี่ยงการย้ายข้อมูลคุณสามารถตอบกลับในกล่องโต้ตอบด้วยวิธีต่อไปนี้:  
* ไม่ใช่ตอนนี้: การตั้งค่าจะไม่ถูกโอนย้ายโดย ESLint พร้อมท์อีกครั้งในครั้งถัดไปที่คุณเปิดเวิร์กสเปซ  
* ห้ามโยกย้ายการตั้งค่า: การโยกย้ายการตั้งค่าจะถูกปิดใช้งานโดยเปลี่ยนการตั้งค่าผู้ใช้eslint.migration.2_xเป็นoff  


การโยกย้ายสามารถทริกเกอร์ด้วยตนเองได้ตลอดเวลาโดยใช้คำสั่ง ESLint: Migrate Settings  


## คำสั่ง:  
  ส่วนขยายนี้ก่อให้เกิดคำสั่งต่อไปนี้เพื่อจานสีคำสั่ง  
  * Create '.eslintrc.json' file: สร้าง.eslintrc.jsonไฟล์ใหม่  
  * Fix all auto-fixable problems: ใช้การแก้ไขอัตโนมัติของ ESLint กับปัญหาที่แก้ไขได้ทั้งหมด  
  * Disable ESLint for this Workspace: ปิดใช้งานส่วนขยาย ESLint สำหรับพื้นที่ทำงานนี้    
  * Enable ESLint for this Workspace: เปิดใช้งานส่วนขยาย ESLint สำหรับพื้นที่ทำงานนี้    
  * Reset Library Decisions: รีเซ็ตการยืนยันการตรวจสอบความถูกต้องของไลบรารี ESLint    

## การใช้ส่วนขยายกับการทำงานของรหัส VS  
ส่วนขยายจะขย้ำไฟล์แต่ละไฟล์เฉพาะในการพิมพ์ หากคุณต้องการผ้าสำลีชุดพื้นที่ทำงานทั้งหมดeslint.lintTask.enableไปtrueและการขยายนอกจากนี้ยังจะมีส่วนร่วมeslint: lint whole folderงาน tasks.jsonไม่มีความจำเป็นอีกต่อไปเพื่อกำหนดงานที่กำหนดเองในการเป็น  
##  การใช้ ESLint เพื่อตรวจสอบไฟล์ TypeScript    
แนะนำที่ดีเกี่ยวกับวิธีการใช้ผ้าสำลี typescript ESlint สามารถพบได้ในtypescript - ESLint โปรดทำความคุ้นเคยกับคำแนะนำก่อนใช้ส่วนขยาย VS Code ESLint ในการตั้งค่า TypeScript ตรวจสอบให้แน่ใจว่าคุณสามารถตรวจสอบไฟล์ TypeScript ได้สำเร็จในเทอร์มินัลโดยใช้eslintคำสั่ง

โครงการนี้ใช้ ESLint เพื่อตรวจสอบความถูกต้องของไฟล์ TypeScript ดังนั้นจึงสามารถใช้เป็นพิมพ์เขียวเพื่อเริ่มต้น

เพื่อหลีกเลี่ยงการตรวจสอบจากการติดตั้ง TSLint ปิด TSLint "tslint.enable": falseใช้    

## การตั้งค่าที่เก็บโมโน  
เช่นเดียวกับ JavaScript ที่ตรวจสอบความถูกต้องของ TypeScript ในที่เก็บข้อมูลโมโนคุณต้องแจ้งให้ทราบถึงส่วนขยาย VS Code ESLint ว่าไดเรกทอรีทำงานปัจจุบันคืออะไร ใช้การeslint.workingDirectoriesตั้งค่าที่จะทำ สำหรับที่เก็บนี้การตั้งค่าไดเรกทอรีการทำงานมีลักษณะดังนี้:  

        "eslint.workingDirectories": [ "./client", "./server" ]


















  
  




 


  


