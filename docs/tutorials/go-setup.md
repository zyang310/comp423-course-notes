* Primary author: [Zhi Hang Yang](https://github.com/zyang310/){:target="_blank"}
* Reviewer: [Joseph Zheng](https://github.com/joz2005){:target="_blank"}

# Hello, Welcome to my Go tutorial!

## **What you will Learn**

By completing this tutorial, you will learn:

 - Initialize a new project
 - Setting up a dev container
 - Run your first Golang code

## **Prerequisites**

Before we get [into the thick of it](https://www.youtube.com/watch?v=At8v_Yc044Y){:target="_blank"}, make sure you have these set up:

1. **A GitHub account:** If you don't have one yet sign up at the [Hub](https://github.com/){:target="_blank"}.
2. **Git Installed:** Git Good by [installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git){:target="_blank"} if you haven't already.
3. **Visual Studio Code (VS Code):** Download and install this bad-boy [here](https://code.visualstudio.com/){:target="_blank"}.
4. **Docker Installed:** You need this to run the dev container. [Get Docker here](https://www.docker.com/products/docker-desktop/){:target="_blank"}!
5. **Install Go:** You got to [GO](https://go.dev/){:target="_blank"} download the language before using it!

## **Part 1. Project Setup: Initializing your Repository**
### **Step 1: Create a Local Directory and Initialize Git**

(A) Open your terminal or command prompt.  

(B) Create a new directory for your project.  

``` bash
mkdir my-first-go-project 
cd my-first-go-project 
```

(C) Initialize a new Git Repository

``` bash
git init # (1)!

```

1. Initialize a folder as a new, empty git repository.

### **Step 2:**

!!! important
    WIP

## **Part 2. Setting up your Dev Container**

1. In VS Code, open your folder that includes your project.
2. Install the **Dev Containers** extension for VS Code.
3. Create a `.devcontainer ` directory in the root of your project with the following file in side of this "hidden configuration directory:  

``.devcontainer/devcontainer.json``

Now paste this into your `devcontainer.json` file:

``` json title="devcontainer.json"
{ 
  "name": "give a desriptive name",
  "image": "mcr.microsoft.com/devcontainers/go:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["golang.go"]
    }
  },
} 
```

 - `name`: Give a descriptive name to your dev container
 - `image`: The Docker image to use, in this case, the latest version of a Python environment.
 - `customizations`: Adds useful configurations to VS Code, Adding extensions here ensures other developers on your project have them installed in their dev containers automatically.

Reopen the project in the container by pressing `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac), typing `"Dev Containers: Reopen in Container"`, and selecting the option. This may take a few minutes while the image is downloaded and the requirements are installed.

Once your dev container setup completes, close the current terminal tab (trash can), open a new terminal pane within VSCode, and try running `go version`!

## **Part 3. Hello World!**

### **Step 1: Writing the code**

Now everything is set up, we can bring it all to life!

1. In your main directory, create folder to house your new project, maybe name it `first-go`, and in it a new file called `main.go`.
2. In your `main.go` file, you can now write your first Go code.

``` Go title="Hello World!"
package main

import "fmt" // (1)!

func main(){
    fmt.Println("Hello World!")
}
```

1. **fmt is the standard library for formatting input/output in Golang**

!!! info "What is package main and why are we importing fmt?"
    Golang's design philosophy encourages modularization and seperation into packages. In a way, this is very similar to the concept of classes in Java. This way of importing and creating packages **decouples** code making it easier to **maintain, debug, and reuse code**.

### Step 2: Running the code

Because programs in Go are packages, we will first have to turn `main.go` into a package!

Making sure you are in your `first-go` folder, then in your terminal, run the following command.

```bash
go mod init main.go
```
Now that you have turned your `main.go` into a package, you can now run it! Again, make sure you are in your `first-go` folder. Now in your terminal, run the following command to run your program.

```bash
go run main.go
```
You should now see `Hello World!` in your terminal.

!!! question "How does `go run` exactly work?"
    Because **Golang** is a `compiled language`, everytime a program is ran, the program first has to be compliled into machine code (eg. binary). `go run` does both this in succession, both compliling and running after the program is compiled. **The compiled file is not saved** 

Compared to `go run`, `go build` is faster because this command only compiles the program into binary code and does not run it creating a `.exe` file.

To test it out, go to your terminal (make sure that you are in the `first-go` directory) and input this command:

```bash
go build main.go
```
In your directory, you should see a `main.exe` file appear. This `.exe` file contains the binary conversion/equivalent of the code you wrote in your `main.exe` directory.

In your terminal, now run this command to the compliled main.exe.

```bash
./mian.exe # (1)!
```

1. `./` exectutes the program in the currently working directory.

### **Pros and Cons**

The `run` subcommand is very useful in active development, when you want to experiment or test out a new feature. However, this is very slow because you have to recompiled the code everytime you want to run it.  

The `build` subcommand promotes reuseablility, meaning that you can execute the code without having to recompliling it each time, saving time and resources. However the tradeoff, is that the compiled `.exe` file takes up space and it is a hassle having to build and then run it.


