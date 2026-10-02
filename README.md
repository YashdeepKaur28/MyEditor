# Online Java Compiler — AJAX-Based Web Compiler ☕

A **web-based Java compiler** built with **Java Servlets, AJAX, and Runtime.exec()**. Users can write Java code in the browser, compile it on the server, and see the compiler output — all without page reloads.



---

## 📸 Preview
<img width="870" height="546" alt="Screenshot 2026-09-03 145446" src="https://github.com/user-attachments/assets/4993a8ed-b42c-4d28-8cb9-c946e922a763" />


---

## 📖 Overview

**Online Java Compiler** is a web application that lets users write and compile Java code directly in the browser. The code is sent to the server via AJAX, written to a temporary file, compiled using the JDK's `javac`, and the compiler output is returned to the browser — no page reload needed.

**Built to practice:**
- **Servlets** — handling POST requests with form data
- **AJAX (XMLHttpRequest)** — sending code and receiving output asynchronously
- **Runtime.exec()** — spawning external processes from Java
- **Process I/O** — reading the error/output streams of `javac`
- **File I/O** — writing user code to `.java` files on the server

---

## ✨ Features

- 📝 **Code editor** in the browser (textarea)
- ⚙️ **Compile button** — sends code to server via AJAX
- 📤 **Live output** — shows compiler errors without reloading
- 📁 **Per-class files** — writes each submission as `<ClassName>.java`
- 🗂️ **Separate output folder** for compiled `.class` files

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | Java (JDK 1.6+ with WebLogic) |
| Web | Servlets, HTML, JavaScript |
| AJAX | XMLHttpRequest |
| Process | `Runtime.exec()` calling `javac` |
| Server | Oracle WebLogic Server 12c |
| Build | Manual `javac` + WAR packaging |

---


## 🔄 How It Works

```
┌──────────────────┐
│  User types code │
│  in browser      │
└────────┬─────────┘
         │ AJAX POST (className + code)
         ▼
┌──────────────────────────────────┐
│  Compile servlet (on server)     │
│  1. Reads className + code       │
│  2. Writes to Files/<Name>.java  │
│  3. Runs javac via Runtime.exec  │
│  4. Captures stderr              │
└────────┬─────────────────────────┘
         │ Output (errors or success)
         ▼
┌──────────────────┐
│  Shown in browser│
│  output textarea │
└──────────────────┘
```

---

## ⚙️ Setup & Deployment

### Prerequisites

- **JDK 1.6+** (WebLogic 12.1.1 bundled JDK works)
- **Oracle WebLogic Server 12.1.1**
- **Notepad + a browser**

### Step 1 — Configure paths

Edit `Compile.java` and update the two paths:

```java
String path = "D:/java/AJAX/OnlineCompilerAJAX/";
String command = "C:\\Oracle\\Middleware\\jdk160_29\\bin\\javac -d "
                + path + "Files\\classes " + path + "Files\\" + filename;
```

Change both to match your local setup.

### Step 2 — Compile the servlet

```cmd
path1.bat
javac -d WebContent\WEB-INF\classes src\Compile.java
```

### Step 3 — Build the WAR

```cmd
cd WebContent
jar -cvf ..\OnlineCompiler.war *
```

### Step 4 — Deploy

1. Start WebLogic
2. Open Admin Console: `http://localhost:7001/console`
3. **Deployments → Install** → select `OnlineCompiler.war`
4. Start the deployment

### Step 5 — Access

```
http://localhost:7001/OnlineCompiler/
```

Type a class name, paste Java code, click **COMPILE**, and see the output.

---

## 🎮 Usage

1. Open the page
2. **Enter Class Name** — must match the `public class` name in your code
3. **Write Java Code** — e.g.:
   ```java
   public class Hello {
       public static void main(String[] args) {
           System.out.println("Hello, world!");
       }
   }
   ```
4. Click **COMPILE**
5. Compiler output appears on the right

If code compiles → "Compiled Successfully"
If errors → they show up in the output box

---

## 🧠 Key Concepts Demonstrated

- **Runtime.exec()** — spawning external processes from Java
- **Process stream handling** — reading `getErrorStream()` to capture `javac` output
- **AJAX without libraries** — plain `XMLHttpRequest` for async calls
- **File I/O** — writing uploaded code to disk before compiling
- **Servlet as process proxy** — the servlet runs `javac` on behalf of the browser
- **Namespace pattern** — one file per submitted class

---

## ⚠️ Known Limitations

- **No code execution** — only compiles (running is a separate concern)
- **No sandboxing** — in production, arbitrary code execution is a **serious security risk**
- **Hardcoded paths** — should read from config
- **No timeout on `javac`** — a slow compile could hang the server
- **No authentication** — anyone can submit code
- **No file cleanup** — old `.java`/`.class` files accumulate

**This project is for learning only.** Do not deploy publicly.

---

## 🚀 Future Enhancements

- [ ] Add **RUN** support (compile + execute with timeout)
- [ ] **Sandbox** the compilation (Docker container per submission)
- [ ] **File cleanup** after N minutes
- [ ] **Syntax highlighting** in the editor (CodeMirror / Ace)
- [ ] **Multiple classes** in one submission
- [ ] **Auth** — only logged-in users can compile
- [ ] **Rate limiting** — prevent abuse
- [ ] **Replace Runtime.exec with ProcessBuilder** (better error handling)
- [ ] **WebSocket** for real-time streaming of output

---

## 👩‍💻 Author

**Yashdeep Kaur**
- 🎓 B.Tech CSE, Punjabi University, Patiala (2026)
- 💼 Java Full Stack Trainee @ CodeSquadz
- 📧 ykdeep2453@gmail.com
- 🔗 [LinkedIn](https://linkedin.com/in/yashdeep-kaur-16aa083b1)
- 🐙 [@YashdeepKaur28](https://github.com/YashdeepKaur28)

---

⭐ If you found this useful, consider giving it a star!
