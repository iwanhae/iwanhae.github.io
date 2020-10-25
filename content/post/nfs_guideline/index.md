---
title: 우분투, NFS 설정
description: 구 블로그에서 가져옴
date: 2016-01-03
slug: nfs_guideline
image: serverside-scripting-electronics-accessory-file-system-andrew-computer-icon.jpg
draft: false
categories:
    - Server
---
### 서버쪽

`apt-get install nfs-common nfs-kernel-server rpcbind`

설치 완료후

`/etc/exports`

파일을 수정

`/home/test/testfolder`

를 공유한다 가정할때

마지막줄에

`/home/test/testfolder 192.168.0.X(rw, no_root_squash, sync)`<br>
`[/경로] [허용할 IP주소. *은 모두허용](옵션들)`

와 같은 줄을 추가. (IP주소와 옵션은 붙어있다. 띄어쓰기하면 기본값으로 열리니 주의)

옵션은 다음과 같은 선택지가 있음

    ro : 읽기 전용
    rw : 읽기 및 쓰기 가능
    no_root_squash : 클라이언트쪽 root도 서버쪽 root와 같은권한가짐
    no_all_squash : root이외 모든사용자에대해 UID가 같으면 같은권한을가짐
    sync : 서버와 클라이언트사이에 sync를 맞춤
    insecure : 인증안되도 접속허가

설정해준뒤<br>
`service nfs-kernel-server restart`<br>
`service rpcbind restart`<br>
로 서버 재시작

### 클라이언트쪽

`apt-get install nfs-common`<br>
설치해준뒤

`mount -t nfs [주소]:[/경로] [/마운트 할장소]`<br>
`(ex : mount -t nfs blog.iwanhae.ga:/home/test/testfolder /home/anywhereyouwant)`

해주면 끗