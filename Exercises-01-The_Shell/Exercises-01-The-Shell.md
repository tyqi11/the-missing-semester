# Exercises 01: The Shell 

1. **Create a new directory called `missing` under `/tmp`.**

   ```bash
   # go to the /tmp folder under /var
   cd ../../var/tmp
   
   # make directory
   mkdir missing
   ```

2. **Look up the `touch` program. The `man` program is your friend.**

   ```bash
   man touch
   ```

3. **Use `touch` to create a new file called `semester` in `missing`.**

   ```bash
   touch semester
   ```

4. **Write the following into that file, one line at a time:**     

   ```
   #!/bin/sh
   curl --head --silent https://missing.csail.mit.edu
   ```

   **The first line might be tricky to get working. It’s helpful to know that `#` starts a comment in Bash, and `!` has a special meaning even within double-quoted (`"`) strings. Bash treats single-quoted strings (`'`) differently: they will do the trick in this case. See the Bash [quoting](https://www.gnu.org/software/bash/manual/html_node/Quoting.html) manual page for more information.**

   ```bash
   echo '#!/bin/sh' > semester
   echo 'curl --head --silent https://missing.csail.mit.edu' >> semester
   
   # check the result
   cat semester
   ```

5. **Try to execute the file, i.e. type the path to the script (`./semester`) into your shell and press enter. Understand why it doesn’t work by consulting the output of `ls` (hint: look at the permission bits of the file).**

   ![ex1-permission](images\ex1-5-permission.png)

   It is not executable as there is no `x` but `-` in the corresponding place.

6. **Run the command by explicitly starting the `sh` interpreter, and giving it the file `semester` as the first argument, i.e. `sh semester`. Why does this work, while `./semester` didn’t?**

   Answer: [[Can scripts run even when they are not set as executable?](https://askubuntu.com/questions/25681/can-scripts-run-even-when-they-are-not-set-as-executable)](https://askubuntu.com/questions/25681/can-scripts-run-even-when-they-are-not-set-as-executable)

   In short: when using `bash <script_file_name> `, the user only need read access for the file. But to run by asking the kernel to call bash, the file has to be executable. 

7. **Look up the `chmod` program (e.g. use `man chmod`).**

   ```bash
   man chmod
   ```

8. **Use `chmod` to make it possible to run the command `./semester` rather than having to type `sh semester`. How does your shell know that the file is supposed to be interpreted using `sh`? See this page on the [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) line for more information.**

   ```bash
   # simple version
   chmod +x semester
   
   # -c: report when a change is made
   # u: user, g: group, o: other, a: all
   chmod -c a+x semester
   ```

   ![ex1-8-chmod](\images\ex1-8-chmod.png)

9. **Use `|` and `>` to write the “last modified” date output by `semester` into a file called `last-modified.txt` in your home directory.**

   ```bash
   ./semester | grep -i last-modified > ~/last-modified.txt
   ```

   ![ex1-9-last-modified](images\ex1-9-last-modified.png)

10. **Write a command that reads out your laptop battery’s power level or your desktop machine’s CPU temperature from `/sys`. Note: if you’re a macOS user, your OS doesn’t have sysfs, so you can skip this exercise.**

    ```bash
    cat /sys/class/power_supply/BAT0/capacity
    # 100
    cat /sys/class/power_supply/BAT0/capacity_level
    # Full
    ```

    