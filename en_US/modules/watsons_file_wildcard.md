# EMQX & Watsons File Wildcard

## File wildcards
The source file path and target path of files such as POS reports, sales data, and purchase records support the use of wildcards. By using file path wildcards, files can be copied, backed up, and organized more efficiently. Wildcards provide flexibility and automation, reducing manual effort and ensuring accuracy and consistency in file operations. Currently only supports `*` to match files.

## Example

| wildcard | matching result |
| --------------- | --------------------------------- -|
| `D:/file/*` | Files in the file directory under D drive |
| `D:/file/*.*` | Files with suffixes in the file directory under the D drive |
| `D:/file/a*` | files starting with a in the file directory under the D disk |
| `D:/file/*.csv` | Files with the suffix csv in the file directory under the D disk |