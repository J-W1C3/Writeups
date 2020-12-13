# Forense

## Encrypted Storage 1

Esta es la descripción del reto, y nos proporcionan

```
Our client was attacked by some ransomware. Maybe it was separatist dwarves?

He send us encrypted filesystem. Decrypt it, he need some data from secure storage.
```

We got a file

```
root@W1C3B0X:~/Descargas# file filesystem 
filesystem: Linux rev 1.0 ext4 filesystem data, UUID=500a749b-81c7-471a-9be5-73271dde40f1 (extents) (64bit) (large files) (huge files)
```

And I saw that the file gets files, and use foremost tool

```
root@W1C3B0X:~/Descargas# foremost filesystem 
Processing: filesystem
|foundat=flag.txtUT
*|
root@W1C3B0X:~/Descargas# cd output/
root@W1C3B0X:~/Descargas/output# ls
audit.txt  mov  pdf  png  zip
```

We see the zip and is protected with password so lets go with john

```
root@W1C3B0X:~/Descargas/output/zip# zip2john 00011568.zip > hash.txt
ver 1.0 efh 5455 efh 7875 00011568.zip/flag.txt PKZIP Encr: 2b chk, TS_chk, cmplen=28, decmplen=16, crc=FAC1E208
root@W1C3B0X:~/Descargas/output/zip# john hash.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
No password hashes left to crack (see FAQ)
root@W1C3B0X:~/Descargas/output/zip# john hash.txt --show
00011568.zip/flag.txt:cling:flag.txt:00011568.zip::00011568.zip

1 password hash cracked, 0 left
```

Now we have the password and lets go to extract de files!

```
root@W1C3B0X:~/Descargas/output/zip# unzip -P cling 00011568.zip 
Archive:  00011568.zip
 extracting: flag.txt                
root@W1C3B0X:~/Descargas/output/zip# cat flag.txt 
kks{n0t_s3cur3}
```
