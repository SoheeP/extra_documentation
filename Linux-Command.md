# 리눅스 Command

### 자주 쓰는 Command

| Command                           | Description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| `ifconfig`                        | 네트워크 인터페이스를 설정하는 명령                          |
| `pwd` (print workin directory)    | 현재 작업중인 디렉토리 정보 출력                             |
| `traceroute [domain or IP]`       | - 네트워크 경로를 추적 <br />- 단, ICMP 프로토콜을 제한하는 라우터가 중간에 존재할 경우 <br />정보를 파악할 수 없음. |
| `dig` (domain information groper) | 네임서버로부터 정보를 가져올 수 있는 툴                      |
| `nslookup`                        | DNS 서버에 질의(query)를 보내 name server 관련된 조회를 할 수 있는 명령어. |
| `w`                               | 서버와 접속한 사용자의 접속 정보 및 작업정보를 확인하는 명령어 |
| `nmap` (network mapper)           | 네트워크 탐색과 보안감사를 하는 오픈 소스 툴                 |
| `cd` (change directory)           | 경로 이동                                                    |
| `ls` (list)                       | - 디렉토리 목록 확인<br />- `-R` 옵션은 하위목록까지 전부 보여준다.<br />- `-l` 명령으로 최근 업데이트 일자를 확인할 수 있다. |
| `find`                            | - 특정 파일이나 디렉토리를 검색<br />- 옵션으로는 `-name`, `-type`이 있고 다양하게 활용해서 찾을 수 있다. |
| `mkdir`(make directory)           | - 디렉토리 생성<br />-  `-p` 옵션을 주면 하위 디렉토리까지 한 번에 생성 가능 |
| `rm` (remove)                     | - 파일이나 디렉토리를 삭제<br />- `-r` 옵션은 디렉토리를 삭제할 때 씀<br />- `-f` 옵션을 주면 삭제여부를 붇지 않고 바로 삭제(주의) |
| `touch [filename]`                | - 파일이나 디렉토리의 최근 업데이트 일자를 현재 시간으로 변경<br />- 파일이나 디렉토리가 존재하지 않으면 빈 파일 생성 |
| `cp [source] [destination]`       | - 파일 혹은 디렉토리를 복사(copy)<br />- `-r` 옵션은 디렉토리 복사 |
| `mv [source] [destination]`       | - 파일 혹은 디렉토리를 원하는 위치로 이동<br />- 이름을 변경하는 용도로 사용하기도 함<br />- `cp`와 달리 디렉토리를 이동할 때도 별다른 옵션이 필요없음 |
| `cat` (concatenate)               | - 파일의 내용을 출력<br />- 파일 여러개를 합쳐 하나의 파일로 만들기<br />- 기존 파일에 다른 파일 내용을 덧붙일 수 있음<br />- 새로운 파일을 만들 때도 사용 |
| `head`                            | - 파일의 앞 부분을 보고 싶은 줄 수 만큼 보여준다. <br />- 옵션을 정하지 않으면 상위 10줄을 보여준다. |
| `tail`                            | - 파일의 뒷부분을 보고 싶은 줄 수 만큼 보여준다. <br />옵션을 정하지 않으면 하위 10줄을 보여준다.<br />- `-F` 옵션을 주고 실행하면 파일 내용을 계속 화면에 띄워주고, <br />변했을 때 업데이트 된 내용을 갱신해준다.(로그파일에 유용) |
| `grep [option] pattern [file]`    | - 특정 문자열을 찾을 때 사용하는 명령어.<br />- 정규표현식에 의한 패턴 매칭 방식을 사용한다. |
| `ln` (link)                       | - 링크파일을 만드는 명령어<br />- 심볼릭 링크와 하드 링크 방식이 있음. |
| `alias` (command alias)           | 자주 사용하는 명령어                                         |
| `du` (disk usage)                 | - 디렉토리와 모든 하위 디렉토리의 용량(KB) 표시<br />- `-s`로 선택한 디렉토리만의 용량을 확인할 수 있다.<br />- `h`옵션을 추가하면 용량이 읽기 편한 단위로 나온다. |
| `df` (disk free)                  | - 리눅스 시스템 전체의(마운트 된) 디스크 여유 공간 확인<br />- `h` 옵션을 추가하면 용량이 읽기 편한 단위로 나온다. |
| `free`                            | 메모리 사용량, 여유량, 캐싱 메모리를 파악할 수 있다.         |
| `uname`                           | 지정된 시스템 정보를 출력. 옵션이 없으면 `-s` 옵션과 같은 결과를 보여준다. |
| `ps`                              | 현재 시스템에서 돌고 있는 프로세스를 보여주는 명령어         |
| `kill [pid]` / `killall`          | PID에 선언된 시그널 사인을 프로세스에게 보낸다.              |
| `whereis`                         | 명령어의 위치(경로)를 알려주는 명령어                        |
| `chmod [option] [file]`           | 파일이나 디렉토리에 대한 접근 허용 범위를 변경               |



##### `ifconfig`

```bash
$ ifconfig [interface] [option] [address] [up/down]
```



**커맨드옵션**

* up/down: 인터페이스를 활성화/비활성화한다.
* netmask: 넷마스크 주소를 설정한다.
* broadcast: 브로드캐스트 주소를 설정한다.



##### `dig` (domain information groper)

```bash
$ dig @[server] [domain] [query-type] [query-class]
```

`nslookup`과 기능적인 차이는 크게 없지만 사용이 간결하고 출력이 상세하여 Shell Script 등에서 주로 사용된다.

* [server]
  - 질의를 하고자 하는 DNS 서버
  - 만약 name server를 명시하지 않으면 시스템의 resolv.conf 에 있는 네임서버에 query를 시도함.
    ​- resolv.conf : 사용하고자 하는 네임서버를 지정하는 파일.
* [domain]
  * 정보를 요청할 도메인 이름
* [query-type]
  * 요청한 정보에 대한 정보의 타입. 
* [query-class]
  * query의 network class 부분(확인하고자 하는 도메인)

상세 내용은 참조링크를 확인.

참조: [리눅스(Linux) DIG 사용법](https://websecurity.tistory.com/63)



##### `w`

```bash
$ w [options] [user]
```

아무 옵션 없이 `w`만 쓰면, 아래 결과 처럼 출력된다.

```bash
 21:41:07 up 12 days, 10:08,  2 users,  load average: 0.28, 0.20, 0.10
USER      TTY      FROM        LOGIN@   IDLE   JCPU   PCPU WHAT
root      pts/0    10.10.0.2   20:59    1.00s  0.02s  0.00s w
linuxize  pts/1    10.10.0.8   21:41    7.00s  0.00s  0.00s bash
```



`w` 명령어로 알 수 있는 정보

1. 서버의 현재 시각 정보
2. 서버의 부팅한 이후의 시스템 작동 시간
3. 서버 접속자의 총 수 
4. 접속자 별 서버 평균 부하율 정보
5. 접속자 별 서버 접속 계정명
6. 접속자 별 접속 TTY 명
   - TTY: The name of the terminal used by the user.
7. 접속자 별 접속한 IP 명
8. 접속자 별 로그인 시각 정보
9. 접속자 별 CPU 사용 정보(JCPU, PCPU 정보)
   - JCPU: The time used by all processes attached to the tty.
   - PCPU: The time used by the user's current process. The one displayed in the WHAT field.
10. 접속자 별 현재 사용 명령어 정보
    - WHAT: The user's current process and options/arguments.

**커맨드옵션**

* `-h`, `--no-header` : 헤더 정보를 제외한 결과를 표시.
* `-f`, `--from`: FROM 필드(접속 아이피)를 생략한 결과를 표시.
* `-s` : JCPU, PCPU 정보를 생략한 결과를 표시.



##### `cd` (change directory)

* 절대 경로 이동: 최상위 디렉토리(`/`)부터 시작해서 목표 디렉토리까지 가는 경로를 **전부** 기술하는 방식.
* 상대 경로 이동: 현재 자신이 있는 위치를 기준으로 이동하는 것이며, 현재 자신이 있는 위치는 `.`(마침표)로 표기한다.

```bash
$ cd /home/itholic/mydir
$ pwd
/home/itholic/mydir

$ cd ..
$ pwd
/home/itholic

```



##### 허가권(Permission)

`ls` 명령어를 실행해서 파일과 디렉토리의 목록에 나오는 부분을 리눅스에서는 **허가권(Permission)**이라고 부른다.

* `-rw-r--r--` : 파일(앞이 -로 시작)
* `drwxr-xr-x`: 디렉토리(앞이 d로 시작하면 디렉토리를 뜻함)

**rwx**

* r : read(읽기권한)
  * 파일에서의 'r': 파일의 내용을 읽어들이는 명령어와 관련
  * 디렉토리에서의 'r': 디렉토리 내용을 읽어들이는 것과 관련
* w: write(쓰기 권한)
  * 파일에서의 'w': 내용을 수정, 변경하는 명령어와 관련
  * 디렉토리에서의 'w': 디렉토리 및 그 내부의 생성 및 삭제와 관련
* x: execute(실행, 접근 권한)
  * 파일에서의 'x': 있으면 실행파일, 없으면 문서파일의 접근권한을 포함.
  * 디렉토리에서의 'x': 접근 권한의 여부





##### `mkdir` (make directory)

```bash
$ ls
testfile

$ mkdir testdir
$ ls
testdir/ testfile

$ mkdir -p a/b/c/d
$ ls -R a/
a/:
b/

a/b:
c/

a/b/c:
d/
```

위 내용이 전부 출력된다. 현재 폴더부터 마지막 폴더까지 하나하나 라인으로 보여준다.



##### `find`

기본 사용법: `find [검색경로] -name [파일명]`

```bash
$ ls
dir1/  dir3/  file1  file3  picture1.jpg  picture3.jpg
dir2/  dir4/  file2  file4  picture2.jpg  picture4.jpg


$ find ./ -name 'file1'
./file1


$ find ./ -name "*.jpg"
./picture1.jpg
./picture2.jpg
./picture3.jpg
./picture4.jpg
```



##### `head`

```bash
$ cat testfile
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15

$ head -3 testfile
1
2
3

$ head testfile
1
2
3
4
5
6
7
8
9
10
```



##### `tail`

```bash
$ tail -F testfile

6
7
8
9
10
11
12
13
14
15
(계속 화면 출력, 내용 변경시 자동으로 갱신)
```



##### `grep`

자주 사용하는 예제

| Option                     | Description                                                  |
| -------------------------- | ------------------------------------------------------------ |
| `grep "STR" [file]`        | 대상 파일에서 문자열 검색                                    |
| `grep "STR" *`             | 현재 디렉토리 모든 파일에서 문자열 검색                      |
| `grep "STR" *.ext`         | 특정 확장자를 가진 모든 파일에서 문자열 검색                 |
| `grep -i "STR" [file]`     | 대소문자 구분하지 않고 문자열 검색                           |
| `grep -v "STR" [file]`     | 매칭되는 pattern이 존재하지 <u>않는</u> 라인 선택            |
| `grep -w "STR" [file]`     | 단어(word) 단위로 문자열 검색                                |
| `grep -n "STR" [flie]`     | 검색된 문자열이 <u>포함된 라인 번호</u> 출력                 |
| `grep -r "STR" *`          | 하위 디렉토리를 포함한 모든 파일에서 문자열 검색             |
| `grep -m 100 "STR" [file]` | 최대 검색 결과 갯수 제한                                     |
| `grep -H "STR" *`          | 검색 결과 앞에 파일 이름 표시                                |
| `grep "A.*B" *`            | 문자열 A로 시작해서 B로 끝나는 패턴 찾기                     |
| `grep "STR[0-9]" *`        | 0-9 사이 숫자만 변경되는 패턴 찾기                           |
| `grep -F "*[]?..." [file]` | 문자열 패턴 전체를 정규표현식 메타문자가 아닌 일반 문자로 검색하기 |
| `grep "\*" [file]`         | 정규표현식 메타문자를 일반 문자로 검색하기(escape)           |
| `grep "^STR" [file]`       | 문자열 라인 처음 시작 패턴 검색하기                          |
| `grep "$STR" [file]`       | 문자열 라인 마지막 종료 패턴 검색하기.                       |



##### `ln`

```bash
$ ln [option] [source] [destination(or directory)]
```

* `-s`, 심볼릭링크(Symbolic Link): 단순히 원본파일을 가리키도록 링크만 시킨 것으로, MS의 '바로가기' 개념.
* 하드링크(Hard Link): 원본파일과 다른이름으로 존재하는 동일한 파일(동일한 내용의 다른 파일이기도 함). 원본 파일과 링크파일 두개가 서로 다른 파일이기 때문에 둘 중 하나를 삭제하더라도 하나는 그대로 남아있다.
  또, 하드링크에서는 원본파일 내용이 변경되면 링크파일 내용 또한 자동으로 변경된다.



##### `alias`

* `alias` : 리스트 출력
* `unalias [command]`: 특정 alias 해제
* `unalias -a`: 모든 alias 해제



##### `uname`

**커맨드 옵션**

* `-a`, `--all`: 모든 정보
* `-s`, `--kernel-name`: 커널이름 출력(옵션이 없을 경우 이 값과 동일하게 출력된다)
* `-n`, `--nodename`: 네트워크 노드에서의 호스트 이름을 출력
* `-r`, `--kernel-release`: 커널 release 번호 출력
* `-v`, `--kernel-version`: 커널 버전 번호 출력
* `-m`, `--machine`: 하드웨어 이름 출력
* `-p`, `--processor`: 프로세서 타입을 출력
* `-i`, `--hardware-platform`: 하드웨어 플랫폼 정보 출력
* `-o`, --operation-system` 운영체제 정보를 출력



###### `ps`

**커맨드옵션**

* `ax`, `-e`: 모든 프로세스 정보
  파이프를 이용해서 보여지는 목록을 제어할 수 있다.(ex: `ps ax|less`)

* `u`, `-f` 자세한 프로세스 정보

  ```bash
  $ ps aux
  USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND 
  root 1 0.0 0.3 33776 3724 ? Ss Mar19 0:04 /sbin/init 
  root 2 0.0 0.0 0 0 ? S Mar19 0:00 [kthreadd] 
  user 25011 0.0 0.5 26852 5244 pts/14 Ss 18:57 0:00 -bash 
  user 25164 0.0 0.2 22648 2488 pts/14 R+ 19:19 0:00 ps aux
  
  $ ps -ef
  UID PID PPID C STIME TTY TIME CMD 
  root 1 0 0 Mar19 ? 00:00:04 /sbin/init 
  root 2 0 0 Mar19 ? 00:00:00 [kthreadd] 
  user 25011 25010 0 18:57 pts/14 00:00:00 -bash 
  user 25112 25011 0 19:11 pts/14 00:00:00 ps -ef
  ```

* `-u [username]` : 특정 사용자 이름으로 목록을 필터링 할 수 있다. 이 때는 `-e` 옵션을 제거하고 명령을 입력한다.
  둘 이상일 경우는 콤마로 구분하여 입력

  ```bash
  $ ps -fu user 
  $ ps -f -u user 
  UID PID PPID C STIME TTY TIME CMD 
  user 25011 25010 0 18:57 pts/14 00:00:00 -bash 
  user 25280 25011 0 19:44 pts/14 00:00:00 ps -f -u user
  ```

* `-p`: 프로세스 ID로 목록을 필터링 할 수 있다.

* `-C`: 프로세스 이름으로 목록을 필터링 할 수 있다. 단, 와일드카드('*')나 부분적인 이름 검색이 안됌.

* `--sort`: 필요한 필드를 지정하여 오름차순('+'), 내림차순('-')으로 정렬할 수 있다.

  ```bash
  $ ps aux --sort=-pcpu,-pmem | head -5 
  USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND 
  root 1261 0.2 0.3 165508 3928 ? Sl Mar19 7:33 /usr/sbin/someprocess 
  lightdm 9040 0.0 1.9 839564 19988 ? Sl Mar19 0:06 /usr/sbin/otherprocess 
  root 9025 0.0 1.9 235720 19660 tty7 Ss+ Mar19 0:02 /usr/bin/process 
  lightdm 9086 0.0 1.6 508360 16632 ? Sl Mar19 0:00 /usr/lib/service 
  lightdm 9083 0.0 1.4 602992 14696 ? Sl Mar19 0:00 nm-applet
  ```

* `-o`: 원하는 컬럼만 보이도록 할 수 있다.

  ```bash
  $ ps -e -o pid,uname,pcpu,pmem,comm 
  PID USER %CPU %MEM COMMAND 
  1 root 0.0 0.3 init 
  2 root 0.0 0.0 kthreadd 
  25011 ykshin 0.0 0.5 bash 
  25497 ykshin 0.0 0.2 ps
  ```

* `watch`: 일정 시간마다 `ps`를 실행하여 실시간 감시자로 사용할 수 있다.



##### `kill`

시그널 목록은 `kill -l` 명령어로 전체 목록을 볼 수 있다.

시그널 숫자 또는 SIG를 뺀 이름을 주고 프로세스 ID를 주면 해당 프로세스에 시그널을 보낼 수 있다.

아래 명령어는 동일한 작업을 수행한다.

```bash
$ kill -INT [processID]

$ kill -2 [processID]
```

:exclamation: `kill -9`로 시그널을 보내면, 개발자가 구현한 종료 함수가 호출되지 않고 즉시 프로세스 종료가 되어버리므로 데이터 유실이나 리소스가 제대로 안 닫히는 문제가 발생할 수 있다.

&rarr; `kill -TERM [PID]`나 `kill -INT [PID]` 같이 종료를 의미하는 시그널을 여러번 전송하는 방법을 추천한다.



##### `killall` 

```bash
$ killall [option] [name]
```

프로세스 번호가 아닌 이름으로 프로세스를 종료시키는 명령어.



##### `whereis`

`which`와 같이 명령어의 위치(경로)를 반환하지만, 아래와 같은 차이가 있다.

* `which`: 현재 사용하고 있는 명령어의 실행파일(또는 링크)의 위치를 알 수 있다.

  ```bash
  $ which ls
  /bin/ls
  
  $ which python
  /usr/bin/python
  ```

* `whereis`: 명령어의 바이너리(실행파일), 소스, 매뉴얼 파일의 위치를 출력한다.

  ```bash
  $ whereis ls
  ls: /bin/ls /usr/share/man/man1/ls.1.gz
  
  $ whereis python
  (python 글자가 포함된 모든 명령어 - 실행파일, 소스파일, 매뉴얼 파일 - 의 위치가 나온다.)
  ```

**커맨드 옵션**

* `-b`: 바이너리 파일만 출력
* `-m`: 매뉴얼 파일만 출력
* `-s`: 소스 파일만 출력(보통은 없어서 출력되지 않음)



##### `chmod`

```bash
$ chmod [option] [mode] [filename || directory]
```

상단에 `ls`명령어와 관련하여 허가권과 관련있다.

각 권한들을 8진수로 변환하면 r=4, w=2, x=1 값이 되고, `-rw-r--r--`로 표시되는 부분은 부여된 권한을 나타내는데, 3가지 타입에 대한 권한을 나타낸다.

1~3번째가 소유자(owner)에 대한 권한, 4~6번째가 group에 대한 권한, 7~9번째가 others에 대한 권한이 된다.

아래의 예제는 user의 모든 권한을 부여하고, group과 others는 모든 권한을 제외한다.

```bash
$ chmod 700 test.txt
```

또, `+`, `-` 기호를 사용해서 특정 권한을 더하거나 뺄 수 있다.

ex) test.txt파일에 대해 group에 write권한 부여

```bash
$ chmod g+w test.txt
```

ex) test.txt 파일에 대해 others의 모든 권한 박탈

```bash
$ chmod o-rwx test.txt
```





출처: [[linux]리눅스 기본 명령어](https://itholic.github.io/linux-basic-command/), [리눅스의 소유권과 허가권](https://bkdevlog.netlify.app/posts/ownership-permission), [리눅스 grep 명령어 사용법](https://recipes4dev.tistory.com/157), [고슴이](https://sisiblog.tistory.com/19), [Unix, Linux에서 kill명령어로 안전하게 프로세스 종료 시키는 방법](https://www.lesstif.com/system-admin/unix-linux-kill-12943674.html), [[LINUX] chmod로 파일 권한 변경하기](https://gracefulprograming.tistory.com/111)