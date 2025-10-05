``` bash
echo "hello world"
echo hello world
```


## variable

``` bash
name="jaber"
echo "hello, $name"
```


## simple program
``` bash
#!/bin/bash

echo "What is your name?"
read f_name

echo "What is your age?"
read age

if [ "$age" -le 0 ]; then
    echo "Hold up bro, we are waiting for you"
else
    echo "Nice!!"
fi


echo hi $f_name , thanks for your time .

```