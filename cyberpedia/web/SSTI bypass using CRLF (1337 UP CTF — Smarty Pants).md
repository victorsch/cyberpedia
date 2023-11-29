by The WhiteHat Panther

#ssti #crlf #php #smarty #newline #regexbypass

Hi mates! This writeup is intended to showcase the following:

1. SSTI in template Smarty (PHP)
2. Bypassing regex filters using a new line injection

First of all, let’s see how PHP behaves when we invoke a new line inside a function call:

![](https://miro.medium.com/v2/resize:fit:700/0*XIQ5G7UWT-G9zPro.png)

As we can see, our code is:

<?php system('whoami'  
);?>

Now we have confirmed we can inject the sequence \n without breaking the code.

The next step is to confirm our attack vector:

![](https://miro.medium.com/v2/resize:fit:700/0*-knXjPPqhngnXYXM.png)

![](https://miro.medium.com/v2/resize:fit:700/0*iIjrHZyXuj6C21JK.png)

It’s time to take a look at one of our best friends:

[https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection#smarty-php](https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection#smarty-php)

We can see that an input like {system(‘ls’)} should give us RCE. however {} is being restricted by the regex:

![](https://miro.medium.com/v2/resize:fit:700/0*yWY0Tqx376Z5zHRo.png)

![](https://miro.medium.com/v2/resize:fit:700/0*s69RVPCPhtqbWDtF.png)

So, let’s now inject a line terminator \n, in Burp Suite we can do it like this:

- {system(‘ls’)%0a} using URL-encoded new line
- Showing non-printable chars to inject a visible \n

Let’s use the last option first:

![](https://miro.medium.com/v2/resize:fit:700/0*bEBDQOEkMAIiXMaW.png)

To complete the challenge let’s use now %0a:

![](https://miro.medium.com/v2/resize:fit:700/0*JdVSPLztSruuRYyy.png)

That is how we finally manage to get the flag: INTIGRITI{php_4nd_1ts_many_f00tgun5}

I hope you enjoyed the write-up. Don’t forget to follow me to get some cool info regarding AppSec.