# Old-school-conky-bars
Examples of a more oldschool approach to the different bars

These are all handmade for a 36 letter wide window. You will need to account for percent/symbol when modifying the scripts.
i.e. you´ll have to do some math to make it work in your setup. To get a nice gradient you can use https://htmlcolorcodes.com/color-picker/
Remember to cut out the # from hex color codes.

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
