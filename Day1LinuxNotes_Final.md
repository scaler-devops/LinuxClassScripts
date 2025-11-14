Day1 Linux Notes





Linux Foundations — Day 1





Opening Story: Welcome to Your First Linux Server

You just joined a cloud company as a Cloud Engineer.
Your manager says:
“Hey, can you check the logs on the web server and fix permissions if needed?”

You open your laptop… no GUI, no icons, just a blinking cursor — a Linux terminal.

And that’s the moment every engineer faces:

Do you control the terminal, or does the terminal control you?

Today, you’ll learn to navigate, manage, and search in Linux like a pro — using just the keyboard.
Let’s begin your command-line journey!

Section 1 — Login to Linux & Knowing Where You Are



You want to know which user you are logged in as, do you know how to figure that out? Can you create a new user and try to change the password for the sudo user and the new user created?

“I want to check which user is currently logged in — how do I do that?”

- whoami	

“I want to switch to the root user temporarily — which command should I use?”

- sudo su	

“How do I switch to another user’s account with their full environment?”

- su - user	

“How do I change my current user’s password?”

- passwd	

“I’m lost. How can I check which directory I’m currently in?”

- pwd	

“How do I see all the files and folders in my current directory?”

- ls	

“How do I list files with details like permissions, size, and timestamp?”

- ls -l	

“Some files are hidden. How do I list every file, including hidden ones?”

- ls -a	

Explanation:

whoami → tells you which user is logged in

sudo su → execute a command as the superuser (root) 

su - user → change user

passwd → change password of the current user

pwd → shows your current working directory

ls → lists all files in that directory

ls -l → detailed list (permissions, size, owner)

ls -a → shows hidden files too (those starting with .)





What is root?

In Linux, root is the default administrative user. It is the most powerful account on the system, often called the super-user.

Maximum Privileges: The root user has complete, unrestricted power over the system. It can access any file, execute

any command, and modify any part of the operating system, including the kernel.

Unique Identifier: The root user always has a User ID (UID) of 0.

Security Risk: Because of its power, logging in as root for daily tasks is generally discouraged.

Users should instead use the sudo (Substitute User Do) command to temporarily execute commands with root privileges

when necessary.



Pro Tip:



If your screen ever feels cluttered, clear it with:



clear



Quick Quiz 1



Q1. If pwd shows /home/ec2-user/docs, what will cd .. do?
Answer: Move you one level up → /home/ec2-user.



Q2. What does ls -a reveal that ls hides?
Answer: Hidden files (those starting with a .).



Section 2 — Moving Around and Managing Files



Imagine your Linux system is like a big apartment building — everything inside is organized so you can find anything quickly.



Directories = Rooms



Directories (also called folders) are like rooms in this huge building.



Each room can store different things (files) and has a name and a purpose.



Files = Items inside those rooms



Root Directory / = The Building Entrance

Every Linux system begins at / — the entrance to the building.
From there, you can walk into any room.



Home Directory ~ = Your Personal Room

Your home directory (/home/ec2-user or /home/user) is your private room.
Your files, your documents, your projects live here.



Moving Around

cd is how you walk into a room

ls is how you look around the room

pwd is how you check which room you're currently in





Can you try to create a new file?



Commands:



cd /

cd /home

cd ~

mkdir projects

cd projects

touch file1.txt file2.txt



Pro Tip:


touch "$(date +%F).log" creates a log file with today’s date.





Linux File System [give a brief introduction and provide complete file system structure with explanation in lecture notes]



Introduction to Linux File System



The Linux File System (FS) is a highly organized, hierarchical structure. Unlike Windows, which uses drive letters (C:, D:), Linux follows a single inverted tree structure where all files and directories start from one directory called the root directory (/).

FileSystem Structure and Description

All directories and files branch out from the main root directory (/). Below are some of the most important top-level directories:







File System Navigation Commands







Linux File or Directory Properties Absolute and Relative Paths

Paths are how you specify the location of a file or directory.



Absolute Path (Full Path):

 Starts from the root directory (/).

 It defines the complete route to a file, regardless of your current location.

 Example: /home/user/documents/report.pdf



 Relative Path:

 Starts from your current working directory.

 It defines the route relative to where you currently are.

 Special notations:

 . (single dot) refers to the current directory.

 .. (double dot) refers to the parent directory (one level up).

 Example: If you are in /home/user/, the relative path to report.pdf is documents/report.pdf.





Quick Quiz 2



Q1. What’s the difference between / and ~?
Answer: / is system root, ~ is your personal root(home directory).



Q2. If you run touch demo.txt twice, what changes?
Answer: The file’s timestamp, not content.







Section 3 — Copying, Moving, Deleting & Editing Files

Now that you understand your Linux system as a big house with rooms (directories) and items (files), let’s talk about how you manage those items.

Imagine you’re inside your room…
And you have books, notes, tools, and documents lying around.
What can you do with them? 

Copy (cp) — Making a Duplicate



cp file1.txt /home/ec2-user/backup/

Copying is like photocopying a document.
You keep the original where it is, and place the duplicate in another room.





Move (mv) — Shifting or Renaming



mv file2.txt file2_renamed.txt

Moving is like picking up a book and putting it in another shelf.
If you stay in the same room but change the name → that’s renaming, still the same command.





Delete (rm) — Throwing Something Away



rm file2_renamed.txt

Deleting is like putting something in the trash — once thrown, it’s gone.
(And Linux doesn't have a recycle bin, so be careful!)





Edit (vi) — Writing Inside a File



vi notes.txt

Editing is like opening a notebook and writing inside it.
vi is your pen — powerful, always available, and works even without a mouse.





Quick Guide:



Press i → start typing

Press Esc → exit typing mode

Type :wq → save and quit

Type :q! → quit without saving



Pro Tip:


Use cp -i and mv -i to get a warning before overwriting files.



To quickly view a file, use: cat notes.txt



Quick Quiz 3



Q1. Which flag helps you avoid accidental overwrite — -v or -i ?
Answer: -i (interactive prompt).



Q2. If you use mv file.txt /tmp/ , what happens?
Answer: The file moves to /tmp (Linux temp directory).



Q3. In vi, how do you exit without saving?
Answer: :q!



Q4. Which key starts insert mode?
Answer: i







Section 4 — Finding Files



Using the same analogy that our Linux system is a big apartment building with thousands of rooms.
You want to find a specific item, like a book or a tool, hidden somewhere in those rooms.

That job is done by find — your personal detective.

find Command:



find <path> -name <filename>



Example Command:



find /home -type f -name "*.txt"



Explanation:



find → searches the live filesystem

-type f → files only

-name "*.txt" → pattern match



Pro Tip:


To find recently changed files:



find /home -type f -mtime -1



(-mtime -1 = modified in the last 24 hours)



Quick Quiz 5



Q1. Why might find /var/log show “Permission denied”?
Answer: You need sudo for protected directories.



Q2. How to search only .sh files?


Answer: find /home -type f -name "*.sh"







Section 5 — Locate Command (Fast Search)



If find is a detective searching every room in real time…
then locate is the detective who already has a digital map of where everything was yesterday.

He doesn’t walk around — he checks his database instantly.

locate Command:



sudo yum install mlocate -y      # (or apt install on Ubuntu)



sudo updatedb



locate script.sh   # locates script.sh



locate -r '\.sh$\|\.bash$'   # locates anything ending with .sh or .bash





Explanation:



locate is faster than find because it searches a prebuilt database



updatedb rebuilds that database



Use regex (-r) for pattern matching





Pro Tip:


If you add new files and locate doesn’t find them → run sudo updatedb again.





Quick Quiz 6



Q1. Why is locate faster than find?
Answer: It searches a prebuilt database, not the live disk.



Q2. What command updates that database?
Answer: sudo updatedb









Section 6 — Packaging Logs Example

Now imagine your /var/log directory is a room full of old receipts and paperwork.
You want to:

Gather all old log files

Pack them into a single compressed box

Label it

That’s exactly what these commands do.





Step 1 — Finding Logs & Packing Them (Pipeline Command)



Command:



sudo find /var/log -type f -name "*.log" -mtime +0 -print | sudo tar -cvzf oldlogs.tar.gz -T –





Command Breakdown:



(A) find  

Execution flow:

Go to /var/log (/var/log)

Collect only files  (- type f)

That end with .log (-name "*.log")

That were modified more than 0 days ago (-mtime +0)

Print their full paths (-print)

It gathers a list of old logs like:

/var/log/secure.log

/var/log/messages.log



(B) The Pipeline | — Passing the list

The collected list is passed through a pipeline, like sending items on a conveyor belt to another worker.



(C) tar — The packer

The tar command is your worker who:

-c → creates a new box

-v → shows what he’s packing

-z → compresses the box (zip)

-f oldlogs.tar.gz → labels the box

-T - → takes the list directly from the conveyor belt

So tar receives…

/var/log/messages.log

/var/log/secure.log

…and packs them into oldlogs.tar.gz.





Step 2 — Checking the Box



Command:



ls -lh oldlogs.tar.gz

You look at the box’s label to check:

Size

Owner

Permissions

Timestamp

With -h, the size is shown in human readable units (KB, MB).

Purpose: verify archive was created and check its size. 



Example output: -rw-r--r-- 1 root root 12K Nov 12 18:44 oldlogs.tar.gz





Step 3 — Peeking Inside Without Opening



Command:



tar -tzf oldlogs.tar.gz

Without unpacking the whole box, you peek inside to see which files were stored.

Breakdown:



tar - Archive viewer

-t - List the contents of the archive.

-z - Archive is gzip-compressed.

-f oldlogs.tar.gz - Read the file named oldlogs.tar.gz.



Purpose : To verify which .log files were included inside the archive — without extracting it.



Example output:



var/log/secure.log

var/log/messages.log

var/log/cron.log





Quick Quiz 7



Q1. What does -cvzf stand for in tar?
Answer: create, verbose, zip, file.



Q2. What does tar -tzf do?
Answer: Lists files inside the compressed archive.





Optional Challenge



Mini Project:

Create a folder named day1-practice.

Add 3 text files inside it.

Copy them to a backup folder.

Archive all .txt files using tar.

Find the archive with locate.



Share your final tar path as proof you completed the challenge











Hands on  tutorial









touch and mkdir



a.



Step 1: Basic Setup

Open your terminal and make sure you are in a test directory to safely experiment:

mkdir ~/touch-demo cd ~/touch-demo





Step 2: Creating an Empty File

Let’s create a new empty file called file1.txt. touch file1.txt

Now verify that it’s created:

ls -l

Output (example):

-rw-r--r-- 1 vilas vilas 0 Nov 11 13:10 file1.txt

The file size is 0, and it has the current timestamp.





Step 3: Creating Multiple Files at Once

You can create multiple files in one command: touch file2.txt file3.txt file4.txt Check:

ls -l

Output:

-rw-r--r-- 1 vilas vilas 0 Nov 11 13:12 file2.txt

-rw-r--r-- 1 vilas vilas 0 Nov 11 13:12 file3.txt

-rw-r--r-- 1 vilas vilas 0 Nov 11 13:12 file4.txt





Step 4: Updating File Modification Time



If a file already exists, running touch updates its modification time (mtime) and access time (atime).

ls -l file1.txt sleep 5

touch file1.txt ls -l file1.txt

Notice the time difference — the timestamp is updated, but the content is not changed.





Include in Notes

Step 5: Setting a Custom Timestamp

You can manually set the modification date/time.



Format:

touch -t [[CC]YY]MMDDhhmm[.ss] filename

Example:

touch -t 202410151030.00 file2.txt ls -l file2.txt

This sets the timestamp to Oct 15, 2024, 10:30:00.





Step C: Match Timestamp of Another File

You can copy timestamps from one file to another using the -r option:

touch -r file2.txt file3.txt

Now compare:

ls -l file2.txt file3.txt

Both should have the same timestamp.





Step 7: Prevent File Creation (Update Only if Exists)

By default, touch creates a new file if it doesn’t exist. To update only existing files, use -c (or --no-create):

touch -c file10.txt

If file10.txt doesn’t exist, no new file will be created.





Step 8: Create Files Inside Nonexistent Directories

If you try this:

touch newdir/file.txt

You’ll get:

touch: cannot touch 'newdir/file.txt': No such file or directory

Solution: use mkdir -p to create the directory first:

mkdir -p newdir

touch newdir/file.txt





Step 9: Verify Changes Using stat

The stat command gives detailed timestamp information:

stat file1.txt

Output:

Access: 2025-11-11 13:20:35.000000000 +0530

Modify: 2025-11-11 13:20:35.000000000 +0530

Change: 2025-11-11 13:20:35.000000000 +0530





Step 10: Practical Use Cases

Use Case	Example

Create placeholder log files	touch /var/log/app.log

Reset timestamps for build systems	touch *.c before compilation Trigger automation scripts watching file modification touch /tmp/trigger.file

Sync timestamps for backup comparison	touch -r original.txt backup.txt





Step 11: Combine touch with Other Commands

Example 1: Create daily log files automatically

touch "$(date +'%Y-%m-%d').log"

Creates:

2025-11-11.log



Example 2: Create 5 numbered files in a loop for i in {1..5}; do touch file_$i.txt; done Result:

file_1.txt file_2.txt file_3.txt file_4.txt file_5.txt





Cleanup

When done, remove the test directory:

cd ..

rm -rf ~/touch-demo





Summary

Option	Meaning	Example

touch file Create or update file	touch file.txt

-c	Don’t create new files	touch -c file.txt

-r file	Use another file’s timestamp touch -r old.txt new.txt

-t	Specify timestamp	touch -t 202501011230.00 file.txt

--date	Use human-readable date	touch --date="2 days ago" file.txt

cp

a.

What is the cp Command?

cp (short for copy) is a Linux command used to copy files and directories from one location to another.





Step 1: Set Up a Practice Environment

Let’s create a test directory to work in:

mkdir ~/cp-demo cd ~/cp-demo

Then, create a few sample files:

echo "This is file1" > file1.txt echo "This is file2" > file2.txt mkdir folderA

echo "Inside folderA" > folderA/note.txt ls -R





Step 2: Basic File Copy

To copy one file to another file:

cp file1.txt file1_copy.txt

Check:

ls

Output:

file1.txt file1_copy.txt file2.txt folderA/

You now have a copy of file1.txt named file1_copy.txt.





Step 3: Copy File Into a Directory

Let’s copy file2.txt into folderA. cp file2.txt folderA/

Check the contents:

ls folderA

Output:

note.txt file2.txt

The file was copied inside the directory.





Step 4: Copy and Rename at the Same Time

You can also copy and rename a file in one go:

cp file1.txt folderA/file1_renamed.txt

Now check:

ls folderA

Output:

file1_renamed.txt file2.txt note.txt





Step 5: Copy an Entire Directory

To copy directories, you must use the -r (recursive) flag:

cp -r folderA folderB

Check the result:

ls -R

You’ll see:

folderA:

file1_renamed.txt file2.txt note.txt



folderB:

file1_renamed.txt file2.txt note.txt

All files and subdirectories were copied recursively.





Step 6: Avoid Overwriting Files (-i option)

By default, cp overwrites existing files without asking. To make it prompt before overwriting, use -i (interactive):

cp -i file1.txt file1_copy.txt

Output:

cp: overwrite 'file1_copy.txt'?

Type n (no) or y (yes).





Step 7: Preserve File Attributes (-p option)

To preserve timestamps, ownership, and permissions, use -p:

cp -p file1.txt file1_backup.txt

Compare:

ls -l file1.txt file1_backup.txt

Both files have the same modification time and permissions.





Step 8: Combine Options

You can combine options to copy a directory while preserving attributes and prompting before overwrite:

cp -rip folderA folderC

Breakdown:

 -r: recursive

 -i: interactive (ask before overwrite)

 -p: preserve metadata





Step 9: Copy with Verbose Output (-v)

Want to see what’s happening? cp -rv folderA folderD Output:

'folderA' -> 'folderD' 'folderA/note.txt' -> 'folderD/note.txt'

'folderA/file2.txt' -> 'folderD/file2.txt' 'folderA/file1_renamed.txt' -> 'folderD/file1_renamed.txt'

Great for debugging or large copies.





Step 10: Copy Only If Newer (-u)

If you want to copy a file only if the source is newer than the destination, use -u: cp -u file1.txt folderA/file1_renamed.txt

This saves time during backups or syncing.





Step 11: Copy Files Using Wildcards

You can copy multiple files using wildcards like *. mkdir folderE

cp *.txt folderE/

Check:

ls folderE

All .txt files in the current directory are copied into folderE.





Step 12: Copy Hidden Files (Starting with .)

By default, cp skips hidden files (.bashrc, .config, etc.). To include them, use .* or explicitly specify:

mkdir hidden touch .hiddenfile cp -r .* hidden/

This copies hidden files and directories too.





Step 13: Copy Files with Different Owners (Root Example)

When using sudo, file ownership may change. To retain the original owner and permissions (useful for backups):

sudo cp -a /etc/ssh /backup/etc_ssh

Option -a = “archive mode”

Equivalent to -dr --preserve=all (preserves everything).





Step 14: Verify Copy Operation

Use diff or cmp to ensure copied files are identical:

diff file1.txt file1_copy.txt

If no output → files are identical.





Step 15: Cleanup

When done:

cd ..

rm -rf ~/cp-demo





Summary Table

Option	Meaning	Example



cp source dest


Copy a file	cp a.txt b.txt







Archive mode (recursive + preserve all)


cp -a folderA folderB



--parents	Preserve directory structure	cp --parents dir/sub/file.txt

/backup/

-n	Do not overwrite existing files	cp -n a.txt b.txt





Bonus: Real-World Use Cases

Scenario	Command

Backup configuration files	cp -p /etc/ssh/sshd_config ~/backup/ Copy project files with structure	cp -a ~/project ~/project_backup Copy only updated logs	cp -u /var/log/*.log /backup/logs/ Duplicate a directory with feedback cp -rv src_folder dest_folder

mv

a.

What Is the mv Command?

mv stands for move, and it is used to:

Move files/directories from one location to another, or

Rename files/directories.



 Step 1: Setup for Practice



Let’s create a safe workspace:

mkdir ~/mv-demo cd ~/mv-demo

Create some sample files and directories:

echo "This is file1" > file1.txt echo "This is file2" > file2.txt mkdir folderA

echo "Note inside folderA" > folderA/note.txt ls -R





Step 2: Move a File to Another Directory

Basic syntax:

mv source destination



Example:

mv file1.txt folderA/

Check:

ls folderA

Output:

note.txt file1.txt

file1.txt has been moved into folderA/.





Step 3: Move and Rename a File in One Step

You can also rename a file using mv.

mv file2.txt file2_renamed.txt

Check:

ls

Output:

file2_renamed.txt folderA/ file2.txt is now file2_renamed.txt.





Step 4: Move Multiple Files into a Directory

If you want to move several files at once:

mkdir folderB

mv file2_renamed.txt folderA/note.txt folderB/

Now check:

ls folderB

Output:

file2_renamed.txt note.txt

Both files were moved into folderB/.





Step 5: Avoid Overwriting Files (-i option)

By default, mv overwrites files silently.

Use -i (interactive) to ask before overwriting. mv -i folderA/file1.txt folderB/ Output:

mv: overwrite 'folderB/file1.txt'?

Type n (no) or y (yes).

Safe for critical files.





Step 6: Never Overwrite Existing Files (-n option)

If you don’t even want a prompt — just skip overwriting existing files:

mv -n folderA/file1.txt folderB/

If folderB/file1.txt exists, it will not be replaced.





Step 7: Get Verbose Output (-v option)

To see what’s happening:

mv -v folderB/file2_renamed.txt folderA/

Output:

renamed 'folderB/file2_renamed.txt' -> 'folderA/file2_renamed.txt'

-v is great for debugging or scripts.





Step 8: Move an Entire Directory

To move a directory and its contents:

mv folderA folderC

Now check:

ls -R

Output:

folderB/ folderC/

Entire folderA (including its contents) has been moved and renamed to folderC.





Step 9: Move with Absolute and Relative Paths

Example 1: Using relative paths

mv folderC/file2_renamed.txt folderB/

Example 2: Using absolute paths

mv ~/mv-demo/folderB/file2_renamed.txt ~/mv-demo/

Both methods work the same — just different path styles.





Step 10: Move Files Matching a Pattern

Example: Move all .txt files into a folder

mkdir text_files

mv *.txt text_files/

Check:



ls text_files

All .txt files were moved together.





Step 11: Rename a Directory

Rename folderB → backup mv folderB backup Check:

ls

Output:

backup/ folderC/ text_files/ mv can rename directories too.





Step 12: Move Hidden Files (starting with .)

Hidden files (like .bashrc) can also be moved.

touch .hiddenfile mkdir hidden_backup

mv .hiddenfile hidden_backup/

Check:

ls -a hidden_backup

The hidden file was moved successfully.





Step 13: Move and Backup Automatically (--backup)

If you want to keep old files instead of overwriting them, use:

mv --backup file.txt folder/

If a file with the same name exists, it becomes:

file.txt~

Useful for safe overwriting in scripts.





Step 14: Combine Options

Combine multiple flags for safety and visibility: mv -iv backup/file1.txt folderC/ This means:

 -i → ask before overwrite

 -v → show what’s happening





Step 15: Move Files Across Drives or Mounts

When you move files within the same filesystem, mv just updates metadata (very fast). But if you move across filesystems, mv actually copies then deletes the source file.

You can verify using:

df -h

If the source and destination are on different devices, it’ll copy + delete.





Step 16: Cleanup

When done:

cd ..

rm -rf ~/mv-demo





Summary Table

Option	Description	Example

mv src dest Move or rename	mv file1.txt folderA/

-i	Ask before overwrite	mv -i a.txt b.txt

-n	Never overwrite	mv -n a.txt b.txt

-v	Verbose output	mv -v a.txt folder/

--backup	Keep backup of overwritten files mv --backup a.txt folder/

-u	Move only if newer	mv -u a.txt folder/





Real-World Use Cases

Scenario	Command

Rename file safely	mv -i report.txt report_final.txt

Organize log files	mv *.log /var/logs/archive/ Move configuration backups mv -v /etc/*.conf ~/backup/etc/ Rename a folder	mv project project_backup

Move all CSVs to data folder mv *.csv ~/data/

Auto-backup overwrites	mv --backup important.txt /data/





Pro Tip

mv + find = powerful automation. Example:

find . -name "*.log" -exec mv {} /backup/logs/ \;

Moves all .log files from the current directory (and subdirectories) into /backup/logs/.

vi

a.

What is vi?

vi = Visual Editor, one of the oldest and fastest text editors in Unix/Linux.



Its enhanced version, vim (Vi IMproved), is most commonly used today — but everything here works for both.

Tip: If you type vi and your system opens vim, that’s normal — most systems link vi → vim.





Step 1: Open and Exit vi

Create or open a file:

vi testfile.txt

This opens the editor in Normal mode. If the file doesn’t exist, it’ll create one.

Exit Commands (very important!)

Press Esc first (to enter Normal mode), then type one of the following:



Command Action

:w	Save (Write) changes

:q	Quit (if no changes)

:wq or ZZ Save and quit

:q!	Quit without saving

You’ll use :wq most often — it’s your “Save & Exit” combo.





Step 2: Understanding the Three Modes of vi

Mode	Purpose	How to Enter Normal mode	Navigation, editing commands	Press Esc Insert mode	Typing text	Press i, a, or o

Command mode File operations (:w, :q, /search, etc.) Press : from Normal mode Let’s practice.



Step 3: Insert Text

Open your file:

vi notes.txt

Press:

i

→ You are now in Insert mode (you’ll see -- INSERT -- at bottom). Type some text:

This is my first line in vi editor. Learning vi is fun!

Now press:

Esc



→ You’re back to Normal mode.





Step 4: Save and Quit

In Normal mode, type:

:wq

File saved and editor closed.





Step 5: Move Around (Navigation)

Reopen your file:

vi notes.txt

In Normal mode, use these keys:



Key Action

h  Left

l  Right

Down

Up

0  Start of line

$  End of line

w  Jump to next word

b  Jump back one word

G  Go to end of file

gg Go to start of file

:n Go to line n (e.g., :10)

Try moving around — you’ll feel the control.





Step 6: Delete Text

In Normal mode, use:



Command Action

x	Delete one character

dd	Delete entire line

2dd	Delete 2 lines

d$	Delete from cursor to end of line

d0	Delete from cursor to start of line





Step 7: Copy, Paste, and Undo

Command Action

yy	Copy (yank) a line

2yy	Copy 2 lines

p	Paste below the current line

P	Paste above the current line

u	Undo last change

Ctrl + r Redo undone change



Try this:

Move to a line → yy

Move elsewhere → p

Then → u to undo, Ctrl+r to redo.





Step 8: Inserting New Lines

Command Action

Open a new line below and enter Insert mode O   Open a new line above and enter Insert mode A   Move to end of line and enter Insert mode

I  Move to start of line and enter Insert mode Practice:

​

This line is added below. Esc





Step 9: Search and Replace

Search for text



Press /, then type your search term:

/Learning

 Press n to jump to next match

 Press N to jump to previous match





Replace text

Command syntax:

:%s/old/new/g

Example:

:%s/vi/vim/g

Replaces all “vi” with “vim” in the file.

Without %, it replaces only in the current line.

Add c to confirm each change → :%s/vi/vim/gc





Step 10: Cut and Move Lines

To cut and move, combine delete (d) and paste (p): Example:

dd j p



→ Cuts the current line and pastes it below the next one.





Step 11: Case Conversion

Command	Action

~	Toggle case of a character

g~~	Toggle case of current line

gU + motion Uppercase motion (e.g., gUw = uppercase word)

gu + motion Lowercase motion





Step 12: Visual Mode (Block Operations)

Press:

v

→ Start Visual mode (character-wise)

Then move cursor with arrows or hjkl, and:  Press d → delete selection

 Press y → copy selection  Press p → paste selection

Block mode (rectangular selection):

Ctrl + v





Step 13: Working with Multiple Files

Open multiple files:

vi file1.txt file2.txt

Switch between files:



Command	Action

:n	Next file

:N	Previous file

:e anotherfile.txt Open another file





Step 14: Split Windows (Vim only)

Vertical split:

:vs file2.txt

Horizontal split:

:sp file3.txt

Switch between splits:

Ctrl + w, then arrow key





Step 15: Exit Without Saving (Safety Check)

If you make mistakes:

Esc

:q!

This closes without writing changes.





Step 16: Practice Exercises

Try this sequence to master the flow:

Open vi practice.txt

Type 3 lines of text

Copy line 1 (yy)

Paste below (p)

Delete line 2 (dd)

Undo (u)

Search for a word (/word)

Replace it with another (:%s/old/new/g)

Save and quit (:wq)





Step 17: Useful Vim Configs (Optional)

You can customize Vim by editing:

vi ~/.vimrc

Example configuration:

set number

set autoindent set tabstop=4 set expandtab syntax on

set background=dark

This gives line numbers, syntax highlighting, and better indentation.





Summary

Task	Command

Open file	vi filename

Enter insert mode i Exit insert mode	Esc Save	:w

Quit	:q

Save & Quit	:wq

Quit without saving :q!



Delete line	dd

Copy line	yy

Paste line	p

Undo / Redo	u / Ctrl+r

Search	/text

Replace	:%s/old/new/g

Show line numbers :set number





Step 18: Real-World DevOps Use Cases

Use Case	Command

Edit config file	sudo vi /etc/ssh/sshd_config

Modify a Kubernetes YAML	vi deployment.yaml Quick search + replace in logs :%s/error/warning/g Debug script	vi start.sh

Adjust permissions in cron	crontab -e (uses vi by default)







5. find

a.

Step 1: Setup a Practice Area

Let’s first create a directory to safely experiment.



mkdir ~/find-demo cd ~/find-demo

Create some files and directories:



mkdir dir1 dir2 dir3

touch file1.txt file2.log file3.sh echo "hello" > dir1/a.txt

echo "data" > dir1/b.log echo "script" > dir2/run.sh mkdir dir3/subdir

touch dir3/subdir/note.txt

Now verify:



tree ~/find-demo

(if tree is not installed, just use ls -R)





Step 2: Basic Usage — Find by Name

Syntax:

find [path] [criteria]



Example 1: Find all .txt files

find . -name "*.txt"

Output:



./file1.txt

./dir1/a.txt

./dir3/subdir/note.txt

- -name matches the filename (case-sensitive).





- Step 3: Case-Insensitive Search

find . -iname "*.TXT"

- -iname ignores case, matching .txt, .TXT, etc.





Step 4: Find by File Type

Option	Meaning

-type f Regular file

-type d Directory

-type l Symbolic link



Example:

Find only directories:



find . -type d

Find only files:

find . -type f





Step 5: Find by File Size

Option Example	Meaning

+100k find . -size +100k Files > 100 KB

-10M find . -size -10M Files < 10 MB

1G	find . -size 1G	Files exactly 1 GB



Example:

find . -size -1k



- Lists files smaller than 1 KB.





Step 6: Find by Modification Time

Option	Meaning

-mtime n Modified exactly n days ago

-mtime -n Modified less than n days ago

-mtime +n Modified more than n days ago



Example:

find . -mtime -1

- Files modified in the last 24 hours. To check access time:

find . -atime -1

To check change time (metadata):

find . -ctime -1





Step 7: Find by Owner or Group

Example:

Find files owned by your username:



find . -user $USER

Find files owned by root:



sudo find /etc -user root

Find by group:



find /var/log -group syslog





Step 8: Find by Permissions

Example:

Find world-writable files:

find . -perm 777



Find files with executable permission for the owner:



find . -perm -u=x

Find files where others have write access:



find . -perm -o=w





Step 9: Combine Multiple Conditions

You can use logical operators:

 -and or implicit space (default)

 -or

 ! (NOT)

Example:

Find .txt and .log files:

find . \( -name "*.txt" -or -name "*.log" \)

Find files NOT ending with .sh:

find . ! -name "*.sh"





Step 10: Execute Actions on Found Files

Use -exec to run a command on each result.

Example 1: Show details (ls -l)

find . -type f -name "*.txt" -exec ls -l {} \;

Each {} represents the file name.

\; ends the -exec command.





Example 2: Delete all .log files

Use carefully!

find . -type f -name "*.log" -exec rm -v {} \;

Output:

removed './dir1/b.log' removed './file2.log'





Example 3: Replace with xargs (faster)

find . -name "*.txt" | xargs cat

- Displays all .txt files’ content together.





Step 11: Find Empty Files or Directories

Find empty files:



find . -type f -empty

Find empty directories:

find . -type d -empty

You can remove empty directories:

find . -type d -empty -delete





Step 12: Limit Search Depth

Option	Description

-maxdepth n Search up to n levels down

-mindepth n Skip the first n levels Example:

find . -maxdepth 1 -type f

- Only finds files in the current directory (not subdirectories).





- Step 13: Find Newer or Older Files

Compare timestamps between files:

touch ref.txt

find . -newer ref.txt

- Lists files modified after ref.txt.





Step 14: Find and Archive or Copy

Example: Copy all .sh files to another folder



mkdir ~/backup

find . -type f -name "*.sh" -exec cp {} ~/backup/ \;

Example: Archive (compress) all .txt files

find . -name "*.txt" | tar -cvzf txt_files.tar.gz -T -





- Step 15: Find Large Files (Sysadmin Example)

Find all files > 500MB in /var:

sudo find /var -type f -size +500M -exec ls -lh {} \;

- Useful for identifying disk usage.





Step 16: Find Recently Changed Configs

Find files changed in /etc in last 2 days:

sudo find /etc -mtime -2 -type f

- Great for troubleshooting config changes.





Step 17: Find and Count Files

Count total .txt files:

find . -type f -name "*.txt" | wc -l





- Step 18: Real-World DevOps Examples

Task	Command

Find log files > 50MB	find /var/log -type f -name "*.log" -size

+50M

Find old temp files	find /tmp -type f -mtime +7 Find all shell scripts	find / -type f -name "*.sh" Delete .pyc cache files	find . -name "*.pyc" -delete Find broken symlinks	find . -xtype l

List only directories	find . -type d



Find all files with permission 777

Find files modified in last 1


find . -perm 777



hour	find . -mmin -60





- Step 19: Clean Up

When done:



cd ~

rm -rf ~/find-demo





- Summary Table

Option / Pattern	Description	Example

-name "pattern" Match name	-name "*.log"

-iname	Case-insensitive	-iname "*.TXT"

-type f/d	File or directory	-type f

-size +n/-n	File size	-size +100k

-mtime	Modified days ago -mtime -2

-user	By owner	-user root

-perm	Permissions	-perm 644

-empty	Empty files/dirs	-empty

-exec cmd {} \; Execute command -exec ls -l {} \;



- Pro Tip

You can combine find with other tools for powerful automation. Example — find and archive all logs older than 7 days:

find /var/log -type f -name "*.log" -mtime +7 -print | tar -cvzf o

Or delete them safely:

find /var/log -type f -name "*.log" -mtime +7 -exec rm -v {} \;

6. locate

a. Step 1: Install locate (if not already installed)

Most systems have it preinstalled, but check:

On Ubuntu/Debian:

sudo apt update

sudo apt install mlocate

On CentOS/RHEL/Fedora:



sudo yum install mlocate

After installation, initialize its database:

sudo updatedb

This builds /var/lib/mlocate/mlocate.db — the index file used by locate.



- Step 2: Verify Installation

Check version:

locate --version

Check where the database is stored:

locate -S

Output example:

Database /var/lib/mlocate/mlocate.db: 256,324 directories

1,548,213 files



- Step 3: Basic Usage

Let’s create a practice area:

mkdir ~/locate-demo cd ~/locate-demo

touch apple.txt banana.log cherry.txt mango.sh mkdir fruits veggies

touch veggies/carrot.txt veggies/potato.txt sudo updatedb

Now run:

locate apple

- Output:

/home/youruser/locate-demo/apple.txt

It found it instantly because it searches the prebuilt database.



Step 4: Search by Partial Name

You can search for any substring (not just full filenames):

locate txt

Lists all files containing “txt” in their path (may include system files too).



Step 5: Case-Insensitive Search

locate -i APPLE

Matches both apple.txt and Apple.txt if they exist.



Step 6: Limit Number of Results

Sometimes locate returns hundreds of matches. Limit with -n. Example:



locate -n 5 log

Shows only the first 5 results.



 Step 7: Filter by Exact Path (Using /)

If you want files only in a specific directory:

locate /home/youruser/locate-demo/

You can also pipe to grep for refined search:

locate txt | grep locate-demo





-

Step 8: The updatedb Command

Since locate uses a database, it may not see newly created files until you update the index. Let’s test:

1 Create a new file:

touch newfruit.txt

2 Try to locate it:

locate newfruit

X No output (database not updated yet) 3 Update the index:

sudo updatedb

4 Try again:

locate newfruit

Now it appears!

Tip: Some systems auto-update mlocate.db daily via cron or systemd.



Step 9: Permission Awareness

By default, locate lists only files you have permission to see. Root users can see all.

To locate system files (e.g., in /etc):

sudo locate passwd



Step 10: Excluding Paths

You can exclude directories from indexing by editing:

sudo nano /etc/updatedb.conf

Example section:

PRUNEPATHS="/tmp /var/tmp /var/cache /snap"

You can add paths you don’t want indexed (like large backups).



Then rebuild the index:

sudo updatedb



Step 11: Combine with grep for Better Filtering

Example: find only .txt files locate txt | grep '\.txt$' Find files in /etc only:

locate conf | grep '^/etc/'

Find .sh files owned by your home directory:

locate '.sh' | grep "$HOME"



- Step 12: Find Directory Names Only

To find directories, combine locate with grep and / at end:

locate /fruits/ | grep '/$'

Or use:

locate fruits | grep /fruits$



- Step 13: Performance Comparison with find

Let’s compare:

Using find

time find / -name "apple.txt" 2>/dev/null

Using locate

time locate apple.txt

⏱ You’ll see locate is significantly faster (milliseconds vs. seconds).



- Step 14: Locate Command Options Summary Option	Description	Example

-i	Case-insensitive search	locate -i apple

-n N	Limit to N results	locate -n 5 txt

-r regex Use regex search	locate -r '.*\.log$'

-S	Show database stats	locate -S

--help  Help manual	locate --help

-e	Check if file still exists	locate -e file.txt

-0	Null-separated output (for scripting) locate -0 '*.sh'



- Step 15: Using Regex Search (-r)

You can use regular expressions for flexible matching: Find all .sh or .bash files:

locate -r '\.sh$|\.bash$'

Find files that start with “car”:



locate -r '/car[^/]*$'



- Step 16: Check for Deleted Files

Since locate uses a database, it might still list deleted files. To confirm if they still exist, use -e:

locate -e oldfile.txt

If the file was deleted, it won’t be shown.



Step 17: Practical DevOps Use Cases Use Case	Command

Find config files quickly	locate .conf Find shell scripts in system	locate .sh Find nginx or apache configs `locate nginx

Find Python virtualenvs	locate site-packages Locate binary executables	locate bin/python List recent log files	`locate log

Check where docker files are `locate docker



Step 18: Hands-On Practice Tasks

Here’s a mini lab to strengthen your skills:



Task	Command (Try it Yourself)



Create a demo folder with some files

Update the locate database


mkdir -p ~/locate-lab && cd ~/locate-lab && touch apple.txt orange.log banana.conf grape.sh

sudo updatedb



Locate all .sh files	locate -r '\.sh$'



Locate files with “banana”

Case-insensitive search for “APPLE”


locate banana



locate -i apple



Show first 3 results only locate -n 3 txt



Verify file existence (check deleted file)


rm apple.txt && locate -e apple.txt



Check how many .log `locate -r '.log$' files exist



Display database statistics

Exclude /tmp from indexing


locate -S



Edit /etc/updatedb.conf and re-run sudo updatedb







Summary Table Command	Purpose

sudo updatedb Update locate database locate keyword Search for keyword locate -i	Case-insensitive

locate -n	Limit output

locate -r	Regex search

locate -S	Database stats

locate -e	Show only existing files



Pro Tips



locate is lightning-fast — great for day-to-day searches.

Use find when you need live results or filter by size/time/permissions. Combine locate with grep, wc, or xargs for powerful one-liners.

Run sudo updatedb periodically (or via cron) to keep it current.



