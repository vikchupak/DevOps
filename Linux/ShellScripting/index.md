# About $PATH env variable

`$PATH` env variable contains a colon-separated list of directories that the shell searches for commands that do not contain a slash in their name **(commands with slashes are interpreted as file names to execute, and the shell attempts to execute the files directly, like `./script.sh`)**.

# `which` command

Finds path to binary to be executed based on `$PATH`

Example `which nano` => outputs `/usr/bin/nano`

# Can bash script file be excecuted without extension?

Yes, a Bash script file can be executed without an extension. In Linux and other Unix-based systems, the file extension is not required for the system to recognize a file as executable. The execution of a script is determined by the **shebang** (`#!`) at the top of the file and the executable permission set on the file, not by its extension.

**Execute the Script**:
   You can now run the script by specifying its path. For example, if the script is in the current directory:
   ```bash
   ./my_script
   ```

   If the script is located in a directory that is part of your `$PATH` (like `/usr/local/bin/` or `~/bin/`), you can execute it just by typing the script's name:
   ```bash
   my_script
   ```
