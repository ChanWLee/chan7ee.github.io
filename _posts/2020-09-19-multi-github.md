---
title: "SSH key & multi GitHub & IntelliJ"
date: 2020-09-19 23:03:30 +0900
categories: chan update
---
## SSH key 발급

- git bash에서 실행
- 아래 명령 입력, 이메일은 수정

```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
- 엔터 클릭

```bash
Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
```

- SSH 암호 입력, 암호입력없이 하려면 엔터

```bash
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
```
- ssh key 클립보드에 복사

```bash
$ clip < ~/.ssh/id_rsa.pub
```

## 발급한 SSH key를 ssh-agent에 등록

- ssh-agent 시작하기
```
# start the ssh-agent in the background
```

> Git Bash
```bash
$ eval "$(ssh-agent -s)"
```
> 다른 terminal
```bash
$ eval $(ssh-agent -s)
```

- SSH key를 ssh-agent에 추가
```bash
$ ssh-add ~/.ssh/id_rsa
```


## GitHub 계정에 SSH key 등록

- Sign in  > 아이콘 클릭 > Settings

> ![](https://help.github.com/assets/images/help/settings/userbar-account-settings.png)

- SSH keys > New SSH key

>![](https://help.github.com/assets/images/help/settings/settings-sidebar-ssh-keys.png)

- Title 입력, Key > Ctrl+V

>![](https://help.github.com/assets/images/help/settings/ssh-key-paste.png)

- Addd SSH key

>![](https://help.github.com/assets/images/help/settings/ssh-add-key.png)


- GitHub 암호 입력

***


Multi SSH keys 셋팅
---

- 위의 방법으로 여러개의 키를 생성, ssh-agent에 추가

- 저장된 keys 확인

`$ ssh-add -l`

- ssh config 수정

```bash
    $ cd ~/.ssh/
    $ touch config
    $ vi config
```

- 내용추가
```shell
    #activehacker GitHub계정ID
    Host github.com-activehacker
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa_activehacker

    #jexchan GitHub계정ID
    Host github.com-jexchan
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa_jexchan
```
***
## IntelliJ 에 SSH key 적용

- VCS > Checkout from Version Control > Git

> Git Repository URL:  `github.com-jexchan:jexchan/repo`

```
github.com-jexchan: config에서 설정한 Host
jexchan: github의 id
repo: repository 이름
```
 Parent Directory: `/User/workspace`<br />
 Directory Name: `repo`

- Test 클릭

- Clone 클릭
