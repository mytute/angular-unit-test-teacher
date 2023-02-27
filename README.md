Unit Tests : Test a component in isolation, without external resources(file system, database, API endpoint)

jasmine කියන්නේ open-source javascript testing framework එකක්.

Angular testing by using : Angular CLI, Jasmine, Karma, Protractor and Cucumber.

Jasmine is framework and Karma is the runner.

Some of the Testing use cases
1. testing routes
2. testing route data - query/ params
3. testing components
4. testing dependency injection
5. testing services
6. Setting up Mock Service and data.
7. Testing forms
8. testing validations
9. testing elements in templates

Unit Testing    
* testing smaller granular independent modules, services or pipes is called as unit testing.     
* focus is on "task" level testing.     
* provides input and verifies output for smaller sample.    
* ideal for testing individual pieces of the big picture.    
* framework used are Jasmine and Karma.     

End to End Testing    
* Automating the entire end to end functional flows.    
* Helps in building automated test suites when the application or product sizes outgrows.    
* Protractor framework is used to End to End Testing.
* BDD(behaviour driven development) frameworks likes Cucumber are also used for testing the functional flows.

Testing Utilities Provided by Angular    
* Auto generation of code (.spec.ts file)     
* Angular natively supports unit tests using jasmine and Karma.   
* Angular CLI has built-in commands to run the test unit tests.    
* Angular CLI has built-in commands to run End to End tests.    
* Using Angular CLI - we generate the test files(spec) files.    
* We can also use Angular In-Memory service to mock the services.    
* Angular provides easy way to Mock Service and use Classes which will helps in testing.    
* Support for extending and using other frameworks like BDD(cucumber) etc.

In this tutorial we look at.    
* Angular CLI.    
* Jasmine.    
* Karma.    
* Protractor.    
* Cucumber.    

Jasmine Framework    
* Jasmine is an open source testing framework for Javascript.
* Jasmine is Behavior Driven Development testing framework.    
* In BDD - the tests are written in non-technical language which makes it easy for Business.     
* It does not require any Javascript framework.    
* Easy to ready syntax, easy to maintain.    
* Jasmine has native supports for Async testing.(can do http request)    
* Jasmine supports Spy objects using which we can target an element(browser inspect elements) we want to test.    
```javascript
describe('appComponent',()=>{
  it('it should navigate', ()=>{
    console.log("navigated to page");
  })

  it('it should navigate2', ()=>{
    console.log("navigated to page2");
  })
})
```    

Karma Framework    
* Karma is an open source testing framework for Javascript.   
* Karma is created and maintained primarily by the core Angular team.    
* The framework is natively integrated into the Angular apps by default.    
* Since it's integrated, we can easily run our tests from the CLI console.    
* One of the striking features is the ability to run on different browser resolutions
like Tablet, Mobile ect.    
* Karma is used for running and executing the test scripts.    
* Hence the framework plays well with other Javascript frameworks like Jasmine, Mocha etc.    
* The framework can integrated right into the build pipelines which means it will run in our build and deployment pipelines.   


Unit Tests.

1. Each of the unit test file will having ending with spec.ts

2. to run unit test
```bash
ng test
```


E2E Tests.

1. The end to end test scripts are located in the e2e folder. .e2e-spec.ts file

2. to run E2E test
```bash
ng e2e
```

3. It would give report to tests passed and failed.   
4. Angular uses Protractor for running the end to end tests.    
5. To change the default config (config located in protractor.conf.js file).


Test Code Coverage Report

1. Angular has support for generating code Coverage test report.    
2. Most, if not all, clients will ask you to submit the test code Coverage report.    
3. If the code coverage is more than 85% - your code is considered to be good.   
4. We can generate code coverage for Unit Tests.    
5. to run test code coverage.    
```bash
$ ng test --code-coverage=true
```    
6. above cmd we can add to package.json script.
```json
"scripts"{
  "test:coverage": "ng test --code-coverage=true"
}
```    
and to run
```bash
$ npm run test:coverage
```   

Skip Test in Angular     

to skip test when app init.(not generating .spec.ts file)     
```bash
$ ng new app-name --skip-tests    
```  
to skip testing exists project(don't do until pro tester)    
  go to Angular.json and set "SkipTests":true

to skip test special test case.
  add "x" in front of the tests.
  * Xdescribe
  * Xit

to force run sepcified test case
fdescribe('des main', ()=>{
  it('des test', ()=>{})
  })

Write Tests in Jasmine

1. basic concepts
   Describe : A test suite begins with a call to the global Jasmine function
              describe with two parameters(a string and a function )
              inside describe can have multiple test spec (it())
   Specs : Specs are defined by calling the global Jasmine function it, Which, likes
           describe takes a string and a function. eg expect(10).toBe(10) > tset pass
   Expect : Expectations are build with the function expect which takes a value,
            called the actual.  
            inside it() statement can have expect value  
   Matcher : It is chained with a Matcher function, which takes the expected value.


```typescript
fdescribe('ListOrdersComponent', ()=>{
  it('First Test Script', ()=>{
      var tax = 10 * 2;
      expect(tax).toBe(10);
  });
})
```

Angular Test Spec In Detail    

1. TestBed, Async are Import from built-in modules.    
2. Importing Required Modules.
3. Import required components.    
4. BeforeEach methods are method make ground work before start testing.    
5. TestBed.configureTestingModule({}) is import of test config file.    
6. A fixture a wrapper for the component and it's template.    


```typescript
// importing required classes and interfaces
import { async, ComponentFixture, TestBed } from '@angular/core/testing';
// import component that we are going to test. we can import more components(child parent components )
import { ReviewsComponent } from './reviews.component';

//
describe('ReviewsComponent', () => {
  let component: ReviewsComponent;
  // fixture is wrapper around the component
  // using fixture we can get properties of component class and template.
  // queryElement = fixture.debugElement.queryElement.query((By.css('.brand')));
  let fixture: ComponentFixture<ReviewsComponent>;

  // beforeEach : before running have to make some ground work.
  beforeEach(async(() => {
    // configure testing module  
    // module - import components, providers etc.
    // this is like Module in Angular.    
    TestBed.configureTestingModule({
      declarations: [ ReviewsComponent ]
    })
    .compileComponents();
  }));

  // TestBed -> Pipe, Directive, module which you cannot provide data directly we can override to Mock Data.

  beforeEach(() => {
    // using fixture we can access the component's class properties as well as template elements(css, html).    
    fixture = TestBed.createComponent(ReviewsComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });

});

```


AAA Pattern in Angular Tests

AAA Pattern is a design pattern which help you design and think in a way to arrange test.  

Arrange - arrange everything like setup ground work for working with tests for execution.(ground work before execute inside 'beforeEach' function )    
Act - Act on your unit test case, calling methods, processing data etc.    
Assert - Verifying the actual data of test result and expected data.( expect().toBeTruthy(); )   


BeforeEach Method

TestBed (ATB)    

1. The TestBed is the first and largest of the Angular testing utilities.   
2. Configures and initializes environment for unit testing and provides methods for creating components and services in unit tests.    
3. It creates a dependency injection (DI) context and allows us to override provides, services, and whole modules.    
4. It complies, instantiates, and renders to HTML our components attaching them to the fixture instance. Any module, component or service that your tested component needs have to be included in the testbed.    

```typescript
// config TestBed before test inside "beforeEach" as async
beforeEach(async(() => {
  TestBed.configureTestingModule({
    imports: [
      RouterTestingModule // import all module related to test
    ],
    declarations: [
      AppComponent // import all component related to test
    ],
    providers: [] // import all providers related to test
  }).compileComponents();
}));
```

to run test case 
```bash
$ ng test # execute all test cases   
$ ng test --include src\app # run test inside special folder 
```

to diable particular test case.(use xit instead of it)
```typescript
// just on test case
  xit('show the addion result', ()=>{
    expect(Addition(1,2)).toBe(3)
  });

 // for all test cases of component
  xdescribe('AppComponent', () => {
   /*  ...  */
});
```

## basic test case.   
```typescript
describe('AppComponent', () => {
  beforeEach(async () => {
    await TestBed.configureTestingModule({
      imports: [
        RouterTestingModule
      ],
      declarations: [
        AppComponent
      ],
    }).compileComponents();
  });

  // basic test case    
  it('My test case', ()=>{
    expect(true).toBe(true)
  })
});
```

## test case external function from file.   

```typescript
/* calculator.ts */
export function Addition(num1:number, num2:number):number{
    return num1 + num2;
}
```

```typescript
import { Addition } from './calculator'; // import file

describe('AppComponent', () => {
  beforeEach(async () => {
    await TestBed.configureTestingModule({
      imports: [
        RouterTestingModule
      ],
      declarations: [
        AppComponent
      ],
    }).compileComponents();
  });

  // test case    
  it('show the addion result', ()=>{
    expect(Addition(1,2)).toBe(3)
  });
});
```

## Jasmin Matchers.  

Inbuilt Matchers 
* The matchers which are inbuild in the jasmine framework are called inbuild matcher. The user can easily use it implicitly.   

Custom Matchers 
* The matchers which are not present in the inbuild system library of jasmine is call as custom matcher. Custom matcher needd to be defined explicitly(). 


## ToBe and ToEqual  

we can use "toBe" for primitives like strings, numbers or Booleans, everything else use "toEqual".   

```typescript
import { Addition } from './calculator'; // import file

describe('AppComponent', () => {
  beforeEach(async () => {
    await TestBed.configureTestingModule({
      imports: [
        RouterTestingModule
      ],
      declarations: [
        AppComponent
      ],
    }).compileComponents();
  });

  it('toBe and toEqual primitives case', ()=>{
    var a = "Hello";
    var b = "Hello";
    expect(a).toBe(b); // pass
    expect(a).toEqual(b); //  pass
  });
  it('toBe and toEqual none primitives test case', ()=>{
    var a = [1,2];
    var b = [1,2];
    expect(a).toBe(b); // fail
    expect(a).toEqual(b); // pass
  });
});
```

## toBe(true), toBeTrue() and toBeTruthy() , toBeFalse() and toBeFalsy()    

toBe() > actual === expected
toBeTrue() > actual === true (primitive boolean and boolean object)
toBeFalse() > actual == false (primitive boolean and boolean object)

toBeTruthy() and toBeFalsy() 
```typescript
expect(true).toBeTruthy(); // true
expect('1').toBeTruthy(); // true  
expect(0).toBeTruthy(); // false
expect(undefined).toBeTruthy(); // false
expect(NaN).toBeTruthy(); // false 
expect(false).toBeTruthy() // false
expect('').toBeTruthy() // false
```

we are frequently use "toBeTruthy" to check is component created or not.    
```typescript
  it('should create the app', () => {
    const fixture = TestBed.createComponent(AppComponent);
    const app = fixture.componentInstance;
    expect(app).toBeTruthy();
  });
```

## toBeGreaterThan() ,toBeGreaterThanOrEqual() ,toBeLessThan() 

```typescript
  it('toBeGreaterThan test case', ()=>{
    var a = 5;
    expect(a).toBeGreaterThan(4); // pass
    expect(a).toBeGreaterThan(6); // fail 
    expect(a).toBeGreaterThan(5); // fail 
    expect(a).toBeGreaterThanOrEqual(5); // pass
    expect(a).toBeGreaterThanOrEqual(4); // pass
    expect(a).toBeLessThan(5); // fail
    expect(a).toBeLessThanOrEqual(5); // pass
    expect(a).toBeLessThan(6); // pass
  });
```

## toMatch() and toBeCloseTo() 

The 'toMatch' matcher should be applied successfully for regular expressions.   
```typescript
  it('Jusmin Matcher - Match function', ()=>{
    var input = "The dotnetoffice tutorials";
    var strPhone = "011-789-56-67";
    expect(input).toMatch(/dotnetoffice/); // pass
    expect(input).toMatch(/dotnetoffice/i); // pass
    expect(input).not.toMatch(/dot1/); // pass
    expect(strPhone).toMatch(/\d{3}-\d{3}-\d{2}-\d{2}/); // pass
  });
```   

The 'toBeCloseTo' is used to check whether a number is close to another number, up to given level of decimal percision.  
```typescript
  it('Jusmin Matcher - toBeCloseTo', ()=>{
    var pi = 3.1415926, e = 2.78
    expect(pi).not.toBeCloseTo(e); // pass
    expect(pi).toBeCloseTo(e,0); // pass > for 0 decimal place 3=3
    expect(4.334).toBeCloseTo(4.334); // pass > 4.334 = 4.334
    expect(4.334).toBeCloseTo(4.3345,1); // pass > for 1 decimal place 4.3 = 4.3
    expect(4.334).toBeCloseTo(4.3345,1); // pass > for 1 decimal place 4.3 = 4.3
    expect(4.334).not.toBeCloseTo(4.3, 2); // pass > for 2 decimal place 4.33 != 4.30
    expect(4.223).not.toBeCloseTo(4.22, 3); // pass > for 3 decimal place 4.223 != 4.300
    expect(4.223).not.toBeCloseTo(4.22,4); // pass > for 2 decimal place 4.2230 != 4.3000
  });
```   

## toBeDefined and toBeUndefined    

The 'toBeDefined' matcher should be applied successfully to compares against defined.    
The 'toBeUndefined' matcher should be applied successfully to compares against undefined.  

```typescript
  it('Jusmin Matcher - toBeDefined ', ()=>{
     var MyObj ={
      foo: 'foo'
     }; // object defined
     var Myfunction = (function(){})(); // function not defined
     var strUndefined; // variable not defined
     expect("The Dotnet office").toBeDefined(); // pass
     expect(MyObj).toBeDefined(); // pass
     expect(MyObj.foo).toBeDefined(); // pass
     expect(Myfunction).not.toBeDefined(); // pass
     expect(strUndefined).not.toBeDefined(); // pass
     // not.toBeDefined() = toBeUndefined()
  });
```

##  tobenull() ,tocontain() ,tobeNan() , toBePositiveInfinity, toBeNegetiveInfinity matcher   

```typescript
  it('Jusmin Matcher - tobenull ', ()=>{
     var nullValue = null;
     var valueUndefined; // undefine
     var notNull = "notNull";
     expect(null).toBeNull(); // pass
     expect(nullValue).toBeNull(); // pass
     expect(valueUndefined).not.toBeNull(); // pass
     expect(notNull).not.toBeNull(); // pass
  });
```
```typescript
  it('Jusmin Matcher - toContain ', ()=>{
     var MyArray = ["jusmine", "Dotnetoffice", "Tutorials"];
     expect([1,2,3]).toContain(2); // pass
     //expect([1,2,3]).toContain[2]; ?
     expect([1,2,3]).toContain(2,3); // pass
     expect(MyArray).toContain("jusmine"); // pass
     //expect(MyArray).toContain["jusmine"]; // pass
     expect([1,2,3]).not.toContain(4); // pass
     expect(MyArray).not.toContain("dot"); // pass
  });
```
```typescript
  // tobeNan for match undetermined value
  it('Jusmin Matcher - tobeNan ', ()=>{
    expect(0/0).toBeNaN(); // pass
    expect(0/5).not.toBeNaN(); // pass
  });

  it('Jusmin Matcher - toBePositiveInfinity and toBeNegativeInfinity', ()=>{
    expect(1/0).toBePositiveInfinity(); // pass
    expect(-1/0).toBeNegativeInfinity(); // pass
  });
```

## BeforeEach, AfterEach, BeforeAll, AfterAll in Jasmin    

beforeEach() is run before each test in a describe.    
afterEach() is run after each test in a describe.   

to show test cases will not run in order

```typescript
describe('AppComponent', () => {
  it("test 1",()=>{
    console.log("test 1");
  });
  it("test 2",()=>{
    console.log("test 2");
  });
  it("test 3",()=>{
    console.log("test 3");
  });

});

/* result > 
   test 1
   test 3 
   test 2
*/
```

use beforeEach, afterEach, beforeAll, afterAll

```typescript
  beforeAll(()=>{
    console.log("before all");
  })
  afterAll(()=>{
    console.log("after all");
  });
  beforeEach(()=>{
    console.log("before each");
  })
  afterEach(()=>{
    console.log("after each");
  })
  it("test 1",()=>{
    console.log("test 1");
  });
  it("test 2",()=>{
    console.log("test 2");
  });
  it("test 3",()=>{
    console.log("test 3");
  });

  /* reuslt > 
    before all
    before each 
    test 2
    after each
    before each 
    test 1 
    after each
    before each 
    test 3
    after each
    after all
  */
 ```

here by using beforeEach we can create new instence of component for every test case.

```typescript
export class AppComponent {

  public count:number=0;

  increaseCount(): void{
    this.count +=1;
  }
  decreaseCount(): void{
    this.count -=1;
  }
}
```

```typescript
  var comp: AppComponent | null;
  beforeEach(()=>{
    comp = new AppComponent()
  })
  afterEach(()=>{
    comp = null;
  })
  it("increase count",()=>{
    comp?.increaseCount();
  });
  it("decrease count",()=>{
    comp?.decreaseCount();
  });
 ```

 ## Arrange-Act-Assert(AAA) Pattern   

 * Arrange inputs and targets.    
 * Act on the target behavior.   
 * Assert expected outcomes.  

 ```typescript
   it("test",()=>{
    // Arrange
    let comp = new AppComponent();

    // Act
    let msg = comp.showMessage("Hello");
 
    // Assert
    expect(msg).toBe("Hello");
  });
 ```  

 ## TestBed and Component Fixture   

 The Angular Test Bed(ATB) is a higher level Angular Only testing framework that allows us to easily test behaviors that depend on the Angular Framework. 

 It's allows to    
 1. test the interaction of a directive or component with its template.   
 2. easily test change detection.   
 3. provide methods to create components and services for unit test case.   
 4. test and use Angular's DI(dependency injection) framework.   
 5. test using the NgModule configuration we use in our application.   
 6. test user interaction via clicks and input fields.  


initializing spec file for component 
 ```typescript
import { ComponentFixture, TestBed } from '@angular/core/testing';
// import { AppRoutingModule } from '../app-routing.module';
import { StudentComponent } from './student.component';

describe('StudentComponent', () => {
  let component: StudentComponent;
  let fixture: ComponentFixture<StudentComponent>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [ StudentComponent ], // default own component imported
      providers: [], // add services here 
      imports: [] // // add modules here ex: [AppRoutingModule] 
    })
    .compileComponents(); // compile and provide for test

    // allow to access html, scss, and ts of component
    fixture = TestBed.createComponent(StudentComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });
});
 
```   
## service file with test  

specially add 'HttpClientModule' to 'service.spect.ts' file.

```typescript
/* student.service.spect.ts */
import { HttpClientModule } from '@angular/common/http'; // + add
import { TestBed } from '@angular/core/testing';

import { StudentService } from './student.service';

describe('StudentService', () => {
  let service: StudentService;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [HttpClientModule], // + add
    });
    service = TestBed.inject(StudentService);
  });

  it('should be created', () => {
    expect(service).toBeTruthy();
  });
});
```
```typescript
/* student.service.ts */
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http'; // + add

@Injectable({
  providedIn: 'root'
})
export class StudentService {
  constructor(private http: HttpClient) { } // + add
}
```

```typescript
/* app.module.ts */

/* ... */
import { HttpClientModule } from '@angular/common/http';
/* ... */

@NgModule({
  declarations: [
    AppComponent,
    StudentComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule, // + add after 'BrowserModule'
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```


##  SpyOn to mock and Stub methods  

this is help to mock the execution of th Angular method.   

* Stub : a dummy piece of code that lets the test run, but you don't care what happens to it.    
* Mock : a dummy piece of code, that intercepts some calls to a real piece of code, allowing you to verify calls without replacing the entire origin object.    

This example show how we can test api call even we don't have real working api.

```typescript 
/* student.component.ts */

import { Component } from '@angular/core';
import { StudentService } from './student.service';

@Component({
  selector: 'app-student',
  templateUrl: './student.component.html',
  styleUrls: ['./student.component.scss']
})
export class StudentComponent {
  sum:number =0;
  result: any ;
  constructor(private service:StudentService) { }

  calculate(num1:number, num2:number){
    this.sum = num1 + num2;
    return this.sum;
  }

  saveData(): void{
    let info={
      sumVal: this.calculate(5,5),
      name: "Dot Net Office"
    };
    this.saveDataIntoConsole(info);
    this.service.saveDatails(info).subscribe(res=>{
      this.result = res;
    })
  }

  studentResult(): string{
    if(this.calculate(10,20) >= 40){
      return "Pass";
    }else{
      return "Fail";
    }
  }

  saveDataIntoConsole(info:any):void{
    console.log(info);
  }

}
```
```typescript 
/* student.component.spec.ts */

import { HttpClientModule } from '@angular/common/http'; // + add
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { of } from 'rxjs';
import { StudentComponent } from './student.component';
import { StudentService } from './student.service'; // + add


describe('StudentComponent', () => {
  let component: StudentComponent;
  let fixture: ComponentFixture<StudentComponent>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [ StudentComponent ], // default own component imported
      providers: [StudentService], // + add
      imports: [HttpClientModule] // + add
    })
    .compileComponents();

    fixture = TestBed.createComponent(StudentComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });

  // custom test case 
  it("SpyOn method 1", ()=>{ // + add
    spyOn(component, 'calculate'); // start spy on 'calculate' method on component 
    component.saveData(); // call 'saveData' method on component
    expect(component.calculate).toHaveBeenCalled() // check 'calculate' method call in 'saveData' method
  })

  // custom test case 
  it("SpyOn method 2", ()=>{ // + add
    spyOn(component, 'calculate').and.returnValues(10,20); // set return values to 'calculate' method
    const rusult = component.studentResult();
    expect(rusult).toBe("Fail"); // pass
  })

  // custom test case 
  it("SpyOn method 3", ()=>{ // + add
    // import service 
    const service = fixture.debugElement.injector.get(StudentService);
    spyOn(service, 'saveDatails').and.callFake(()=>{ // create fake response to method in service file.
      return of({
        "result1":200
      })
    });
    component.saveData();
    expect(component.result).toEqual({
      "result1":200
    }); // pass
  })

  // custom test case 
  it("SpyOn-Stub method 4", ()=>{ // + add
    // import service 
    const service = fixture.debugElement.injector.get(StudentService);
    spyOn(service, 'saveDatails').and.callFake(()=>{ // create fake response to method in service file.
      return of({
        "result1":200
      })
    });
    spyOn(component, "saveDataIntoConsole").and.stub(); // not care about "saveDataIntoConsole" method response
    component.saveData();
    expect(component.result).toEqual({
      "result1":200
    }); // pass
  })

});
```
```typescript 
/* student.service.ts */

import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})
export class StudentService {

  constructor(private http: HttpClient) { }

  saveDatails(info:any){
    return this.http.post('https://localhost:4200', info);
  }
}
```

## Change detection   

Change Detection is the backbone of the Angular framework, and each component has it's own change detector and re-render view to sync with component.   

example shows without clicking button by execute it's function and check is template changed or not.

```typescript
/* student.component.spec.ts */

import { ComponentFixture, TestBed } from '@angular/core/testing';
import { StudentComponent } from './student.component';

describe('StudentComponent', () => {
  let component: StudentComponent;
  let fixture: ComponentFixture<StudentComponent>;
  let h1: HTMLElement; //  + add
  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [ StudentComponent ], 
      providers: [], 
      imports: [] 
    })
    .compileComponents();
   
    fixture = TestBed.createComponent(StudentComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
    h1 = fixture.nativeElement.querySelector('h1'); // + add
  });

  it('verify the h1 element value', () => { // + add
    component.studentSchoolResult();
    fixture.detectChanges() // this line makes update template. otherwise this will fail test.
    expect(h1.textContent).toBe(component.studentResult);
  });
});
```

```html
<!-- student.component.ts  -->
<button (click)="studentSchoolResult()">Get Result</button>
<h1>{{studentResult}}</h1>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-student',
  templateUrl: './student.component.html',
  styleUrls: ['./student.component.scss']
})
export class StudentComponent {

  constructor() { }

  studentResult!:string;

  studentSchoolResult(): string{
    const marks:number = 24;
    if(marks > 50){
      this.studentResult = "Pass";
    }else{
      this.studentResult = "Fail";
    }
    return this.studentResult;
  }
}
```   

## Debug Element & DOM events (tutorial 20)
