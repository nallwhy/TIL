## Finding big directories and files on Ubuntu

Directories
```bash
du -sh /*
```

Files
```bash
sudo find / -type f -size +10M -exec ls -lh {} \;
```

Reference:  
https://superuser.com/questions/162749/how-to-get-the-summarized-sizes-of-folders-and-their-subfolders  
https://stackoverflow.com/questions/20031604/amazon-ec2-disk-full  
  