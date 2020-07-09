# jjvison

<pre> jjvison </pre>

# InfluxDB Installation

## 1. Repository의 GPG key를 더하기
```
curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -
```

## 2. Repository를 더하기
```
echo "deb https://repos.influxdata.com/debian stretch stable" | sudo tee /etc/apt/sources.list.d/influxdb.list
```

## 3. 프로그램 설치
```
sudo apt update
sudo apt install influxdb
```

## 4. 프로그램 실행
```
sudo service influxdb start
```
## 5. 데이터베이스 만들기
```
>create database <데이터베이스이름>
```
```
확인 : show databases 
```
# Grafana Installation

## 1. Repository의 GPG key를 더하기
```
curl https://bintray.com/user/downloadSubjectPublicKey?username=bintray | sudo apt-key add -
```

## 2. Repository를 더하기
```
echo "deb https://dl.bintray.com/fg2it/deb stretch main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

## 3. 프로그램 설치
```
sudo apt update
sudo apt install grafana
```

## 4. 프로그램 실행
```
sudo service grafana-server start
```
## influxdb import with python
```
sudo pip install influxdb
```

```
### Git hub
 - Reposity down load
```
```
git clone https://github.com/qwer78781/jjvison
```

``` 
set nu   //Line number
set cindent  // C language indent
set ts=4   // tab size 4
if has("syntax")  //syntax on
 syntax on
endif
1 set nu
  2 set cindent
  3 set ts=4
  4 set softtabstop=4
  5 set bg=dark
  6 set expandtab
  7 let python_version_2 = 1
  8 let python_highlight_all = 1
  9 filetype indent plugin on
 10 if has("syntax")
 11     syntax on
 12 endif

```
```
  1 #!/usr/bin/python
  2 
  3 import time
  4 import RPi.GPIO as GPIO
  5 
  6 print GPIO.VERSION
  7 GPIO.setmode(GPIO.BCM)
  8 GPIO.setup(4, GPIO.IN)
  9 
 10 def interrupt_fired(channel):
 11     print("interrupt Fired")
 12     print(channel)
 13 
 14 GPIO.add_event_detect(4, GPIO.FALLING, callback=interrupt_fired)
 15 
 16 while(True):
 17     time.sleep(1)
 18     print("timer fired")
 ```
