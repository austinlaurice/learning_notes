#Django

##翻譯：
    python manage.py makemessages -a
    vim staffsite/staffsite/locale/zh/LC_MESSAGES/django.po
    python manage.py compilemessages

#Run OSS-Polis

##環境設定：
    git clone https://github.com/OpenNetworking/OSS-Polis.git
    git clone https://github.com/OpenNetworking/gcoin.git
    git clone https://github.com/OpenNetworking/oss-pool.git
    cd OSS-Polis
    virtualenv env --no-site-package
    . ./env/bin/activate
    pip install -e gcoin-rpc/
    cd oss-pool
    pip install -e aipu-client/ api_query/ issuerrpc/ monitormail/ storeclient/
    cd OSS-Polis
    pip install -r requirements.txt

#General settings

##firewall:

- 開port

    firewall-cmd --permanent --zone=public --add-port=8000/tcp

- 重啟防火牆

    systemctl restart firewalld


#Bitcoin:

- 開啟 bitcoind

    bitcoind -gcoin -gen -daemon

第一次打開的時候，他會叫你設定bitcoin.conf
    
    vim ~/.bitcoin/bitcoin.conf

rpcuser=<自己設定>
rpcpassword=<自己設定>
rpcport=<自己設定>
port=<自己設定>

-------------------------
example:

rpcuser=bitcoinrpc
rpcpassword=6SWniYid45ph9VFhVPepSzin2oJSsyepWiZKnJitZELD
rpcport=12345
port=55321

-------------------------
note: rpcport跟port不可以跟別人一樣。 如果你發現port有人用了就換一個


設定好bitcoin.conf

    bitcoind -gen -gcoin -daemon
應該就沒問題了
    
    試試看
    
    bitcoin-cli -gcoin getinfo

---------------------------------------------

mint color 0

    bitcoin-cli mint 1 0

-----------------------------------
wait 10 blocks

    bitcoin-cli -gcoin getbalance

看看有沒有
{
  “0”: 1.0000000,
}

--------------------------------------

    bitcoin-cli -gcoin listwalletaddress

隨便選一個喜歡的
for example,  
1AhZHrTHn95ug5813MAZ3F7qo7PENxg8CZ

-----------------------------------

送color 1 的license給 1AhZHrTHn95ug5813MAZ3F7qo7PENxg8CZ
    bitcoin-cli -gcoin sendlicensetoaddress 1AhZHrTHn95ug5813MAZ3F7qo7PENxg8CZ 1

等10個block 
1AhZHrTHn95ug5813MAZ3F7qo7PENxg8CZ就變成issuer，有權力可以mint coin

做到這邊就差不多了

----------------------------------------

#跑Abe

- Step 1: Create database for abe

* Enter mysql interactive shell(in 112.121.87.195)
    mysql -uroot -p
    password is empty

* Create a database for abe(都要分號)

    CREATE DATABASE <db_name>;
因為 112.121.87.195是共用的所以麻煩大家要開database都加個prefix

* Create a user and grant the user all privileges on abe database

    CREATE USER <user>;
    GRANT ALL ON <db_name>.* TO  <user>@'localhost' IDENTIFIED BY '<password>';

- Step 2: Install abe
 
* Download gcoin-abe repo from Github

 I have write a make file to download related repo from Github.
 So we can just run:
    cd Wallet-Server
    make initial_clean copy

 note: initial_clean will delete all file in packages directory
          copy will clone all related repo from Github           
* Enter virtualenv and pip install gcoin-abe
    cd Wallet-Server run:
    . ./env/bin/activate
    cd packages/gcoin-abe
    (env)pip install -r requirement.txt
    (env) pip install -e packages/gcoin-abe


- Step 3: create a config file

find a place 哪裏都可以
    vim abe.conf

content is as below:

----------------------------------------------
    default-loader = blkfile
    dbtype MySQLdb
    connect-args {"user":"<user>","db":"<db_name>","passwd":"<password>"} 
    upgrade
    port 8003
    host 0.0.0.0
    datadir += [{
        "dirname" : "/home/laurice/.bitcoin/gcoin",
        "chain" : "GCoin",
        "code3" : "GC"}]

----------------------------------------------
note: the parameter in connect-args need to be consistent with step 1
select a port that will not conflict with others, if you want to connect to abe from outside you need to open firewall
use your own dirname 

- Step 4: catch up (init)

    (env) python -m Abe.abe --config /path/to/abe.conf --commit-bytes 100000 --no-serve 

- Step 5: run abe

    (env) python -m Abe.abe --config /path/to/abe.conf 
