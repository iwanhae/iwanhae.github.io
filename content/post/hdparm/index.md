---
title: 리눅스, 하드디스크를 절전모드로 두기 (hdparm)
description: 구 블로그에서 가져옴
date: 2015-12-12
slug: introducing-hdparm
image: harddrive-icon-18.jpg
draft: false
categories:
    - Server
---
# 서론
![](/img_server/server_2.jpg)
![](/img_server/server_1.png)

요런식으로 서버를 운영하다보니 하드디스크 돌아가는 소리가 좀 거슬린다....
(특히나 소음 심하다는 Hitachi제 하드디스크....)

그래서 하드디스크를 절전상태로 두는 간단한 방법을 소개한다.

# 본론

일단 하드디스크를 절전상태로 들어가게해주는 **"hdparm"** 을 각자 알아서 설치해 주자. 대중적인 프로그램이니깐 기본적으로 설치되있는 경우도 꽤 많고 설치되있지 않다해도 apt나 yum으로 쉽게 설치 가능하다.

그 후 자신의 설정할 하드디스크의 경로를 알아내자. ROOT권한으로 `fdisk -ls`를 입력하면 현재 인식되있는 모든 저장장치의 정보를 볼수있다.

```bash
Disk /dev/sda: 320.1 GB, 320072933376 bytes
255 heads, 63 sectors/track, 38913 cylinders, total 625142448 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0xf83c5fbd

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1            2048   625141759   312569856   83  Linux
```

`/dev/sda1`은 파티션에 관한 정보고 여기서 필요한건 `/dev/sda`이다.


`/dev/sda`라는 정보를 알아냈으면 `hdparm -S 12 /dev/sda` 라 입력함으로서 1분후에 하드디스크가 꺼지게 할수 있다.

여기서 이상한 점은 `12`라는 숫자가 `1분`을 의미하는 것이다.

명확이 이런식으로 한 이유는 모르겠지만 12가 1분이 된 이유는 12에다 5를 곱하면 60이 되고 60초는 곧 1분이 되기 때문이다.

즉 `입력된 숫자의 5를 곱한값의 초` 후에 하드디스크가 절전모드로 들어간다는 것이다.

문제는 이것도 `240` `(240x5=1200=20분)`까지 얘기이고  이 이후부터는 `(입력된 숫자 - 240)*30분`후에 절전모드에 들어가게 된다. <br>요컨데 `241`을 입력하면 30분후 `242`를 입력하면 1시간뒤에 절전모드에 절전모드에 들어간다는 것이다.

근데 이것도 `251` `(251 = 5시간 30분)`까지의 얘기고

252는 21분
253은 하드디스크 제조사에서 권장하는 시간 (vendor-specific)
255는 21분 15초를 의미한다.

(254는 예비용으로 남겨둠)

#### 덤
hdparm이란 프로그램은 이름에서 예상되듯이 하드디스크의 각종 환경설정(parameter)값을 설정하는 프로그램이다.. 즉 여기서는 대기시간 말고도 여러가지 설정을 통해 하드디스크의 상태를 조절할수 있다.

예를들면

`sudo hdparm -I /dev/sda`를 통해 이 하드디스크가 사용할수있는 기능과 그외 하드디스크에 관련된 정보를 볼수있고

`sudo hdparm -tT /dev/sda`를 통해 하드디스크 그냥 읽기속도와 캐쉬를 이용한 읽기 속도를 비교해볼수도 있고

    /dev/sda:
     Timing cached reads:   1340 MB in  2.00 seconds = 670.39 MB/sec
     Timing buffered disk reads:  48 MB in  3.13 seconds =  15.35 MB/sec
    2009년 생산된 2.5인치 320기가짜리 하드디스크의 읽기속도는 15.35 MB/sec....ㅠㅠ


`sudo hdparm -M 128 /dev/sda`를 통해 하드디스크의 성능을 희생해 더 조용하게 만든다던가

`sudo hdparm -M 254 /dev/sda`를 통해 하드디스크의 성능을 최대로 뽑아냄과 동시에 엄청난 소음에 시달릴수도 있고

`sudo hdparm -f /dev/sda`나 `sudo hdparm -F /dev/sda`를 통해 읽기버퍼(전자)나 쓰기버퍼(후자)를 지워버릴수도 있다.

여러가지를 설정할수 있고 설정방법도 설정할려는 종류에 따라 모두 다르기때문에 자세한건 구글링 해보길 추천하며 글을 마친다.