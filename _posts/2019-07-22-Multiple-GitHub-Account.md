---
layout: post
title: Multiple GitHub Accounts
author: aditya
categories: [ github, git ]
featured: false
image: assets/images/20190722MultipleGitHubAccount_github.jpg
excerpt: "Using Multiple GitHub Accounts on the same system to run git commands"
---


#### The post is also available on the author's Personal Website : [Multiple GitHub Accounts](https://ramanaditya.github.io/blogs/Multiple-GitHub-Account)

Many a times you need to work with two different Github Accounts. If you are using macOs or windows, they save your account information and don't give permissions to operate other accounts.

In order to run git commands for two different github accounts you need to follow the following step by step procedure.

### Generating SSH Key for the account

{% highlight bash %}
ssh-keygen -t rsa -C "Github-email-address"
Generating public/private rsa key pair.

{% endhighlight %}

{% highlight bash %}
Enter file in which to save the key (/Users/aditya/.ssh/id_rsa): /Users/aditya/.ssh/id_rsa_aditya
Created directory '/Users/aditya/.ssh'.
{% endhighlight %}

{% highlight bash %}
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/aditya/.ssh/id_rsa_aditya.
Your public key has been saved in /Users/aditya/.ssh/id_rsa_aditya.pub.
The key fingerprint is:
SHA256:SPfrZGNVJ+gHaidkUrCoOvLcnfDPqn9gRZ3L7cBoAiyE aditya@gmail.com
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|                 |
|   E ....     o.o|
|    ..o*o.  o..=.|
|     .+oS+.=.+ +.|
|    .     Oo+ . O|
|     o.  .** .   |
|      o=oX+.*    |
|     .=*O=+. .   |
+----[SHA256]-----+

{% endhighlight %}

### Copy your SSH key using the command given below

{% highlight bash %}
pbcopy < ~/.ssh/id_rsa_example.pub

{% endhighlight %}


Now you need to add this key in your Github Account

{% highlight bash %}
Open GitHub -> Settings -> SSH and GPG keys -> New SSH Keys -> Copy the key -> Add SSH Key

{% endhighlight %}

Repeat the above steps for the second github account.

### Setup Github Host

{% highlight bash %}
touch ~/.ssh/config

vi config

{% endhighlight %}

{% highlight editor %}

#first account
Host github.com-aditya
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_aditya
#second account
Host github-raman
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_raman

{% endhighlight %}

{% highlight git %}

git init
git remote set-url origin git@github-raman:{ username } / { repository name with .git extension eg., aditya.git}

git config --global user.email "{ your github email }"
git config --global user.name "{ your github name }"

git status
git add --all
git commit -m "commit message"
git push

{% endhighlight %}

Thank you for being the patient reader. Please like and share this post

### To read similar posts by the author please visit [this site](https://ramanaditya.github.io/)