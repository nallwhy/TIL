## How to disable SSH host key checking for all hosts

```bash
echo "
Host *
    StrictHostKeyChecking no
    UserKnownHostsFile=/dev/null
" >> ~/.ssh/config
```bash

* StrictHostKeyChecking: It specifies how to react to an unrecognised or changed SSH host key. If you choose 'no', new host keys will be automatically added to the host key database file.
* UserKnownHostsFile: It specifies the database file to use for storing the user host keys (default is ~/.ssh/known_hosts). The `/dev/null` file is a special system device file that discards anything and everything written to it, and when used as the input file, returns End Of File immediately. If you don't configure the null device file as the host key database, connecting to hosts that changed there host key can be blocked.

Reference:  
http://linuxcommando.blogspot.kr/2008/10/how-to-disable-ssh-host-key-checking.html  
https://www.shellhacks.com/disable-ssh-host-key-checking/
