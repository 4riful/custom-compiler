
---

# Simple Lang Compiler 🚀

This project showcases the design and implementation of a basic compiler, capable of tokenizing, parsing, and generating intermediate code for a custom programming language. The compiler is built using **C#** and includes a graphical user interface (GUI) to interact with the compilation process.

---

## 🚩 Table of Contents
1. [🌟 Overview](#overview)
2. [✨ Features](#features)
3. [⚙️ System Requirements](#system-requirements)
4. [📦 Setup and Installation](#setup-and-installation)
5. [💻 Usage](#usage)
    - [Input Code Example](#input-code-example)
6. [🛠️ Detailed Architecture](#detailed-architecture)
    - [Lexical Analysis](#lexical-analysis)
    - [Syntax Analysis](#syntax-analysis)
    - [Intermediate Code Generation](#intermediate-code-generation)
    - [Symbol and Temporary Tables](#symbol-and-temporary-tables)
7. [🎨 Graphical User Interface](#graphical-user-interface)
8. [📝 Example Output](#example-output)
9. [📈 Future Enhancements](#future-enhancements)
10. [📄 License](#license)
11. [👨‍💻 Contributing](#contributing)

---

## 🌟 Overview

The **Simple Lang Compiler** is designed to illustrate the basic principles of compiler construction. It processes a custom programming language that supports variable declarations, arithmetic operations, conditional statements, and loops. The compiler translates the source code into an intermediate form represented as quadruples, which can then be optimized or executed.

The core components include:
- **Lexical Analysis (Tokenization)**
- **Syntax Analysis (Parsing)**
- **Intermediate Code Generation**
- **Symbol Table and Temporary Variable Management**

---

## ✨ Features

- **Complete Compilation Pipeline**: Tokenization, parsing, and intermediate code generation.
- **Recursive Descent Parser**: Ensures syntactical correctness based on predefined grammar rules.
- **Intermediate Representation**: Generates quadruples as an intermediate form of the source code.
- **Symbol Table**: Manages identifiers (variables and constants) and their types/values.
- **Temporary Variable Table**: Tracks temporary variables generated during code execution.
- **Graphical User Interface (GUI)**: Intuitive interface for users to interact with the compiler.

---

## ⚙️ System Requirements

- **Operating System**: Windows (tested on Windows 10)
- **Development Environment**: Visual Studio (2019 or later)
- **Framework**: .NET Framework 4.7 or higher
- **Memory**: Minimum 4 GB RAM
- **Disk Space**: 50 MB or more for project files and dependencies

---

## 📦 Setup and Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/4riful/custom-compiler.git
   ```

2. **Open the Project in Visual Studio**:
   - Open the `.sln` file (e.g., `compiler202124405005.sln`) in Visual Studio.
   - Ensure that you have the required .NET Framework installed.

3. **Build the Project**:
   - In Visual Studio, build the project to compile the source code.

4. **Run the Application**:
   - You can run the application directly from Visual Studio or by executing the `.exe` file located in the `bin/Debug/` or `bin/Release/` directory.

---

## 💻 Usage

Once the project is built and running, the graphical user interface (GUI) will allow you to input code, tokenize it, parse it, and generate intermediate code.

### Input Code Example

The compiler processes a subset of a programming language. Below is an example of valid input code that the compiler can handle:

```simple-lang
int$f;$f=8;$f=$f;while($f>=$f*4)do$f=$f+6;
if($f<$f*865)thenbegin$f=$f*5;$f=$f+17;end;
elsebegin$f=$f+6;$f=$f+8;end;
```

You can also use other similar structures, for example:

```simple-lang
int$y;$y=94;$y=8;while($y+8>=$y+4)dobegin$y=$y*580;$y=$y+418;end;
if($y*1>=$y)then$y=$y+1;else$y=$y*64;
```

Due to the limitations of the DFA, the language can only accept specific structures as shown in the examples. Input code outside this format will result in an error during tokenization or parsing.

Simply enter this code in the input field, click the **Tokenize** button to break down the code into tokens, and then click **Parse** to validate the syntax and generate intermediate code.

---

## 🛠️ Detailed Architecture

### Lexical Analysis

The **tokenizer** converts the input source code into tokens, which are the smallest meaningful units of the language. It identifies keywords (`int`, `if`, `while`), operators (`+`, `*`, `=`, etc.), and delimiters (`;`, `,`, `()`).

- **Method**: The tokenizer is implemented using a finite state machine (FSM), which scans the input character by character and groups them into tokens.
- **Example Tokens**:
  - `int` → `kw_int`
  - `$f` → `identifier`
  - `=` → `assign`
  - `while` → `kw_while`

### Syntax Analysis

The **parser** is responsible for ensuring the sequence of tokens conforms to the grammar of the language. It uses a recursive descent parsing technique to validate the syntax of the source code.

- **Grammar Rules**: The grammar supports variable declarations, expressions, conditional statements, and loops.
- **Recursive Descent Parsing**: Each non-terminal symbol in the grammar is handled by a corresponding function, which recursively processes the input tokens.

### Intermediate Code Generation

The intermediate code is represented as quadruples, a simplified form of machine instructions. Each quadruple consists of four parts: an operator, two operands, and a result.

- **Example Quadruple**:
  - `($f = $f + 6)` becomes `(+, $f, 6, $f)`

### Symbol and Temporary Tables

- **Symbol Table**: Stores information about variables, their types, and values.
- **Temporary Variable Table**: Manages the temporary variables generated during expression evaluation.

---

## 🎨 Graphical User Interface

The project includes a GUI built using Windows Forms in C#. The interface provides an easy-to-use layout for users:

- **Source Code Input**: A text box to input source code.
- **Tokenization**: A button to tokenize the source code, displaying tokens in a list.
- **Parsing**: A button to analyze the syntax, showing the syntax tree and errors.
- **Intermediate Code Generation**: Displays generated quadruples.
- **Symbol Table and Temporary Variables**: Lists of identifiers and temporary variables are viewable for inspection.
- **Clipboard Support**: Allows users to copy results to the clipboard using `Ctrl+C`.

---

## 📝 Example Output

For the input code:

```simple-lang
int$f;$f=8;$f=$f;while($f>=$f*4)do$f=$f+6;
if($f<$f*865)thenbegin$f=$f*5;$f=$f+17;end;
elsebegin$f=$f+6;$f=$f+8;end;
```

The compiler produces:

### Tokens:
```
[kw_int, int]
[identifier, $f]
[semiColon, ;]
[identifier, $f]
[assign, =]
[integer, 8]
...
```

### Quadruples:
```
Idx  | Op  | Opr1 | Opr2 | Result
0    | =   | 8    | null | $f
1    | =   | $f   | null | $f
2    | *   | $f   | 4    | T0
3    | >=  | $f   | T0   | T1
4    | jnz | T1   | null | 6
5    | j   | null | null | 9
...
```

### Symbol Table:
```
Name   | Type   | Value
$f     | int    | 8
```

### Temporary Variables:
```
Name   | Type   | Value
T0     | int    | $f * 4
T1     | bool   | $f >= T0
```

---

## 📈 Future Enhancements

- **Code Optimization**: Implement optimizations like constant folding, dead code elimination, etc.
- **Support for Functions**: Add function definitions and calls.
- **Advanced Error Handling**: Provide more detailed error messages and debugging information.
- **Control Structures**: Expand the language to support switch statements, function calls, and arrays.
- **Backend Code Generation**: Extend the compiler to generate machine code or LLVM IR.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Contributing

Con

tributions are always welcome! If you find a bug or have a feature request, feel free to create an issue or submit a pull request. Follow these steps to contribute:

1. **Fork the Repository**:
   Click the "Fork" button at the top-right corner of the repository page.

2. **Clone Your Fork**:
   ```bash
   git clone https://github.com/yourusername/custom-compiler.git
   ```

3. **Create a New Branch**:
   ```bash
   git checkout -b feature/YourFeatureName
   ```

4. **Commit Your Changes**:
   ```bash
   git commit -m "Add Your Feature"
   ```

5. **Push to Your Fork**:
   ```bash
   git push origin feature/YourFeatureName
   ```

6. **Open a Pull Request**:
   Navigate to the original repository and open a pull request from your fork.

---

🔗 **Visit the Repository:** [https://github.com/4riful/custom-compiler](https://github.com/4riful/custom-compiler)

Feel free to reach out if you have any questions or need further assistance. Happy compiling! 🎉

--- 
