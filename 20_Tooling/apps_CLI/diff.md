The Linux diff command compares two files (or directories) and shows the differences between them.


Check differences between two files
```sh
# basic usage
# diff <original file> <modified file>
diff file1.txt file2.txt

# The -u argument stands for unified output format.
# Instead of showing only the changed lines, it shows the changed lines along with some surrounding context.
diff -u shared/t3-keybindings.json /root/.t3/userdata/keybindings.json
```
