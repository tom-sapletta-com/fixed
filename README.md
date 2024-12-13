# fixed
fixed issues as devops





## "Too many Authentication Failures for user root" means that Your SSH server's **MaxAuthTries limit was exceeded**. It happens so that Your client is trying to authenticate with all possible keys stored in /home/USER/.ssh/ .

 This situation can be solved by these ways:
 
1.  ssh **\-i /path/to/id\_rsa** root@host
2.  Specify **Host/IdentityFile** pair in **/home/USER/.ssh/config**

A single host in the **config** file should look something like this:

    Host example.com
      IdentityFile /home/USER/.ssh/id_rsa
    

You can also set the user so you don't need to enter it on the command line and shorten long FQDN's too, see this example:

    host short
      IdentityFile /home/USER/.ssh/id_rsa
      User someuser
      HostName really-long-domain.example.com
    

You then connect to the really-long-domain.example.com server with:

    ssh short
    

Note: if you choose to use only the second option, and try to use ssh example.com you will still get errors (if that;s what brought you here), the short version will not give the errors, you can also use both options so you can ssh anyuser@example.com without the errors.

3.  Increase **MaxAuthTries** value on the SSH server in **/etc/ssh/sshd\_config** (not recommended).




I fixed this problem in my systems by running following commands:

eval $(ssh-agent)
ssh-add  ~/.ssh/id_rsa
