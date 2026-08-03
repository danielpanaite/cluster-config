## Terminal theme installer

### Truenas

Add config to **/etc/bash.bashrc** after system updates
```shell
if [ -x /mnt/fuji/home/bin/oh-my-posh ]; then
	eval "$(/mnt/fuji/home/bin/oh-my-posh init bash --config /mnt/fuji/home/sushi_shell.json)"
fi
```