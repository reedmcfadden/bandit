### Level 0

1. To ssh into the server:
    - ssh -p 2220 bandit0@bandit.labs.overthewire.org
    - enter the provided password when prompted
1. Cat the readme file in bandit0's home dir to find the password for the next level!

### Level 1

1. To ssh into the server:
    - Use the same process as before, and use the password discovered in level 0.
1. View the contents of the file '-' in bandit1's home dir. This is a little tricky because cat interprets the '-' character as an instruction to read from stdin. I can get around this by providing the filepath './-'
1. As usual, view the password and use it to login to the next level as the next user.

### Level 2

1. Login
1. View the filename with spaces in it specified in the instructions. This can be done simply with tab completion. The idea here is that spaces separate arguments, so each word is seen as a separate filename. The spaces either need to be escaped like tab completion does automatically or the whole filname needs to be wrapped in quotes so that it is understood properly by the interpreter.
1. As usual, retrieve the password and use to login to the next level.

### Level 3

1. Ssh in as the new bandit user with the discovered password as usual.
1. Cat the hidden file in the ~/inhere/ diretory to see the password

### Level 4

1. Ssh in as the new bandit user with the discovered password as usual.
1. The password file is located under the same ~/inhere/ directory, but this time there are multiple files and only one is human readable text.
1. To determine which one is human readable text, I ran the 'file' command and cat'd the one file that was ASCII text to discover the password.

### Level 5

1. Ssh in as the new bandit user with the discovered password as usual.
1. This one is a bit trickier. Same as the previous two, the file with the password is located somewhere under the ~/inhere/ directory. This time though, there are multiple nested directories and many files, making manually finding the file a poor idea. 
1. The criteria that the password file can be identified by include being human-readable, 1033 bytes in size, and not executable.
1. To find the file, I used the 'find' command, searching for type file and for a size of 1033 bytes. More could be specified to look for a file that was also human-readable and not executable, but that wasn't necessary here.
    1. Here's the command I used, I used xargs to cat the file once find found it: `find ./inhere/ -type f -size 1033c | xargs cat`
    1. Updated command to more specifically to search for files that are not executable as well: `find ./inhere/ -type f -size 1033c -not -executable | xargs cat`

### Level 6

1. Ssh in as the new bandit user with the discovered password as usual.
1. This is similar to Level 5, but the criteria are different. This time the file to find is 33 bytes in size, owned by user bandit7 and owned by group bandit6.
1. I was able to craft a similar find command to find the password here: `find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null | xargs cat`
    1. The list was narrow enough to manually find the file without adding the group filtering, but adding the group filter narrowed it down to a single file which is nice and convenient for piping the file result to xargs and cat.

### Level 7

1. Ssh in as the new bandit user with the discovered password as usual.
1. This challenge requires the use of a new command: 'grep'. Greg can quickly search for text within a file. Since the key is hidden in a large file like a needle in a haystack, but next to a known word, making this is a great tool.
1. Command to find the key: `grep -i millionth ./data.txt | awk
 '{ print $2 }'`
    1. I grabbed the field I wanted by piping the output to awk.

### Level 8

1. Ssh in as the new bandit user with the discovered password as usual.
1. This challenge is similar to the previous, but there are lots of duplicate fake passwords in the file. The key is the only one that appears only once. 
1. To solve this, I used a combination of sort, uniq, and grep: `sort ./data.txt | uniq -c | grep -w 1`
    1. Sort obviously sorts the text, so all the duplicates will be next to each other. Uniq gets rid of the duplicates, and also shows a count of how many duplicates there originally were. I then grep'd for the only password that had one occurrence. The -w flag matches a whole 'word', and since the real password is the only one with a count of 1, it matches nicely. Alternatively you could grep for not 10 duplicates with '-v 10' because all of this other fake passwords had 10 duplicate occurrences. I went with the former because it seemed more precise.

### Level 9

1. Ssh in as the new bandit user with the discovered password as usual.
1. TODO - PICKUP HERE
