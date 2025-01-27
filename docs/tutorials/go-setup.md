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

## **Part 1. Project Setup: Initializing your Repository**
### **Step 1: Create a Local Directory and Initialize Git**

(A) Open your terminal or command prompt.  

(B) Create a new directory for your project.  

``` bash
mkdir first-go-project 
cd first-go-project 
```

(C) Initialize a new Git Repository

``` bash
git init # (1)!

```

1. Initialize a folder as a new, empty git repository.

### **Step 2: Create a remote repository on GitHub**

(1) Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new){:target="_blank"} page.

(2) Fill in the details as follows:

- **Repository Name:** `first-go-project`
- **Description:** "My first Go project"
- **Visibility:** Public

(3) Do not initialize the repository with a README, .gitignore, or license.

(4) Click **Create Repository**.

### **Step 3. Link your Local Repository to GitHub**

(1) Let's create a README file to commit. In your terminal, run:
  ```bash
  echo "# first-go-project" >> README.md
  git add README.md
  git commit -m "First commit with README file"
  ```

(2) Add the GitHub repository as a remote:

   ```bash
   git remote add origin https://github.com/<your-username>/first-go-project.git
   ```

   Replace `<your-username>` with your GitHub username.

(3) Check your default branch name with the subcommand `git branch`. If it's not `main`, rename it to `main` with the following command: `git branch -M main`. Old versions of `git` choose the name `master` for the primary branch, but these days `main` is the standard primary branch name.

  ```bash
  git branch -M main
  ```

(4) Push your local commits to the GitHub repository:

   ```bash
   git push --set-upstream origin main
   ```

!!! info "Understanding the --set-upstream Flag"

    `git push --set-upstream origin main`: This command pushes the main branch to the remote repository origin. The `--set-upstream` flag sets up the main branch to track the remote branch, meaning future pushes and pulls can be done without specifying the branch name and just writing `git push origin` when working on your local `main` branch. This long flag has a corresponding `-u` short flag.

## **Part 2. Setting up your Dev Container**

1. In VS Code, open your folder that includes your project.
2. Install the **Dev Containers** extension for VS Code.
3. Create a `.devcontainer ` directory in the root of your project with the following file inside of this "hidden configuration directory:  

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
  }
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

1. In your main directory, create folder to house your new project, and name it `go-hello-423`  and in it a new file called `main.go`.
2. In your `main.go` file, you can now write your first Go code.

``` Go title="Hello COMP423"
package main

import "fmt" // (1)!

func main(){
    fmt.Println("Hello COMP423!")
}
```

1. **fmt is the standard library for formatting input/output in Golang**

!!! info "What is package main and why are we importing fmt?"
    Golang's design philosophy encourages modularization and seperation into packages. In a way, this is very similar to the concept of classes in Java. This way of importing and creating packages **decouples** code making it easier to **maintain, debug, and reuse code**.

### Step 2: Running the code

Before we start, lets first initialize our go project.

Making sure you are in your `first-go-project` directory, then in your terminal, run the following command.

```bash
go mod init main.go
```

!!! note "what does go mod do?"
    the `go mod init` command is used to initialize a new module in your project. It creates a new `go.mod` file in your current directory. Each Go module is defined by a `go.mod` file that describes the module's properties, including its dependencies on other modules as well as define the module's import path. You can manage your dependencies with other `go mod` commands (e.g., `go mod tidy`, `go get`, etc).


Now that you have initialize your project to use Go modules. It's time to finally run your code! Let's enter the directory containing `main.go` 

```bash
cd go-hello-423
```
Now in your terminal, run the following command to run your program.

```bash
go run main.go
```
You should now see `Hello COMP423!` in your terminal.

!!! question "How does `go run` exactly work?"
    Because **Golang** is a `compiled language`, everytime a program is ran, the program first has to be compliled into machine code (eg. binary). `go run` does both this in succession, both compliling and running after the program is compiled. **The compiled file is not saved** 

Compared to `go run`, `go build` is faster because this command only compiles the program into binary code creating a executable object file and does not run it.

Your current directory should be `first-go-project/go-hello-423`

To see what `go build` do, input this command in your terminal:

```bash
go build main.go

```
In your directory, you should see a `main` file appear. This file contains the binary conversion/equivalent of the code you wrote in your `main.go` file.

In your terminal, run this command to the compliled main.go

```bash
./main # (1)!
```

1. `./` exectutes the program in the currently working directory.

### **Pros and Cons**

The `run` subcommand is very useful in active development, when you want to experiment or test out a new feature. However, this is very slow because you have to recompiled the code everytime you want to run it.  

The `build` subcommand promotes reuseablility, meaning that you can execute the code without having to recompliling it each time, saving time and resources. However the tradeoff, is that the compiled `.exe` file takes up space and it is a hassle having to build and then run it.


