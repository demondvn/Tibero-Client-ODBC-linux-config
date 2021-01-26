# Tibero_linux_config
Config Tibero Client on Linux
```bash
tar xvzf tibero6-bin-FS07_CS_2005-linux64-186728-opt-tested.tar.gz 
cd /root/tibero6/
cd config/
export TB_HOME=/root/tibero6
cd $TB_HOME/config
./gen_tip.sh 

```
	
- :warning: **Update this file**
```bash
cd $TB_HOME/clients/config/
nano tbdsn.tbr
```

## [Config ODBC] 
```bash
 cd /etc/
 nano odbc.ini
```

 ```ini
 [ODBC Data Sources]
tibero = Tibero 6 ODBC driver
[ODBC]
Trace = 1
TraceFile = /home/tibero/iodbc/tmp/odbc.trace
[tibero]
Driver = TiberoDriver
Description = Tibero 6 ODBC Datasource
SID = tibero
User = UIDXXX
Password = PWDXXX
```
  
```bash
nano odbcinst.ini 
```
  
```ini
[TiberoDriver]
Description = Tibero Driver
Driver = /root/tibero6/client/lib/libtbodbc.so
```
## [Environment]
```bash
export ODBCINI=/etc/odbc.ini
export ODBCINSTINI=/etc/odbcinst.ini
export TB_HOME=/root/tibero6
export TB_SID=tibero
export LD_LIBRARY_PATH=$TB_HOME/lib:$TB_HOME/client/lib
export PATH=$TB_HOME/bin:$TB_HOME/client/bin:$PATH
export TB_NLS_LANG=UCS2
export TBCLI_WCHAR_TYPE=UCS2
```


## [Environment Service]
```bash
Environment=ODBCINI=/etc/odbc.ini
Environment=ODBCINSTINI=/etc/odbcinst.ini
Environment=TB_HOME=/root/tibero6
Environment=TB_SID=tibero
Environment=LD_LIBRARY_PATH=$TB_HOME/lib:$TB_HOME/client/lib
Environment=PATH=$TB_HOME/bin:$TB_HOME/client/bin:$PATH
Environment=TB_NLS_LANG=UCS2
Environment=TBCLI_WCHAR_TYPE=UCS2
```
## [Test]
```curl
curl -X POST "http://localhost:5000/api/Auth/Login" -H  "accept: */*" -H  "Content-Type: application/json-patch+json" -d "{\"username\":\"userXXX\",\"password\":\"passXXX\",\"macaddress\":\"string\"}"
```




## [Test with Tool]
```bash
iodbc-config --odbcini --odbcinstini
isql tibero UIDXXX PWDXXX
```
## Another
```bash
iodbctest "DSN=tibero;UID=UIDXXX;PWD=PWDXXX"

"DSN={tibero};UID={UIDXXX};PWD={PWDXXX}"

isql tibero UIDXXX PWDXXX

iusql tibero UIDXXX PWDXXX

iodbc-config --odbcini --odbcinstini
```

