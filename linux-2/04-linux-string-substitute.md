## Linux  String Substitute

There is some data on Nautilus App Server 2 in Stratos DC. Data needs to be altered in several of the files. On Nautilus App Server 2, alter the <span style='color:cyan'>**/home/BSD.txt**</span> file as per details given below:



a. Delete all lines containing word <span style='color:cyan'>**following**</span> and save results in /home/<span style='color:cyan'>**BSD_DELETE.txt**</span> file. (Please be aware of case sensitivity)


b. Replace all occurrence of word <span style='color:cyan'>**the**</span> to <span style='color:cyan'>**for**</span> and save results in <span style='color:cyan'>**/home/BSD_REPLACE.txt**</span> file.


Note: Let's say you are asked to replace word to with from. In that case, make sure not to alter any words containing the string itself; for example upto, contributor etc.

### Solution
1. SSH to the server
2. Run
```
sed '/following/d' /home/BSD.txt > /home/BSD_DELETE.txt
```
3. Run
```
sed 's/\bthe\b/for/g' /home/BSD.txt > /home/BSD_REPLACE.txt
```