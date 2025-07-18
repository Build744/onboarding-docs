# CSharp Basics Project Description
## 🔧 General Instructions – Object-Oriented Programming (OOP)

For each of the following exercises, you must **implement a solution using object-oriented programming principles**. This means:

- You must **model relevant entities** as **classes**;
- Your classes must have appropriate **attributes** and **methods**;
- You must **instantiate objects** when needed to use the defined functionalities;
- Your code must **promote encapsulation, reusability, and readability**.

---

## 1. 🧠 Exercise: **FizzBuzz**

### 🔎 Context  
FizzBuzz is a classic exercise often used to evaluate understanding of conditional logic.

### 🎯 Goal  
Return a string based on the divisibility of an integer number.

### 📝 Business Rules  
- If the number is divisible by **3 and 5** → return `"FizzBuzz"`.
- If the number is divisible **only by 3** → return `"Fizz"`.
- If the number is divisible **only by 5** → return `"Buzz"`.
- Otherwise → return the number as a string.

### 🧪 Test Cases  
| Input | Expected Output |
| ----- | --------------- |
| 15    | "FizzBuzz"      |
| 9     | "Fizz"          |
| 10    | "Buzz"          |
| 7     | "7"             |
| 2     | "2"             |

---

## 2. 📞 Exercise: **North America Phone Number Parser**

### 🔎 Context  
In North American countries (like the United States and Canada), phone numbers are standardized in the **NPA-NXX-XXXX** format (10 digits). This exercise involves string manipulation and exception handling to verify number validity.

### 🎯 Goal  
Analyze a 10-digit number and format it as `(NPA)NXX-XXXX`.

### 📝 Business Rules  
#### `Parse(string number)`  
- Split the string into:
  - **NPA (Area code)**: first 3 digits
  - **NXX (Central Office code)**: next 3 digits
  - **XXXX (Line Number)**: last 4 digits  
- Validations:
  - The number must contain exactly **10 digits**.

#### `ToString()`  
- Returns the formatted version: **`(NPA)NXX-XXXX`**

### 🧪 Test Cases
| `Parse` Input | `ToString()` Output |
| ------------- | ------------------- |
| "5145551234"  | "(514)555-1234"     |
| "2120007890"  | "(212)000-7890"     |

---

## 3. 📐 Exercise: **Quadratic Equation Solver**

### 🔎 Context  
Quadratic equations frequently appear in mathematics and science. This exercise allows practice in implementing mathematical formulas, handling numeric types, and managing multiple output cases (0, 1, or 2 solutions).

### 🎯 Goal  
Write a function that solves a quadratic equation of the form:

```
ax² + bx + c = 0
```
where `a`, `b`, and `c` are real numbers provided by the user.

### 📝 Business Rules  

#### 🔢 Steps to follow:

1. **Calculate the discriminant (Δ)**  
   Use the **complete formula**:
   ```
   Δ = b² - 4ac
   ```

2. **Solve based on Δ:**
   - If **Δ > 0**  
     → Two real roots:  
     ```
     x1 = (-b + √Δ) / (2a)
     x2 = (-b - √Δ) / (2a)
     ```
     → Return `[x1, x2]`
   - If **Δ == 0**  
     → One real root:  
     ```
     x = -b / (2a)
     ```
     → Return `[x]`
   - If **Δ < 0**  
     → No real roots  
     → Return `[]` (empty array)

3. **Special case:**
   - If `a == 0`, it's **not a quadratic equation**.

### 🧪 Test Cases  

| a   | b   | c   | Discriminant (Δ) | Result             |
| --- | --- | --- | ---------------- | ------------------ |
| 1   | -3  | 2   | 1                | [2, 1]             |
| 1   | 2   | 1   | 0                | [-1]               |
| 1   | 1   | 1   | -3               | []                 |
| 0   | 2   | 1   | —                | Exception expected |

---

## 4. 🌡️ Exercise: **Temperature Converter**

### 🔎 Context  
Understanding conversion formulas between **Kelvin**, **Celsius**, and **Fahrenheit** provides practice with mathematical functions, unit handling, and writing clear methods.

### 🎯 Goal  
Convert a given temperature between three units: **Kelvin**, **Celsius**, and **Fahrenheit**.

### 📝 Business Rules  

#### 🔁 Conversions

- `Celsius -> Fahrenheit`: `(C × 9/5) + 32`
- `Celsius -> Kelvin`: `C + 273.15`
- `Kelvin -> Celsius`: `K - 273.15`
- `Fahrenheit -> Kelvin`: `((F - 32) × 5/9) + 273.15`
- `Kelvin -> Fahrenheit`: `((K - 273.15) × 9/5) + 32`

#### 📌 Constraints
- Temperature in **Kelvin** cannot be < 0 

### 🧪 Test Cases  
| Conversion Type | Input | Expected Output |
| --------------- | ----- | --------------- |
| C → F           | 0°C   | 32°F            |
| F → C           | 212°F | 100°C           |
| C → K           | 100°C | 373.15 K        |
| K → F           | 0 K   | -459.67°F       |
| F → K           | 32°F  | 273.15 K        |
| Invalid K       | -10 K | Exception       |