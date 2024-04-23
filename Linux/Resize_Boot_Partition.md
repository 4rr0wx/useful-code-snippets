
Tried it for Ubuntu worked fine there:

1. Run below command to get PV (Physical Volume) name (Ex: `/dev/sda1`)
```
sudo pvs
```

2. Resize the PV (Ex: `sudo pvresize /dev/sda1`)
```
sudo pvresize <PV name from above step>   
```

3. Run below command to get root logical volume name (Filesystem value of `/` row; ex: `/dev/mapper/ubuntu--vg-root`)
```
df -h
```

4. Expand logical volume (ex : `sudo lvextend -r -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv`):
```
sudo lvextend -r -l +100%FREE <root logical volume name from above step>   
```
