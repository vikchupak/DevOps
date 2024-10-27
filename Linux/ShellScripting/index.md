# About $PATH env variable

- `$PATH` env variable contains a colon-separated list of directories that the shell searches **for commands that do not contain a slash in their name**.
- **Commands with slashes are interpreted as file names to execute, and the shell attempts to execute the files directly, like `./script.sh`**.

# `which` command

Finds path to binary to be executed based on `$PATH`

Example `which nano` => outputs `/usr/bin/nano`

# Can bash script file be excecuted without extension?

Yes, a Bash script file can be executed without an extension. In Linux and other Unix-based systems, the file extension is not required for the system to recognize a file as executable. The execution of a script is determined by the **shebang** (`#!`) at the top of the file and the executable permission set on the file, not by its extension.

**Execute the Script**:
   You can now run the script by specifying its path. For example, if the script is in the current directory:
   ```bash
   ./my_script.sh
   ```

   If the script is located in a directory that is part of your `$PATH` (like `/usr/local/bin/` or `~/bin/`), you can execute it just by typing the script's name:
   ```bash
   my_script
   ```

   You can run the script as follows. This will ignore **shebang** and use the specified interpreter:
   ```
   bash my_script.sh
   ```
   
# shebang

The shebang tells the operating system which interpreter to use when executing the script.

- `#!/bin/sh`
- `#!/bin/bash`
- `#!/bin/zsh`
- `#!/usr/bin/node`
- `#!/usr/bin/env node` - To execute the node interpreter by looking it up in the system’s PATH environment variable (more flexible way)
   https://stackoverflow.com/questions/10376206/what-is-the-preferred-bash-shebang

script.js file
```node
#!/usr/bin/env node

console.log('This script is executed by node.js');
```

run script.js
```bash
./script.js
```

# Execute a script in docker container

- `docker exec [-it] <container_name> node /path/to/script.js`
- `docker compose exec [-it] <container_name> node /path/to/script.js`
