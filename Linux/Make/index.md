![Screenshot from 2024-07-21 00-11-25](https://github.com/user-attachments/assets/b8bc5544-e2f5-4061-a6c4-09a60ac7b132)

- `make` - GNU make utility
- GNU is a free and open-source operating system. GNU stands for GNU's not Unix, which makes the term a recursive acronym, or an acronym in which one of the letters stands for the acronym itself.

### How is GNU different from Unix?
GNU is different from Unix in several ways. One key difference is that GNU uses the GNU General Public License (GPL), while Unix is licensed under the GNU Lesser General Public License (LGPL). The GPL allows users to copy, modify, and redistribute GNU, while the LGPL allows users to copy and modify Unix, but does not allow them to redistribute it.

### What is Makefile?
The make command invokes the execution of the makefile. It is a special file that contains the shell commands that we create to maintain the project. The makefile contains targets and commands for execution. It is not allowed to create more than one makefile. It is recommended to create a separate directory for it.

https://www.javatpoint.com/linux-make-command

### make explained
- https://www.youtube.com/watch?v=_r7i5X0rXJk
- https://www.youtube.com/watch?v=yWLkyN_Satk&t=573s

### Using make for docker
https://www.youtube.com/watch?v=44EqIY7v5xM

# Makefile stamp functionality

- It was originally created for C/C++.
- **The key point is C/C++ produces NEW files during compilation.**

C++ project example

```
project/
├─ main.cpp
```

### **Manual commands order**

1. Create `main.o` from `main.cpp` with command `g++ -c main.cpp`
2. Create executable `main` with command `g++ main.o -o main`

### **Makefile**

```make
# Target: executable
main: main.o
	g++ main.o -o main

# How to build main.o from main.cpp
main.o: main.cpp
	g++ -c main.cpp
```

### **Timeline Diagram**

#### **Initial build (first run)**

| Time  | File     | Status / Event                                                |
| ----- | -------- | ------------------------------------------------------------- |
| 10:00 | main.cpp | Last edited at timestamp = 10:00                              |
| 10:05 | main.o   | **Does not exist** → Make creates `main.o`, timestamp = 10:05 |
| 10:06 | main     | **Does not exist** → Make creates `main`, timestamp = 10:06   |

### Next run without chages

- `main.cpp`, timestamp = 10:00
- `main.o`, timestamp = 10:05
- `main`, timestamp = 10:06

Make checks: any dependency newer than target?
- 10:00 (main.cpp) < 10:05 (main.o) → main.cpp older than main.o → skip recreating main.o
- 10:05 (main.o) < 10:06 (main) → main.o older than main → skip recreating main

### Next run with main.cpp changes

- `main.cpp`, timestamp = 10:30
- `main.o`, timestamp = 10:05
- `main`, timestamp = 10:06

Make checks: any dependency newer than target?
- 10:30 (main.cpp) < 10:05 (main.o) → main.cpp newer than main.o → recreating main.o, timestamp = 10:35
- 10:35 (main.o) < 10:06 (main) → main.o newer than main → recreating main, timestamp = 10:40

# Example for docker

## Rebuild image only if package.json has changes

```makefile
package-json-stamp: package.json
	@echo "Building image..."
	docker build -t nest-backend-dev -f Dockerfile.dev .
	touch package-json-stamp

docker-build: package-json-stamp
	@echo "Docker image is up-to-date"
```

```bash
make docker-build
```

## Always rebuild image before publish

```makefile
IMAGE_NAME=vikchupak/my-nestjs-app:latest

build:
	docker build -t "${IMAGE_NAME}" .

# Always build image before publish as build is not file
publish: build
	docker push "${IMAGE_NAME}"
```

```bash
make build
# Runs: docker build -t vikchupak/my-nestjs-app:latest .

make publish
# Runs: docker build -t vikchupak/my-nestjs-app:latest .
# Then runs: docker push vikchupak/my-nestjs-app:latest
```
