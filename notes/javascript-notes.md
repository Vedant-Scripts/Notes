1. ### Execution Context Javascript
   - **Definition:** The environment where JavaScript code is evaluated and executed. It acts as a "container" for the code currently running.
   - **How it Works:** Before execution, the engine **parses** the code to allocate memory for variables and functions (Creation Phase), then runs the code line-by-line (Execution Phase).

    ### Types of EC
    1. **Global Execution Context (GEC)**
    - **Created when:** The JS engine first loads the script.
    - **Scope:** Represents the global scope. (can be accessed any where in the code inside other fn's or loops)
    - **Note:** Only one GEC exists per program.

    2. **Function Execution Context (FEC)**
    - **Created when:** A function is **invoked** (called).
    - **Scope:** Represents that specific function's local scope.
    - **Note:** Each function call gets its own unique EC.
  
2. ### The Call Stack
   - **Role:** A mechanism to track the order of function execution. It remembers "where we are" in the code.
   - **Adding (Push):** When a function is called, it’s added to the top of the stack.
   - **Nesting:** If a function calls another function, the new one is added further up. The engine pauses the current function to run the new one.
   - **Removing (Pop):** When a function finishes, it is removed from the stack, and execution resumes exactly where it left off in the previous function.
   - **Error:** If too many functions are added without finishing (like infinite recursion), it triggers a **"Stack Overflow."**
  
3. ### JS Execution: Line-by-Line
   - **Single-Threaded:** JS can only execute **one** command at a time in a single sequence.
   - **Two-Pass System:** It doesn't just "start" at line 1. It follows a strict two-step process:

   1. **Memory Phase (Creation):** 
      - Scans the entire file **before** running.
      - Allocates memory for variables and functions (**Hoisting**).
      - `var` is set to `undefined`; `functions` are stored in full.

   2. **Execution Phase (Code):**
      - Runs code top-to-bottom.
      - Assigns actual values to variables.
      - Executes function calls by pushing them to the **Call Stack**.

   - **Synchronous:** Each line must finish before the next one starts (unless it's Asynchronous code like `setTimeout`).
  
4. **JS Closures**
    - **Definition:** A closure is a function that remembers its outer variables even after the outer function has finished executing.
    - **The "Why":** Normally, a function's variables are deleted when it finishes (popped from the stack). A **Closure** prevents this because the inner function still holds a **reference** to those variables. -> variable is in use and is in memory even after the outer fn is done executing.
    
    ```javascript
    const createCounter  = () => {
    let count = 0; // This should die when the function ends...
    return () => console.log('count:', ++count); // ...but this inner function keeps it alive!

    }
    const innerfn = createCounter (); // outer finished here
    counter(); // 1
    counter(); // 2  (still the variable is kept in memory since it is used/referenced by inner fn)
    ```

5. **Var, const, let**
    - **Scope:**
     - `var`: **Function-scoped**. Accessible anywhere within the function it's defined in.
     - `let` & `const`: **Block-scoped**. Only accessible within the `{ }` where they are declared.

   - **Hoisting & Initialization:**
     - **All are hoisted** (JS knows they exist before execution).
     - `var`: Initialized with `undefined`. You can use it before its declaration line (returns `undefined`).
     - `let` & `const`: Not initialized. They stay in the **Temporal Dead Zone (TDZ)**. Accessing them before declaration causes a `ReferenceError`.

   - **Reassignment & Redeclared:**
     - `var`: Can be reassigned **and** redeclared.
     - `let`: Can be reassigned, but **not** redeclared in the same scope.
     - `const`: Cannot be reassigned **or** redeclared (must be initialized immediately).

    ```js
    function example() {
    console.log(a); // undefined (Hoisted & Initialized)
    var a = 10;
    var a = 5;      // Redeclare OK

        if (true) {
            // console.log(b); // ReferenceError (TDZ - Hoisted but NOT initialized)
            let b = 20;
            // let b = 30;  // SyntaxError: Already declared
            b = 40;         // Reassign OK
            
            const c = 50;
            // c = 60;      // TypeError: Assignment to constant
        }
    // console.log(b); // ReferenceError: b is block-scoped to the 'if'
    }
    ```
6. ### Lexical Scope & Scope Chain
   - **Lexical Scope:** Scope is determined by where a function is **written**, not called.
   - **Lexical Environment:** Local Memory (where its own variables and functions live) + Reference to Parent Scope ( a pointer to the lexical env of is parents scope).
   - **Scope Chain:** The process of searching for a variable by jumping from the local scope to parent scopes, all the way to the Global scope. (where the parent reference is null) If still not found, it throws a *ReferenceError*
   - **One-Way Street:** Inner functions can see "out" to parents, but parents cannot see "in" to children.

7. ### The "this" Keyword
   - **Definition:** A reference to the current execution context (the "owner" of the executing code).
   - **Rule of Thumb:** Look to the **left of the dot** at the call site. If it's `user.greet()`, then `this` is `user`.
   - **Arrow Functions:** Special exception. They don't have their own `this`; they "look up" to their parent's `this`.
   - **Strict Mode:** In strict mode, `this` in a regular function defaults to `undefined` instead of the global `window`.
     - ### **The `this` Keyword (Call-site Rules)**
     - **Simple Call:** `func()` → `window` (or `undefined` in strict mode).
     - **Method Call:** `obj.method()` → the **object** before the dot.
     - **Constructor:** `new Func()` → the **newly created instance**.
     - **Arrow Fn:** `() => {}` → **Lexical** (inherits from parent scope).

8. ### **Arrow vs. Normal Functions**
   - **`this` Binding:** Normal fns have **Dynamic** `this` (depends on call-site, not where it is written); Arrow fns have **Lexical** `this` (inherits from parent, depends on where it is written).
   - **Constructors:** Normal fns can be called with `new`; Arrow fns **cannot** (no `prototype`).
   - **Arguments:** Normal fns have an built-in `arguments` object; Arrow fns **do not** (use `...args` instead).

9. **The Event Loop**
   - **Definition:** A mechanism that allows **non-blocking, asynchronous** operations in a single-threaded environment.
   - **Role:** It monitors the **Call Stack** and coordinates when tasks from the queues move to the stack.

      #### **Key Components**
      1. **Call Stack:** Executes synchronous code (LIFO). (Async FUNCTIONS run on call stack too, but PAUSE at await) -> Everything runs synchronously UNTIL await.
      2. **Web/Node APIs:** Background environments that handle "slow" tasks (e.g., `setTimeout`, `fetch`, DOM events).
      3. **Microtask Queue:** **High-Priority** tasks. Holds `Promises (.then/.catch)` and `async/await`.
      4. **Macrotask Queue:** **Lower-Priority** tasks. Holds `setTimeout`, `setInterval`, and `I/O`.

      #### **The Execution Cycle (Priority)**
      5. **Execute Synchronous Code:** Runs everything in the Call Stack until empty.
      6. **Clear Microtasks:** Once the stack is empty, the loop executes **all** pending Microtasks.
      7. **Execute One Macrotask:** The loop picks **exactly one** task from the Macrotask Queue and pushes it to the stack.
      8. **Render:** (Browser only) The UI may update before the cycle restarts.

      #### **Interview Summary**
      - **Microtasks > Macrotasks:** Promises always resolve before the next `setTimeout` runs.
      - **Blocking:** If the Call Stack is busy with a heavy loop, the Event Loop cannot move tasks from the queues, "freezing" the app.
  
9. ### NODE CODE SNIPPETS (IN JS/TS)
   - Middleware -> Is a fn
   - Middleware Factory -> It is a FN that returns a fn: (helps in not passing extra params at route layer just the required one, and everything else in middleware factory code)
      ```ts
            export const requireRole = (role: Role) => {
            return (req: Request, res: Response, next: NextFunction) => {
               const { user } = res.locals;
               if (user.role !== role) return res.status(403).json({ message: "You dont have access to this resource" });
               next();
            };
         }
      ```
# 10. Auth System Notes: JWT + Sessions + Rotation
   -  ```js
         Session {
         id (sessionId)
         userId
         refreshTokenHash
         device
         expiresAt
         revokedAt
         createdAt
         updatedAt
         }
      ```
### 🔐 Token Definitions
- **Access Token (Stateless)**
    - **Lifespan:** Short-lived (e.g., 15 min).
    - **Purpose:** API authentication.
    - **Payload:** Contains `userId`, `role`, and `sessionId`.
    - **Efficiency:** No DB lookup required per request.
- **Refresh Token (Stateful)**
    - **Lifespan:** Long-lived.
    - **Purpose:** Issues new access tokens.
    - **Security:** Store as `refreshTokenHash` in DB (never raw).
    - **Role:** Acts as the persistent "key" to a session.

### 🏠 Session Management
- **Definition:** Represents one unique logged-in device or user instance.
- **Storage:** Managed in the DB as the ultimate "Source of Truth."
- **Constraint:** One session entry per login/device.

### 🔁 The Refresh Flow
1. **Lookup:** Retrieve the session from DB using `sessionId`.
2. **Verify:** Hash incoming raw token and compare to stored `refreshTokenHash`.
3. **Rotate:** Issue a brand-new token pair and update the DB with the new hash.
4. **Detect:** If a previously used (rotated) token is presented, trigger **Reuse Detection**.
5. **Revoke:** On reuse detection, delete the entire session to block the attacker.

1.  **Lookup:** Retrieve the session from DB using `sessionId`.
2.  **Verify:** Hash the incoming raw token and compare it to the stored `refreshTokenHash`.
3.  **Rotate:** Issue a brand-new token pair and update the DB with the new hash.
4.  **Detect:** If a previously used (rotated) token is presented, trigger **Reuse Detection**.
5.  **Revoke:** On reuse detection, delete the entire session to block the attacker.

### ✅ Quick Checklist
- **DO:** Rotate tokens on every single refresh.
- **DO:** Use short-lived access tokens to limit exposure.
- **AVOID:** Hitting the DB for every standard API request.
- **AVOID:** Storing raw refresh tokens or creating a new session entry on every refresh.
