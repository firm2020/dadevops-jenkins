# Build and run Jenkins
```console
docker-compose up -d
```

# Setup SSH Keys for Build Agent (optional)
```console
$ ssh-keygen -t ed25519 -f jenkins_agent
Generating public/private ed25519 key pair.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in jenkins_agent
Your public key has been saved in jenkins_agent.pub
The key fingerprint is:
SHA256:fxSDpx446tbQzZNGrjZejrqnFd/1kaweXKXzL2cYHno james@james-CELSIUS
The key's randomart image is:
+--[ED25519 256]--+
|                 |
|           .     |
|          . +   .|
|         ..o o..o|
|       .S=o.. += |
|      ...*B+..=+.|
|      .o.o=.o* +o|
|     ...*+ .o E +|
|     .=Bo..  o +.|
+----[SHA256]-----+

$ cat jenkins_agent
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACDPPvuKX/+7Vbgj3yrofEVibEwZOPihhrYDLjwcHyDxoQAAAJhv1aFvb9Wh
bwAAAAtzc2gtZWQyNTUxOQAAACDPPvuKX/+7Vbgj3yrofEVibEwZOPihhrYDLjwcHyDxoQ
AAAEB9xj5JhPG63RSAVgWJAB/h/To/1LVAega7lUxeFTKZpc8++4pf/7tVuCPfKuh8RWJs
TBk4+KGGtgMuPBwfIPGhAAAAE2phbWVzQGphbWVzLUNFTFNJVVMBAg==
-----END OPENSSH PRIVATE KEY-----


$ cat jenkins_agent.pub 
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIM8++4pf/7tVuCPfKuh8RWJsTBk4+KGGtgMuPBwfIPGh james@james-CELSIUS

$ docker exec -it agent /bin/bash
root@f3d90bf675ae:/home/jenkins# cd .ssh
root@f3d90bf675ae:/home/jenkins/.ssh# rm authorized_keys 
root@f3d90bf675ae:/home/jenkins/.ssh# echo "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKWKeVt7eyTNeJcR0poQk9gZtedINDHTI7BKuVXAZ9Je james@james-CELSIUS" > authorized_keys
root@f3d90bf675ae:/home/jenkins/.ssh# chmod 600 authorized_keys
root@f3d90bf675ae:/home/jenkins/.ssh# chown jenkins:jenkins authorized_keys

$ docker-compose up -d
Creating network "jenkins_default" with the default driver
Creating jenkins ... done
Creating agent   ... done
```

