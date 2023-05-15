# First of all
```
man ssh-keygen
man ssh-copy-id
```

* ~/.ssh/ - standard ssh dir location in home directory
* ~/.ssh/config - config for hosts, users and identiti files (keys) 
* ~/.ssh/authorized_keys - list of authorized keys

# Generate new ssh key
```
ssh-keygen -t ed25519 -C "username@pc" -f id_ed25519_custom
```
or
```
ssh-keygen -t rsa -b 4096 -C "username@pc" -f id_rsa_custom

```

*Explanation:*
* -t - type: ed25519, ecdsa, rsa
* -f - custom key name if needed (public part will be located with .pub extension) 
* -b - block size in bits

# Copy key to server

```
ssh-copy-id username@server.domain.tld
ssh-copy-id -i /path/to/id_ed25519_custom username@10.11.12.13
```

*Explanation:*
* -i - path to key location. If argument omitted then ~/.ssh/id_rsa, ~/.ssh/id_dsa, ~/.ssh/id_ecdsa, ~/.ssh/id_ecdsa_sk, ~/.ssh/id_ed25519, and ~/.ssh/id_ed25519_sk will be added
* username - username at remote server

# SSH Agent

Add identity to agent.
Allows to add key for use with openssh auth agent. Without this you have to enter pass phrase for key every time you use it.
```
ssh-add ~/.ssh/id_rsa
```

Remove identity from agent.
Allows to avoid using your key without pass phrase, if you added key to agent previously.
```
ssh-add -d ~/.ssh/id_rsa
```

Also you can manually add contents of public part (id_rsa.pub) to server location `/root/.ssh/authorized_keys` or `~/.ssh/authorized_keys` (dependint on user on remote server)