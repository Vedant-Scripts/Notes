1. **JS Closures**
    A closure is a function that remembers its outer variables even after the outer function has finished executing.
    
    - **Key Takeaway**: Closure is not about access, its about "retaining access of the variable even after execution ended"
    - Because the inner fn -> referencing the variable and is in use. so the variable, is in memory even after the outer fn is done executing.
    
    ```javascript
    const outerfn = () => {
    let count = 0;
    return () => console.log('count:', ++count);

    }
    const innerfn = outerfn(); // outer finished here
    innerfn(); // 1
    innerfn(); // 2  (still the variable is kept in memory since it is used/referenced by inner fn)
    ```

2. **Var, const, let**
   - var is function scoped, can be reassigned, redeclared.
   - let and const block scope, let can be reassigned but not redeclare. Const cant do any
   - hoisting means - js knows about the varibale declaration before the execution 
   - var -> initialized with undefined (will give undefined till declaration line arrives )
   - let and const -> not initialized (temporal dead zone).( : Reference Error wont run the variable until the vaible declaration has arrived)
    ```js
    function () => {
        console.log(a); // undefined  => HOISTING and intialized 
        // var
        if (true) {
            var a = 10;
        }
        console.log(a); // can be accessed
        a = 8; // can be re assigned 
        var a = 5; //can be redeclared

        // let and const
        if (false) {
            console.log(y);  // hoisted but not initialized  (REFERENCE ERROR)

            let y = 7;
            let y = 9; // error
            y = 8; // can be reassigned 
            const z = 10;
            z = 10; // error
            const z = 5; // error

        }
        console.log(y); // can't be accessed block
        console.log(z);// can't be accessed since block
    }

    ```

3. 