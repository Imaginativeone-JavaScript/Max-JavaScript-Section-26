Section 26: Meta-Programming: Symbols, Iterators, Generators, Reflect API & Proxy API 0 / 11 | 57min
- [ ] 466. Module Introduction 2min
- [ ] 467. Understanding Symbols 8min

  ```javascript
  // "Library Land
  const uid = Symbol();
  console.log(uid);
  
  // "App Land" = Using the Library
  const: user = { // I want an id property that I don't want to be overwritten
    // id: 'p1',
    [uid]: 'p1', // Library internal id
    name: 'Max',
    age: 30
  };
  
  user.id = 'p2'; // This should not be possible (at first). Fixed by using [uid]
  ```

- [ ] 468. Well-known Symbols 5min
  - Built within the JavaScript Engine
  - MDN

  ```javascript
  // "Library Land
  const uid = Symbol();
  console.log(uid);
  
  // "App Land" = Using the Library
  const: user = { // I want an id property that I don't want to be overwritten
    // id: 'p1',
    [uid]: 'p1', // Library internal id
    name: 'Max',
    age: 30,
    [Symbol.toStringTag]: 'User' // I can view more info within an object, when I get [object Object] in the console.
  };
  
  console.log(user.toString()); // [object Object]
  ```
  
- [ ] 469. Understanding Iterators 6min

  ```javascript
  const company = {
    curEmployee: 0,
    employees: ['Max', 'Manu', 'Anna'];
    next() { // The next() function makes this into a loop-able object
      if (this.curEmployee >= this.employee.length) {
        return { value: this.curEmployee, done: true };
      }
      const returnValue = { 
        value: this.employees[this.curEmployee], 
        done: false 
      };
      this.curEmployee++;
      return returnValue;
    }
  }
  ```

- [ ] 470. Generators & Iterable Objects 1 1min

  ```javascript
  const company = {
    curEmployee: 0,
    employees: ['Max', 'Manu', 'Anna'];
    next() { // The next() function makes this into a loop-able object
      if (this.curEmployee >= this.employee.length) {
        return { value: this.curEmployee, done: true };
      }
      const returnValue = { 
        value: this.employees[this.curEmployee], 
        done: false 
      };
      this.curEmployee++;
      return returnValue;
    },
    // Create an "iteration generator" here
    [Symbol.iterator]: function* employeeGenerator() {
      
      let employee = company.next();
      yield employee.value;
      while(!employee.done) {
        employee = company.next();
      }
    }
  }

  for (const employee of company) {
    console.log(employee);
  }
  ```

- [ ] 471. Generators Summary & Built-in Iterables Examples 3min
- [ ] 472. The Reflect API 7min
  - API to control objects
  
  ```javascript
  const course = {
    title: "JavaScript the Complete Guide";
  };
  
  Reflect.setPrototypeOf(course, {
    toString() {
      return this.title;
    }
  });
  
  Reflect.defineProperty(course, 'price', { /* writeable, etc */ });
  ```
  
  - Subtle differences from the Object API
  
- [ ] 473. The Proxy API and a First "Trap" 9min
  - Tweak objects
  - Create "traps" for object operations
  - Step in and execute code
  
  ```javascript
  
  const courseHandler = {
    get(obj, propertyName) {
      console.log(propertyName);
      return obj[propertyName];
    }
  };
  
  const pCourse = new Proxy(course, courseHandler); // title (property) printed, as well as the value
  ```
  
- [ ] 474. Working with Proxy Traps 3min
- [ ] 475. Wrap Up 2min
- [ ] 476. Useful Resources & Links 1min
