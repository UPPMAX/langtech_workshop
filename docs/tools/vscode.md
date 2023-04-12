* Visual studio code is great for remote development if you want IDE feature
  e.g. code completion and debugging.
* For a general introduction please see: <https://code.visualstudio.com/docs/remote/ssh>

## Running VSCode on compute nodes

It is possible to use the login node as a "jump box"

```
$ ssh -J host1 host2
```

We can also set this up in the `~/.ssh/config` file as:

``` bash title="~/.ssh/config"
### First jump host. Directly reachable
Host betajump
  HostName jumphost1.example.org
 
### Host to jump to via jumphost1.example.org
Host behindbeta
  HostName behindbeta.example.org
  ProxyJump  betajump
```

However, we don't know which compute node we will be allocated. This can be
solved by some `regex`

``` bash  title="~/.ssh/config
Host *+*
  ProxyCommand ssh $(echo %h | sed 's/+[^+]*$//;s/\([^+%%]*\)%%\([^+]*\)$/\2 -l \1/;s/:/ -p /') nc $(echo %h | sed 's/^.*+//;/:/!s/$/ %p/;s/:/ /')
```

which allows you to do stuff like

```
ssh matpiq@rackham5+rackham2
```

in VScode
