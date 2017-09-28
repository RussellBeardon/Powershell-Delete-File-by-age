# Created by Russell Beardon - June 2015
#
# Deletes Data from directory of set age. Can be run from a scheduled task. Creates a log of deleted items.
#
# !!!!!!!!!!!!!!!BE VERY CAREFUL WITH THIS SCRIPT - IT WILL DELETE DATA!!!!!!!!!!!!!!!!!!!!!!!!!
#
# PARAMETERS:
#    directory: parent directory of files or folders you wish to delete
#    age: Delete file or folder older than set age
#    filetype: delete only files matching this file type
#    logdir: Directory for log file creation
#    namelike: Name
#    type: (both, file, directory) will only delete files/directories or both
#
#
#
Param(
    [parameter(Mandatory=$true)]
    [string]$directory,
    [parameter(Mandatory=$true)]
    [int]$age,
    [string]$fileType="*",
    [string]$logDir = "c:\scripts\logs\",
    [string]$namelike = "*",
    [string]$type = "both", # both, file, directory
    [string]$delete = "no" # no, yes
)

echo "delete set to: $delete"

# get the current date for log name
$format_date = get-date -Format "yyyyMMdd.HHMMss"

# Set log file
$logfile = "log_deleted.$format_date.txt"
$log = $logDir + $logfile
out-file $log -noclobber

# determine how far back we go based on current date 
$del_date = (get-date).AddDays(-$age)

if($type -eq "both" -or $type -eq "file") {
    # delete the files  (file type matches $file_type, older than $del_date)
    $oldFiles = Get-ChildItem $directory -Recurse | ? { $_.PSIsContainer -eq $false -AND $_.LastWriteTime -lt $del_date -AND $_.name -like $namelike }
}

if($type -eq "both" -or $type -eq "directory") {
    # delete folders (older than $del_date, is a directory, contains no files, contains no directories)
    $oldFolders = Get-ChildItem $directory -Recurse | ? { $_.LastWriteTime -lt $del_date } | ? { $_.PSIsContainer -eq $true } | ? {$_.GetFiles().Count -eq 0 } | ? { $_.GetDirectories().Count -eq 0 }
}

echo "deleting: Files" | out-file $log -append
$oldFiles | out-file $log -append
echo "deleting: Folders" | out-file $log -append
$oldFolders | out-file $log -append

if($delete -eq "yes") {
    $oldFolders | remove-item # Delete Folders
    $oldFiles | remove-item # Delete Files
}
