# THM-ConvertMyVideo-Writeup
- I can see port 22 for ssh and port 80 for HTTP open so I'm gonna try to detect them.
<img width="795" height="327" alt="image" src="https://github.com/user-attachments/assets/a72adca4-ae19-4e7f-808b-2ae3b5716e12" />

- I gonna open the web server to see what information we can get more and it contain a tool covert youtubeID to mp3
  <img width="541" height="427" alt="Screenshot 2025-07-17 120019" src="https://github.com/user-attachments/assets/0999b44b-b92b-4708-a8e1-0f5edbc772ec" />

- I try to utilize semicolon ( ; ) or use the backticks ( ` ) and its work so I think it contains Command Injection vulnerability but there is a problem that if we have a <space character> the command won't be executed so I use ${IFS} to get a reverse shell by using wget ( I also use chmod to make sure that reverse shell is enabled to run )
<img width="1092" height="491" alt="Screenshot 2025-07-17 122158" src="https://github.com/user-attachments/assets/2e0b4f2c-cda3-4e7e-af9b-af7cf43ed037" />

- To use that reverse shell, I use this command ( ;bash${IFS}rev.sh; )
  <img width="546" height="350" alt="Screenshot 2025-07-17 122611" src="https://github.com/user-attachments/assets/c2d1ec24-485a-4858-a495-2e596cda97ed" />

- Using nc to listen, I get the low-level user and the user flag is located in /var/www/html/admin folder
<img width="663" height="257" alt="image" src="https://github.com/user-attachments/assets/723ffecf-c49a-4ff4-be58-5d995f07d333" />

- After that, I download pspy64 to discover the crontab in this machine and I detect that /var/www/html/tmp/clean.sh is running once every minute
  <img width="972" height="144" alt="Screenshot 2025-07-17 222627" src="https://github.com/user-attachments/assets/1a732f53-a9a8-44bf-8c4a-749a7c71e8dc" />

- So I use echo command to rewrite clean.sh to make that file become a reverse shell
  <img width="813" height="251" alt="Screenshot 2025-07-17 233754" src="https://github.com/user-attachments/assets/117895c2-9ae4-4545-ab78-a0c479c3ead2" />

- And after execute that modified clean.sh and waiting for about 1 minute, I gain a root user
  <img width="653" height="278" alt="Screenshot 2025-07-17 222543" src="https://github.com/user-attachments/assets/dae102f8-2124-4cf3-b789-85e89364904a" />


