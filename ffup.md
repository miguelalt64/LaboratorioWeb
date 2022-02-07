# ATTACKING WEB APPLICATIONS WITH FFUF

## Introduction

Welcome to the Attacking Web Applications with Ffuf module!

There are many tools and methods to utilize for directory and parameter fuzzing/brute-forcing. In this module we will mainly focus on the ffuf tool for web fuzzing, as it is one of the most common and reliable tools available for web fuzzing.

The following topics will be discussed:

- Fuzzing for directories
- Fuzzing for files and extensions
- Identifying hidden vhosts
- Fuzzing for PHP parameters
- Fuzzing for parameter values

Tools such as ffuf provide us with a handy automated way to fuzz the web application's individual components or a web page. This means, for example, that we use a list that is used to send requests to the webserver if the page with the name from our list exists on the webserver. If we get a response code 200, then we know that this page exists on the webserver, and we can look at it manually.

## Web Fuzzing

We will start by learning the basics of using ffuf to fuzz websites for directories. We run the exercise in the question below, and visit the URL it gives us, and we see the following website:
   
http://SERVER_IP:PORT
![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/htbimg/web_fnb_main_site.jpg)

The website has no links to anything else, nor does it give us any information that can lead us to more pages. So, it looks like our only option is to 'fuzz' the website.

### Fuzzing

The term fuzzing refers to a testing technique that sends various types of user input to a certain interface to study how it would react. If we were fuzzing for SQL injection vulnerabilities, we would be sending random special characters and seeing how the server would react. If we were fuzzing for a buffer overflow, we would be sending long strings and incrementing their length to see if and when the binary would break.

We usually utilize pre-defined wordlists of commonly used terms for each type of test for web fuzzing to see if the webserver would accept them. This is done because web servers do not usually provide a directory of all available links and domains (unless terribly configured), and so we would have to check for various links and see which ones return pages. For example, if we visit https://www.hackthebox.eu/doesnotexist, we would get an HTTP code 404 Page Not Found, and see the below page:
 
https://www.hackthebox.eu/doesnotexist
![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/htbimg/web_fnb_HTB_404.jpg)

However, if we visit a page that exists, like /login, we would get the login page and get an HTTP code 200 Found, and see the below page:
   
https://www.hackthebox.eu/login
![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/htbimg/web_fnb_HTB_login.jpg)

This is the basic idea behind web fuzzing for pages and directories. Still, we cannot do this manually, as it will take forever. This is why we have tools that do this automatically, efficiently, and very quickly. Such tools send hundreds of requests every second, study the response HTTP code, and determine whether the page exists or not. Thus, we can quickly determine what pages exist and then manually examine them to see their content.

### Wordlists

To determine which pages exist, we should have a wordlist containing commonly used words for web directories and pages, very similar to a Password Dictionary Attack, which we will discuss later in the module. Though this will not reveal all pages under a specific website, as some pages are randomly named or use unique names, in general, this returns the majority of pages, reaching up to 90% success rate on some websites.

We will not have to reinvent the wheel by manually creating these wordlists, as great efforts have been made to search the web and determine the most commonly used words for each type of fuzzing. Some of the most commonly used wordlists can be found under the GitHub SecLists repository, which categorizes wordlists under various types of fuzzing, even including commonly used passwords, which will later utilize for Password Brute Forcing.

Within our PwnBox, we can find the entire SecLists repo available under /opt/useful/SecLists. The specific wordlist we will be utilizing for pages and directory fuzzing is another commonly used wordlist called directory-list-2.3, and it is available in various forms and sizes. We can find the one we will be using under:

```bash
Miguel Angel@htb[/htb]$ locate directory-list-2.3-small.txt
/opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt
```

> Tip: Taking a look at this wordlist we will notice that it contains copyright comments at the beginning, which can be considered as part of the wordlist and clutter the results. We can use the following command to get rid of these lines:

### Removing Comments

```bash
Miguel Angel@htb[/htb]$ sudo sed -i 's/^\#.*$//g' /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt && sudo sed -i '/^$/d' /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt
```

## Directory Fuzzing

Now that we understand the concept of Web Fuzzing and know our wordlist, we should be ready to start using ffuf to find website directories.

### Ffuf

Ffuf is pre-installed on your PwnBox instance. If you want to use it on your own machine, you can either use "apt install ffuf -y" or download it and use it from its GitHub Repo. As a new user of this tool, we will start by issuing the ffuf -h command to see how the tools can be used:

```bash
Miguel Angel@htb[/htb]$ ffuf -h

HTTP OPTIONS:
  -H               Header `"Name: Value"`, separated by colon. Multiple -H flags are accepted.
  -X               HTTP method to use (default: GET)
  -b               Cookie data `"NAME1=VALUE1; NAME2=VALUE2"` for copy as curl functionality.
  -d               POST data
  -recursion       Scan recursively. Only FUZZ keyword is supported, and URL (-u) has to end in it. (default: false)
  -recursion-depth Maximum recursion depth. (default: 0)
  -u               Target URL
...SNIP...

MATCHER OPTIONS:
  -mc              Match HTTP status codes, or "all" for everything. (default: 200,204,301,302,307,401,403)
  -ms              Match HTTP response size
...SNIP...

FILTER OPTIONS:
  -fc              Filter HTTP status codes from response. Comma separated list of codes and ranges
  -fs              Filter HTTP response size. Comma separated list of sizes and ranges
...SNIP...

INPUT OPTIONS:
...SNIP...
  -w               Wordlist file path and (optional) keyword separated by colon. eg. '/path/to/wordlist:KEYWORD'

OUTPUT OPTIONS:
  -o               Write output to file
...SNIP...

EXAMPLE USAGE:
  Fuzz file paths from wordlist.txt, match all responses but filter out those with content-size 42.
  Colored, verbose output.
    ffuf -w wordlist.txt -u https://example.org/FUZZ -mc all -fs 42 -c -v
...SNIP...
```

As we can see, the help output is quite large, so we only kept the options that may become relevant for us in this module.

### Directory Fuzzing

As we can see from the example above, the main two options are -w for wordlists and -u for the URL. We can assign a keyword to a wordlist to refer to it where we want to fuzz. For example, we can pick our wordlist and assign the keyword FUZZ to it by adding :FUZZ after it:

```bash  
Miguel Angel@htb[/htb]$ ffuf -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ
```

Next, as we want to be fuzzing for web directories, we can place the FUZZ keyword where the directory would be within our URL, with:

```bash
Miguel Angel@htb[/htb]$ ffuf -w <SNIP> -u http://SERVER_IP:PORT/FUZZ
```

Now, let's start our target in the question below and run our final command on it:

```bash
Miguel Angel@htb[/htb]$ ffuf -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ


        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.1.0-git
________________________________________________

 :: Method           : GET
 :: URL              : http://SERVER_IP:PORT/FUZZ
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
________________________________________________

<SNIP>
blog                    [Status: 301, Size: 326, Words: 20, Lines: 10]
:: Progress: [87651/87651] :: Job [1/1] :: 9739 req/sec :: Duration: [0:00:09] :: Errors: 0 ::
```

We see that ffuf tested for almost 90k URLs in less than 10 seconds. This speed may vary depending on your internet speed and ping if you used ffuf on your machine, but it should still be extremely fast.

We can even make it go faster if we are in a hurry by increasing the number of threads to 200, for example, with -t 200, but this is not recommended, especially when used on a remote site, as it may disrupt it, and cause a Denial of Service, or bring down your internet connection in severe cases. We do get a couple of hits, and we can visit one of them to verify that it exists:

http://SERVER_IP:PORT/blog

We get an empty page, indicating that the directory does not have a dedicated page, but also shows that we do not have access to it, as we do not get an HTTP code 404 Not Found or 403 Access Denied. In the next section, we will look for pages under this directory to see whether it is really empty or has hidden files and pages.

