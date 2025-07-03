[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [HPCC](index.md) :fontawesome-solid-angle-right: **File Access**


# To give file access

```
cd
setfacl -R -m g::r-x .
setfacl -R -m g:ME:r-x .
setfacl -R -m g:chem:r-x .

```