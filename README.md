# Old-school-conky-bars
Examples of a more oldschool approach to the different bars

These are all handmade for a 36 letter wide window. You will need to account for percent/symbol when modifying the scripts.
i.e. you´ll have to do some math to make it work in your setup. To get a nice gradient you can use https://htmlcolorcodes.com/color-picker/
Remember to cut out the # from hex color codes. The GPU & VRAM utilization is based on a nvidia setup.

Example:<br>
<img width="337" height="33" alt="low" src="https://github.com/user-attachments/assets/57d24a05-e450-4c60-b4b8-e93e637449ec" />
<img width="339" height="35" alt="full" src="https://github.com/user-attachments/assets/b5db231c-5ffa-4e2f-b267-ae98b93d5004" />

<h3>CPU Usage:</h3>

conky.conf
~~~
${execpi 5 /your/folder/conky/scripts/CPU_ut.sh}
${voffset -33}
{font :bold:size=6}|' ' ' ' ' ' '25' ' ' ' ' ' ' '50' ' ' ' ' ' ' '75' ' ' ' ' ' '|
~~~
CPU_ut.sh
~~~
#!/bin/sh
mpstat 1 1 | awk 'NR==5{
   n = ((100-$12)/2.857); two = 10;  three = 20; four = 30;
   if(n>=four) {
        t = "${color FF00C0}";
        for(;n>=four;n--)
                t = t "\\#"
    }
   if(n>=three) {
        r = "${color B80088}";
        for(;n>=three;n--)
                r = r "\\#"
    }
   if(n>=two){
        a = "${color 780057}";
        for(;n>=two;n--)
                a = a "\\#"
    }
    f = "${color 4A0033}";
    for(;n>0;n--)
                f = f "\\#";
   print f a r t
  }'
~~~

<h3>GPU Usage:</h3>

conky.conf
~~~
${execpi 5 /your/folder/conky/scripts/GPU_ut.sh}
${voffset -33}
{font :bold:size=6}|' ' ' ' ' ' '25' ' ' ' ' ' ' '50' ' ' ' ' ' ' '75' ' ' ' ' ' '|
~~~
CPU_ut.sh
~~~
#!/bin/sh
nvidia-smi --query-gpu=utilization.gpu --format=csv,noheader | sed 's/ %//' | awk 'NR==1{
   n = ($1/2.857); two = 10;  three = 20; four = 30;

And so on...
~~~

<h3>RAM Usage:</h3>

conky.conf
~~~
${execpi 5 /your/folder/conky/scripts/RAM_ut.sh} 
${voffset -33}
{font :bold:size=6}|' ' ' ' ' ' '25' ' ' ' ' ' ' '50' ' ' ' ' ' ' '75' ' ' ' ' ' '|
~~~
RAM_ut.sh (32Gb of RAM)
~~~
#!/bin/sh
cat /proc/meminfo | awk 'NR==3{
   n = ((((32659836-$2)/1024)/1024)*1.1428);two = 10;  three = 15; four = 25; 

And so on...
~~~

<h3>VRAM Usage:</h3>

conky.conf
~~~
${execpi 5 /your/folder/conky/scripts/VRAM_ut.sh}
${voffset -33}
{font :bold:size=6}|' ' ' ' ' ' '25' ' ' ' ' ' ' '50' ' ' ' ' ' ' '75' ' ' ' ' ' '|
~~~
VRAM_ut.sh
~~~
#!/bin/sh
nvidia-smi -i=0 --query-gpu=utilization.memory --format=csv,noheader | awk 'NR==1{
   n = (($1)/2.857);two = 10;  three = 15; four = 25;

And so on...
~~~


<h3>Have fun Conking!</h3>
