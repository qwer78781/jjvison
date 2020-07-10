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
 ```
   1 #!/usr/bin/python
  2 
  3 import time
  4 import RPi.GPIO as GPIO
  5 import request, json
  6 from influxdb import InfluxDBClient as influxdb
  7 
  8 GPIO.setmode(GPIO.BCM)
  9 GPIO.setup(4, GPIO.IN)
 10 
 11 def interrupt_fired(channel):
 12     print("interrupt Fired")
 13     a = 1
 14     print(a)
 15 GPIO.add_event_detect(4, GPIO.FALLING, callback=interrupt_fired)
 16 
 17 while(True):
 18      time.sleep(1)
 19      a = 0
 20      data = [{
 21          'measurement' : 'pir',
 22          'tags':{
 23              'VisionUni' : '2410',
 24              },
 25          'fields':{
 26              'pir' : a,
 27              }
 28          }]
 29      client = None
 30      try:
 31          client = influxdb('localhost',8086,'root','root','pir')
 32      except Exception as e:
 33          print "Exception" + str(e)
 34      if client is not None:
 35          try:
 36              client.write_points(data)
 37          except Exception as e:
 38              print "Exception write " + str(e)
 39          finally:
 40              client.close()
 41      print("running influxdb OK")
```

```
1 #!/usr/bin/python
  2 
  3 import time
  4 import RPi.GPIO as GPIO
  5 import requests, json
  6 from influxdb import InfluxDBClient as influxdb
  7 
  8 GPIO.setmode(GPIO.BCM)
  9 GPIO.setup(4, GPIO.IN)
 10 
 11 def interrupt_fired(channel):
 12     print("interrupt Fired")
 13     a = 5
 14     print(a)
 15 GPIO.add_event_detect(4, GPIO.FALLING, callback=interrupt_fired)
 16 
 17 while(True):
 18      time.sleep(1)
 19      a = 1
 20      data = [{
 21          'measurement' : 'pir',
 22          'tags':{
 23              'VisionUni' : '2410',
 24              },
 25          'fields':{
 26              'pir' : a,
 27              }
 28          }]
 29      client = None
 30      try:
 31          client = influxdb('localhost',8086,'root','root','pir')
 32      except Exception as e:
 33          print "Exception" + str(e)
 34      if client is not None:
 35          try:
 36              client.write_points(data)
 37          except Exception as e:
 38              print "Exception write " + str(e)
 39          finally:
 40              client.close()
 41      print("running influxdb OK")
 42 
```

```
  1 #!/usr/bin/python
  2 
  3 import sys, serial, time
  4 
  5 comm = '/dev/ttyAMA0'
  6 baudrate = 38400
  7 
  8 device = serial.Serial(comm, baudrate, timeout = 5)
  9 print(device)
 10 
 11 while(True):
 12     try:
 13         rcvBuf = bytearray()
 14         device.reset_input_buffer()
 15         rcvBuf = device.read_until(size=12)
 16         print rcvBuf
 17     except Exception as e:
 18         print("Exception read") + str(e)
 19 
 20         time.sleep(5)
                           
```
