# Powershell-Delete-File-by-age
Powershell script to delete files older than x days

Deletes Data from directory of set age. Can be run from a scheduled task. Creates a log of deleted items.

!!!!!!!!!!!!!!!BE VERY CAREFUL WITH THIS SCRIPT - IT WILL DELETE DATA!!!!!!!!!!!!!!!!!!!!!!!!!

PARAMETERS:

directory: parent directory of files or folders you wish to delete

age: Delete file or folder older than set age

filetype: delete only files matching this file type

logdir: Directory for log file creation

type: (both, file, directory) will only delete files/directories or both

delete: yes, no (defaults to no)
