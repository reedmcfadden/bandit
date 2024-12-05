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

1. Pickup here.
