# vision project

## Install DHT11 sensor
```
git clone https://github.com/adafruit/Adafruit_Python_DHT.git
cd Adafruit_Python_DHT
sudo python setup.py install
cd examples
cd Adafruit_Python_DHT/examples
```
- run
```
python AdafruitDHT.py 11 4
```

```
curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -
```
```
echo "deb https://dl.bintray.com/fg2it/deb stretch main" | sudo tee -a / etc/apt/sources.list.d/influxdb.list
```

```
sudo apt update
sudo apt install influxdb
```

```
sudo service influxdb start
```
