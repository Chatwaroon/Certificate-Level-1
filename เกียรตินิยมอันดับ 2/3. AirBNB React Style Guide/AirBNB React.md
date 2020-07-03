# คู่มือสไตล์ Airbnb React  / JSX   
คู่มือสไตล์นี้ส่วนใหญ่ขึ้นอยู่กับมาตรฐานที่แพร่หลายใน JavaScript แม้ว่าบางอนุสัญญา (เช่น async / await หรือฟิลด์คลาสคงที่) อาจยังคงรวมอยู่หรือถูกห้ามเป็นกรณี ๆ ไป ขณะนี้ยังไม่รวมหรือมีสิ่งใดก่อนกำหนดในขั้นตอนที่ 3 ในคู่มือนี้  
## สารบัญ  
1. Basic Rules    
2. Class vs React.createClass vs stateless    
3. Mixins    
4. Naming    
5. Declaration    
6. Alignment    
7. Quotes  
8. Spacing  
9. Props
10. Refs  
11. Parentheses  
12. Tags  
13. Methods  
14. Ordering  
15. isMounted  

# Basic Rules    
* รวมองค์ประกอบ React เพียงหนึ่งรายการต่อไฟล์  
    * อย่างไรก็ตามอนุญาตให้ใช้Stateless ได้หลายตัวต่อหนึ่งไฟล์ react/no-multi-compeslint:  
* ใช้ไวยากรณ์ JSX เสมอ  
* อย่าใช้React.createElementจนกว่าคุณจะเริ่มต้นแอพจากไฟล์ที่ไม่ใช่ JSX  
* react/forbid-prop-typesจะช่วยให้arraysและobjectsถ้ามันเป็นข้อสังเกตอย่างชัดเจนสิ่งที่arrayและobjectมีการใช้arrayOf, หรือobjectOfshape  

#  Class vs React.createClass vs stateless  
* ถ้าคุณมีรัฐภายในและ / หรือ refs ชอบมากกว่าclass extends React.Component React.createClasseslint:react/prefer-es6-class react/prefer-stateless-function   

        // bad
        const Listing = React.createClass({
        // ...
        render() {
            return <div>{this.state.hello}</div>;
        }
        });

        // good
        class Listing extends React.Component {
        // ...
        render() {
            return <div>{this.state.hello}</div>;
        }
        }  
และถ้าคุณไม่มีสถานะหรืออ้างอิงชอบฟังก์ชั่นปกติ (ไม่ใช่ฟังก์ชั่นลูกศร) ในชั้นเรียน:  
  
        // bad
        class Listing extends React.Component {
        render() {
            return <div>{this.props.hello}</div>;
        }
        }

        // bad (relying on function name inference is discouraged)
        const Listing = ({ hello }) => (
        <div>{hello}</div>
        );

        // good
        function Listing({ hello }) {
        return <div>{hello}</div>;
        }  

# Mixins  
* อย่าใช้มิกซ์อิน  

# Naming  
* ส่วนขยาย : ใช้.jsxส่วนขยายสำหรับส่วนประกอบการทำปฏิกิริยา eslint:react/jsx-filename-extension  
* ชื่อไฟล์ : ใช้ PascalCase สำหรับชื่อไฟล์ เช่นReservationCard.jsx.  
* การตั้งชื่ออ้างอิง : ใช้ PascalCase สำหรับทำปฏิกิริยาส่วนประกอบและ camelCase สำหรับอินสแตนซ์ของพวกเขา eslint:react/jsx-pascal-case   

        // bad
        import reservationCard from './ReservationCard';

        // good
        import ReservationCard from './ReservationCard';

        // bad
        const ReservationItem = <ReservationCard />;

        // good
        const reservationItem = <ReservationCard />;  

* การตั้งชื่อส่วนประกอบ : ใช้ชื่อไฟล์เป็นชื่อส่วนประกอบ ยกตัวอย่างเช่นควรจะมีชื่อของการอ้างอิงReservationCard.jsx ReservationCardอย่างไรก็ตามสำหรับส่วนประกอบรูทของไดเรกทอรีให้ใช้index.jsxเป็นชื่อไฟล์และใช้ชื่อไดเรกทอรีเป็นชื่อส่วนประกอบ:  

        // bad
        import Footer from './Footer/Footer';

        // bad
        import Footer from './Footer/index';

        // good
        import Footer from './Footer';  
* การตั้งชื่อส่วนประกอบที่สูงกว่า: ใช้คอมโพสิตของชื่อส่วนประกอบที่สูงกว่าและชื่อของคอมโพเนนต์ที่ส่งผ่านเป็นชื่อdisplayNameบนส่วนประกอบที่สร้างขึ้น ยกตัวอย่างเช่นองค์ประกอบลำดับที่สูงกว่าwithFoo()เมื่อผ่านองค์ประกอบที่Barควรผลิตส่วนประกอบที่มีของdisplayNamewithFoo(Bar)   

        // bad
        export default function withFoo(WrappedComponent) {
        return function WithFoo(props) {
            return <WrappedComponent {...props} foo />;
        }
        }

        // good
        export default function withFoo(WrappedComponent) {
        function WithFoo(props) {
            return <WrappedComponent {...props} foo />;
        }

        const wrappedComponentName = WrappedComponent.displayName
            || WrappedComponent.name
            || 'Component';

        WithFoo.displayName = `withFoo(${wrappedComponentName})`;
        return WithFoo;
        }  

* การตั้งชื่ออุปกรณ์ประกอบฉาก : หลีกเลี่ยงการใช้ชื่ออุปกรณ์ประกอบฉาก DOM เพื่อจุดประสงค์ที่แตกต่างกัน  

        // bad
        <MyComponent style="fancy" />

        // bad
        <MyComponent className="fancy" />

        // good
        <MyComponent variant="fancy" />  

# Declaration  
* ห้ามใช้displayNameสำหรับการตั้งชื่อคอมโพเนนต์ ให้ตั้งชื่อคอมโพเนนต์โดยอ้างอิง    

        // bad
        export default React.createClass({
        displayName: 'ReservationCard',
        // stuff goes here
        });

        // good
        export default class ReservationCard extends React.Component {
        }  

# Alignment    
* ทำตามสไตล์การจัดตำแหน่งเหล่านี้สำหรับไวยากรณ์ JSX eslint:react/jsx-closing-bracket-location react/jsx-closing-tag-location  

        // bad
        <Foo superLongParam="bar"
            anotherSuperLongParam="baz" />

        // good
        <Foo
        superLongParam="bar"
        anotherSuperLongParam="baz"
        />

        // if props fit in one line then keep it on the same line
        <Foo bar="bar" />

        // children get indented normally
        <Foo
        superLongParam="bar"
        anotherSuperLongParam="baz"
        >
        <Quux />
        </Foo>

        // bad
        {showButton &&
        <Button />
        }

        // bad
        {
        showButton &&
            <Button />
        }

        // good
        {showButton && (
        <Button />
        )}

        // good
        {showButton && <Button />}  

# Quotes   
* ใช้เครื่องหมายคำพูดคู่ ( ") สำหรับแอตทริบิวต์ JSX เสมอ แต่เป็นเครื่องหมายคำพูดเดี่ยว ( ') สำหรับ JS อื่น ๆ ทั้งหมด eslint:jsx-quotes  

        // bad
        <Foo bar='bar' />

        // good
        <Foo bar="bar" />

        // bad
        <Foo style={{ left: "20px" }} />

        // good
        <Foo style={{ left: '20px' }} />  

# Spacing  
* รวมช่องว่างเดียวในแท็กปิดตัวเองเสมอ eslint: no-multi-spaces,react/jsx-tag-spacing  

        // bad
        <Foo/>

        // very bad
        <Foo                 />

        // bad
        <Foo
        />

        // good
        <Foo />  

* อย่าใส่แผ่นค้ำยัน JSX ที่มีช่องว่าง eslint:react/jsx-curly-spacing  

        // bad
        <Foo bar={ baz } />

        // good
        <Foo bar={baz} />  

# Props  
* ใช้ camelCase สำหรับชื่อ prop เสมอ  

        // bad
        <Foo
        UserName="hello"
        phone_number={12345678}
        />

        // good
        <Foo
        userName="hello"
        phoneNumber={12345678}
        />  

* trueงดค่าของเสาเมื่อมันเป็นอย่างชัดเจน eslint:react/jsx-boolean-value  

        // bad
        <Foo
        hidden={true}
        />

        // good
        <Foo
        hidden
        />

        // good
        <Foo hidden />  

* รวมถึงaltเสาใน<img>แท็กเสมอ หากภาพเป็น presentational, altสามารถเป็นสตริงที่ว่างเปล่าหรือต้องมี<img> role="presentation"eslint:jsx-a11y/alt-text  

        // bad
        <img src="hello.jpg" />

        // good
        <img src="hello.jpg" alt="Me waving hello" />

        // good
        <img src="hello.jpg" alt="" />

        // good
        <img src="hello.jpg" role="presentation" />  

* อย่าใช้คำเช่น "รูปภาพ", "ภาพถ่าย" หรือ "รูปภาพ" ใน<img> altอุปกรณ์ประกอบฉาก eslint:jsx-a11y/img-redundant-alt  

        // bad
        <img src="hello.jpg" alt="Picture of me waving hello" />

        // good
        <img src="hello.jpg" alt="Me waving hello" />  

* ใช้บทบาท ARIA ที่ถูกต้องและไม่เป็นนามธรรมเท่านั้น eslint:jsx-a11y/aria-role  

        // bad - not an ARIA role
        <div role="datepicker" />

        // bad - abstract ARIA role
        <div role="range" />

        // good
        <div role="button" />  

* อย่าใช้accessKeyกับองค์ประกอบ eslint:jsx-a11y/no-access-key    


        // bad
        <div accessKey="h" />

        // good
        <div />  

* หลีกเลี่ยงการใช้ดัชนีอาร์เรย์เป็นkeyprop ต้องการรหัสที่เสถียร eslint:react/no-array-index-key  

เราไม่แนะนำให้ใช้ดัชนีสำหรับกุญแจหากลำดับของรายการอาจมีการเปลี่ยนแปลง   

        // bad
        {todos.map((todo, index) =>
        <Todo
            {...todo}
            key={index}
        />
        )}

        // good
        {todos.map(todo => (
        <Todo
            {...todo}
            key={todo.id}
        />
        ))}  

* กำหนด defaultProps อย่างชัดเจนสำหรับอุปกรณ์ประกอบฉากที่ไม่จำเป็นทั้งหมด  

        // bad
        function SFC({ foo, bar, children }) {
        return <div>{foo}{bar}{children}</div>;
        }
        SFC.propTypes = {
        foo: PropTypes.number.isRequired,
        bar: PropTypes.string,
        children: PropTypes.node,
        };

        // good
        function SFC({ foo, bar, children }) {
        return <div>{foo}{bar}{children}</div>;
        }
        SFC.propTypes = {
        foo: PropTypes.number.isRequired,
        bar: PropTypes.string,
        children: PropTypes.node,
        };
        SFC.defaultProps = {
        bar: '',
        children: null,
        };  

* ใช้อุปกรณ์ประกอบฉากการแพร่กระจายเท่าที่จำเป็น  
  
ข้อยกเว้น  
* HOC ที่พร็อกซีประกอบฉากและรอก propTypes  
  
        function HOC(WrappedComponent) {
        return class Proxy extends React.Component {
            Proxy.propTypes = {
            text: PropTypes.string,
            isLoading: PropTypes.bool
            };

            render() {
            return <WrappedComponent {...this.props} />
            }
        }
        }   

* การแพร่กระจายวัตถุด้วยอุปกรณ์ประกอบฉากที่เป็นที่รู้จักและชัดเจน สิ่งนี้มีประโยชน์อย่างยิ่งเมื่อทำการทดสอบส่วนประกอบการทำปฏิกิริยาด้วย Mocha's beforeEach build  

        export default function Foo {
        const props = {
            text: '',
            isPublished: false
        }

        return (<div {...props} />);
        }  

หมายเหตุสำหรับการใช้งาน: กรองอุปกรณ์ประกอบฉากที่ไม่จำเป็นออกหากเป็นไปได้ นอกจากนี้ให้ใช้ประเภทแบบตรงทุกประการเพื่อช่วยป้องกันข้อผิดพลาด  

        // bad
        render() {
        const { irrelevantProp, ...relevantProps } = this.props;
        return <WrappedComponent {...this.props} />
        }

        // good
        render() {
        const { irrelevantProp, ...relevantProps } = this.props;
        return <WrappedComponent {...relevantProps} />
        }  

# refs  
* ใช้การเรียกกลับที่อ้างอิงเสมอ eslint:react/no-string-refs  
  
        // bad
        <Foo
        ref="myRef"
        />

        // good
        <Foo
        ref={(ref) => { this.myRef = ref; }}
        />    

# Parentheses  
* ล้อมรอบแท็ก JSX ในวงเล็บเมื่อขยายมากกว่าหนึ่งบรรทัด eslint:react/jsx-wrap-multilines  
  
        // bad
        render() {
        return <MyComponent variant="long body" foo="bar">
                <MyChild />
                </MyComponent>;
        }

        // good
        render() {
        return (
            <MyComponent variant="long body" foo="bar">
            <MyChild />
            </MyComponent>
        );
        }

        // good, when single line
        render() {
        const body = <div>hello</div>;
        return <MyComponent>{body}</MyComponent>;
        }  

# Tags  
* แท็กปิดตัวเองเสมอที่ไม่มีลูก eslint:react/self-closing-comp  

        // bad
        <Foo variant="stuff"></Foo>

        // good
        <Foo variant="stuff" />

* หากองค์ประกอบของคุณมีคุณสมบัติหลายบรรทัดปิดแท็กในบรรทัดใหม่ eslint:react/jsx-closing-bracket-location  

        // bad
        <Foo
        bar="bar"
        baz="baz" />

        // good
        <Foo
        bar="bar"
        baz="baz"
        />  

# Methods  
* ใช้ฟังก์ชั่นลูกศรเพื่อปิดตัวแปรท้องถิ่น มันจะมีประโยชน์เมื่อคุณต้องการส่งข้อมูลเพิ่มเติมไปยังตัวจัดการเหตุการณ์ แม้ว่าให้แน่ใจว่าพวกเขาจะไม่ทำร้ายประสิทธิภาพการทำงานโดยเฉพาะอย่างยิ่งเมื่อส่งผ่านไปยังองค์ประกอบที่กำหนดเองที่อาจ PureComponents เพราะพวกเขาจะก่อให้เกิดการแสดงผลที่ไม่จำเป็นทุกครั้ง  

        function ItemList(props) {
        return (
            <ul>
            {props.items.map((item, index) => (
                <Item
                key={item.key}
                onClick={(event) => { doSomethingWith(event, item.name, index); }}
                />
            ))}
            </ul>
        );
        }  

  
  * ผูกตัวจัดการเหตุการณ์สำหรับวิธีการแสดงผลในตัวสร้าง eslint:react/jsx-no-bind  
  
        // bad
        class extends React.Component {
        onClickDiv() {
            // do stuff
        }

        render() {
            return <div onClick={this.onClickDiv.bind(this)} />;
        }
        }

        // very bad
        class extends React.Component {
        onClickDiv = () => {
            // do stuff
        }

        render() {
            return <div onClick={this.onClickDiv} />
        }
        }

        // good
        class extends React.Component {
        constructor(props) {
            super(props);

            this.onClickDiv = this.onClickDiv.bind(this);
        }

        onClickDiv() {
            // do stuff
        }

        render() {
            return <div onClick={this.onClickDiv} />;
        }
        }  

* อย่าใช้คำนำหน้าขีดเส้นใต้สำหรับวิธีการภายในของส่วนประกอบ React  
  
        // bad
        React.createClass({
        _onClickSubmit() {
            // do stuff
        },

        // other stuff
        });

        // good
        class extends React.Component {
        onClickSubmit() {
            // do stuff
        }

        // other stuff
        }  

* อย่าลืมส่งคืนค่าในrenderวิธีการของคุณ eslint:react/require-render-return  

        // bad
        render() {
        (<div />);
        }

        // good
        render() {
        return (<div />);
        }  

# Ordering  
* การสั่งซื้อสำหรับclass extends React.Component:    
* วิธีการกำหนดpropTypes, defaultProps, contextTypesฯลฯ ...  

        import React from 'react';
        import PropTypes from 'prop-types';

        const propTypes = {
        id: PropTypes.number.isRequired,
        url: PropTypes.string.isRequired,
        text: PropTypes.string,
        };

        const defaultProps = {
        text: 'Hello World',
        };

        class Link extends React.Component {
        static methodsAreOk() {
            return true;
        }

        render() {
            return <a href={this.props.url} data-id={this.props.id}>{this.props.text}</a>;
        }
        }

        Link.propTypes = propTypes;
        Link.defaultProps = defaultProps;

        export default Link;  

* Ordering for React.createClass: eslint: react/sort-comp  

# isMounted  
* isMountedอย่าใช้ eslint:react/no-is-mounted





















