## PHP & MySQL Environment Setup with Docker

Docker နဲ့ PHP + MySQL setup လုပ်နည်းလေးကို tutorial ရေးသွားမှာဖြစ်ပါတယ်။ Docker ကိုမသိသေးတဲ့သူပဲဖြစ်ဖြစ်၊ 
သိပြီး PHP Environment setup လိုအပ်လာရင်ပဲဖြစ်ဖြစ်အသုံးဝင်မယ်လို့ထင်ပါတယ်။ 
မသိသေးတဲ့သူအတွက်ဆို အစပြုဖို့လမ်းကြောင်းကောင်းတစ်ခုရသွားမယ်ထင်ပါတယ်။

### Docker ဘာလို့သုံး ?

Docker မသုံးခင်က PHP အတွက် environment setup လုပ်တော့မယ်ဆို XAMPP တို့လို all in one package တွေသုံးတယ်။ ဒါမှမဟုတ် လိုအပ်တဲ့ software တွေကို manual သွင်းတယ်။ နည်းနည်းအလုပ်ရှုပ်တယ်၊ သွင်းထားတဲ့ software version တစ်ခုပဲသုံးလို့ရမယ်၊ ဥပမာ PHP 7 သွင်းထားတယ်ဆို 7 ပဲသုံးလို့ရမယ်၊ 8 သွင်းမယ်ဆို manual installation/update ပြန်လုပ်ဖို့လိုမယ်။

Docker သုံးရင်ဒါတွေဖြေရှင်းနိုင်မယ်။ အကြမ်းဖျင်း intro ဝင်ရမယ်ဆို docker ဆိုတာ development လုပ်ဖို့အတွက် virtual environments တွေဖန်တီးပေးတယ်၊ environments တိုင်းကလည်း isolate (တစ်ခုပေါ်တစ်ခုမမှီခို) ဖြစ်စေတဲ့ PaaS (Platform as a service) တစ်ခုပဲဖြစ်စပါတယ်။ 

Docker မှာ image တွေရှိတယ်၊ image ဆိုတာကတော့ ပြောင်းလဲလို့မရတဲ့(immutable/read-only) ဖြစ်တဲ့ pre-defined source code တွေ၊ libraries တွေကိုဆိုလိုတာဖြစ်ပါတယ်။

Image တွေက template လိုပုံစံတွေဖြစ်တဲ့အတွက်သူ့ချည်းပဲ run လို့မရဘူး။ ဒါကြောင့်ဒီ Image တွေကို base လုပ်ပြီးတော့ container ဆိုတာကိုဖန်တီးလို့ရပါတယ်။ 
Container ဆိုတာကိုဖန်တီးလိုက်ခြင်းအားဖြင့် immutable ဖြစ်တဲ့ Images တွေအပေါ်ကို write လုပ်လို့ရမယ့် layer တစ်ခုရလာပါတယ်။ ဒီ container တွေက ကိုယ့်ရဲ့ OS ပေါ်မှာမှီခိုခြင်းမရှိသလို container အချင်းချင်းလည်းမှီခိုခြင်းမရှိဘဲ run နိုင်တဲ့ virtual environment တွေပဲဖြစ်ပါတယ်၊ ဒါကြောင့်မို့ docker container တွေကို isolated virtual run-time environment လို့ခေါ်ခြင်းဖြစ်ပါတယ်။

ဥပမာအခု tutorial မှာဆို ကျနော်တို့ container တစ်ခုဖန်တီးမယ်၊ container ထဲမှာ PHP, MySQL, Web Server softwares (docker images)တွေပါမယ်။ ကိုယ့်ရဲ့PC/server ပေါ်မှာအဲ့လိုမျိုး container တွေ တစ်ခုထက်မက လိုသလိုဆောက်ပြီး run သွားလို့ရတယ်။ ကိုယ်သုံးနေတဲ့ OS ပေါ်မှာတင် Project တစ်ခုနဲ့တစ်ခုမှာမတူတဲ့ software version တွေသွင်းပြီးအသုံးပြုနိုင်မယ်။ Project ကို move/deploy လုပ်ရတာလွယ်သွားမယ်။

ဥပမာ server ပေါ်တင်တော့မယ်ဆိုအရင်ကလို software တွေကို manual လိုက်သွင်းနေစရာမလိုတော့ဘူး။ docker folder တင်လိုက်တာနဲ့ကိုယ်သတ်မှတ်ထားတဲ့ environment configuration setting တွေအတိုင်း installation လုပ်သွားမယ်။ server ပေါ်မှာသွင်းပြီးသားတွေရှိရင်လည်း container ပေါ် tie ဖြစ်ပြီး installation လုပ်တဲ့အတွက် conflict ဖြစ်စရာမရှိတော့ဘူး။ local မှာအလုပ်လုပ်တယ်၊ server မှာအလုပ်မလုပ်ဘူးဆိုတဲ့အရာတွေကိုဖြေရှင်းသွားနိုင်မယ်။ 

Environment setup အပိုင်းကိုဆက်သွားမှာဖြစ်လို့ Docker ကိုအကြမ်းဖျင်းပဲရေးသွားနိုင်တာ နားလည်ပေးပါဗျ။ Docker အကြောင်းနားမလည်သေးဘူးဆို မိမိဘာသာတီးမိခေါက်မိရှိလောက်အောင် စာထပ်ဖတ်ဖို့အကြံပေးချင်ပါတယ်။

Prerequisites အနေနဲ့ကျနော်တို့စက်ထဲမှာ docker installation လုပ်ထားဖို့လိုပါတယ်။ OS ပေါ်မူတည်ပြီး configuration တွေကွဲပြားနိုင်တာရှိတဲ့အတွက် official documentation ကိုကြည့်ပြီး installation လုပ်ပေးဖို့အကြံပေးချင်ပါတယ်။
https://docs.docker.com/get-docker/

အခု tutorial မှာတော့ PHP, MySQL နဲ့ web server အဖြစ် NGINX ကိုသုံးပြီးတော့ setup လုပ်ပြသွားမှာဖြစ်ပါတယ်။ အရင်ဆုံးအဲ့ဒီ services/images တွေကို create လုပ်ဖို့အတွက် yml configuration file တစ်ခုစဆောက်ပါမယ်။ 

folder/docker-compose.yml
```
version: '3'
services:
    web-server:
        image: nginx:latest
        ports:
            - "80:80"
```

Docker-compose yml specification အတွက် v3 ကိုအသုံးပြုပါမယ်။ version နဲ့ပတ်သတ်ပြီးအသေးစိတ်ကိုအောက်က official link မှာကြည့်နိုင်ပါတယ်။
https://docs.docker.com/compose/compose-file/compose-file-v3/

-	services ဆိုတဲ့ key အောက်မှာကျနော်တို့လိုချင်တဲ့ service နဲ့ image တွေ define လုပ်လို့ရပါတယ်။ 
-	ပထမဦးဆုံး web-server စဆောက်ပါမယ်။ web-server အောက်မှာတော့ NGINX image ကိုလှမ်းခေါ်သုံးပါမယ်။ (You can change `web-server` name to anything you want)
-	latest နေရာမှာကိုယ်လိုချင်တဲ့ version ကို define လုပ်နိုင်ပါတယ်။
-	yml file တွေက nesting structure နဲ့သွားတဲ့အတွက် file indentation ကိုဂရုပြုရပါမယ်။
-	web server အတွက် port 80 ကိုအသုံးပြုထားပေမယ့် ကိုယ့်စက်ထဲမှာတစ်ခြားသော software တွေက same port ကိုသုံးထားတာရှိရင်တော့ပိတ်ထားပေးဖို့လိုပါတယ်။

### Running the web server
Terminal ဖွင့်၊ project folder ထဲကိုဝင်ပြီးတော့ docker-compose.yml ရှိတဲ့ path မှာပဲ `docker-compose up` ရိုက်လိုက်မယ်ဆို NGINX ကို installation လုပ်ပြီးတော့ connect လုပ်သွားမှာဖြစ်ပါတယ်။ result ကိုတော့ http://127.0.0.1 မှာကြည့်နိုင်ပါတယ်။
NGINX ရဲ့ default page ကိုမြင်ရမှာဖြစ်ပါတယ်။

### Adding file volumes
Web server run ပြီးပြီဆိုတော့ web server အတွက်လိုအပ်တဲ့ configuration တွေလုပ်ဖို့အတွက်၊ project အတွက်လိုအပ်တဲ့ files တွေအတွက် volumes နှစ်ခုထည့်ပါမယ်။

docker-compose.yml
```
version: '3'
services:
    web-server:
        image: nginx:latest
        ports:
            - "80:80"
        volumes:
            - ./nginx.conf:/etc/nginx/conf.d/nginx.conf
            - ./src:/src
```

nginx.conf နဲ့ src folder ကို docker-compose.yml နဲ့ တစ်တန်းတည်းမှာဆောက်လိုက်ပါမယ်။ colon(:) ဘယ်ဘက်ခြမ်းမှာရှိတာကကျနော်တို့ရဲ့ volumes ဖြစ်ပြီးတော့ ညာဘက်ခြမ်းကတော့ container ဘက်ကဖြစ်ပါတယ်။ volumes က changes မှန်သမျှက ညာဘက်ခြမ်းက container မှာလည်းသက်ရောက်မှာဖြစ်ပါတယ်။

nginx.conf 
```
server {
    listen 80 default_server;
    root /src/public;
} 
```

nginx.conf ထဲမှာ web server နဲ့ပတ်သတ်ပြီး configuration တွေ define လုပ်သွားမှာဖြစ်ပါတယ်။ လောလောဆယ်မှာတော့ /src/public ကို document root အဖြစ် serve လုပ်ထားပေးထားပါတယ်။

src/public/index.html
```
HELLO DOCKER
```
src အောက်မှာ public folder ဆောက်ပြီးတော့အထဲမှာ index.html file ကိုထပ်ဆောက်ထားပါတယ်။

docker run ထားတာကို stop (ctrl + c) နဲ့ cancel လုပ်ပြီးတော့ လုပ်ပြီးတော့ docker-compose up ပြန် run မယ်ဆို HTML code ရဲ့ result ကိုမြင်ရမှာဖြစ်ပါတယ်။ ဒါဆိုရင် file volumes တွေကအလုပ်လုပ်နေပြီဖြစ်ပါတယ်။

### PHP Installation 

PHP အတွက် service တစ်ခုထပ်ထည့်ပါမယ်။

docker-compose.yml 
```
version: '3'
services:
    web-server:
        image: nginx:latest
        ports:
            - "80:80"
        volumes:
            - ./nginx.conf:/etc/nginx/conf.d/nginx.conf
            - ./src:/src
    php:
        build:
            context: .
            dockerfile: PHP.Dockerfile
        volumes:
            - ./src:/src
```

PHP service တစ်ခုထပ်ထည့်ထားပါတယ်။ NGINX လိုမျိုး image entry နဲ့ဆောက်သွားလို့ရပေမယ့် MySQL အတွက် php-extension တွေထပ်သွင်းစရာလိုတဲ့အတွက် PHP dockerfile သီးသန့်ဆောက်ပြီး build entry နဲ့သုံးသွားပါမယ်။ context ကတော့ PHP အတွက် docker configuration file ရှိမယ့် path ပါ။ yml file နဲ့တစ်တန်းတည်းရှိမှာဖြစ်တဲ့အတွက် `.` ပဲထည့်လိုက်ပါမယ်။ PHP files တွေကိုလည်း src volumes ကနေ access လှမ်းလုပ်ရမှာဖြစ်တဲ့အတွက် src volumes ကိုလည်း mount လုပ်ထားပါမယ်။

PHP.Dockerfile
```
FROM php:fpm

RUN docker-php-ext-install pdo pdo_mysql
```

MySQL အတွက် pdo_mysql extension သွင်းထားပါတာ်။ FROM php:fpm ဆိုတာကတော့ php:fpm image ကို base လုပ်မယ်လို့ဆိုလိုတာပါ။ တစ်ခြားသောလိုအပ်တဲ့ extension တွေကိုလည်း ဒီနေရာမှာ installation လုပ်သွားလို့ရပါတယ်။

nginx.conf
PHP files တွေကို run နိုင်ဖို့အတွက် nginx configuration ကိုလည်းပြင်ပေးဖို့လိုပါတယ်။
```
server {
    listen 80 default_server;
    root /src/public;

    index index.php index.html index.htm;

    location ~ \.php$ {
        fastcgi_pass php:9000;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;     
    }
} 
```

index ကိုတော့ index.php ကိုဦးစားပေးပြီး run ဖို့ setting လုပ်ထားမယ်။ Location ကတော့ nginx ကို .php extension နဲ့ files တွေကို fastcgi_pass PHP service ကိုသုံးပြီး run ဖို့လုပ်ပါမယ်။

src/public/index.php
index.php ကိုဖန်တီးထားပါမယ်။
```
<?php
echo phpinfo();
```

Server ကို restart (stop (ctrl + c) and docker-compose up) လုပ်မယ်ဆိုရင်တော့ PHP info page ကိုမြင်ရမှာဖြစ်ပါတယ်။ PHP.Dockerfile ကနေတစ်ဆင့်သွင်းထားတဲ့ pdo_mysql extension ကိုလည်းမြင်နိုင်မှာဖြစ်ပါတယ်။ အကယ်လို့ PHP.Dockerfile ကိုနောက်ထပ် changes တွေလုပ်ခဲ့မယ်ဆိုရင်တော့ docker-compose up မလုပ်ခင် docker-compose build အရင်ထပ်လုပ်ပေးဖို့လိုအပ်ပါတယ်။



### MySQL 

docker-compose.yml
```
version: '3'
services:
    web-server:
        image: nginx:latest
        ports:
            - "80:80"
        volumes:
            - ./nginx.conf:/etc/nginx/conf.d/nginx.conf
            - ./src:/src
    php:
        build:
            context: .
            dockerfile: PHP.Dockerfile
        volumes:
            - ./src:/src
    mysql:
      image: mysql
      volumes:
        - mysqldata:/var/lib/mysql
      environment:
        - MYSQL_ROOT_PASSWORD=secret
        - MYSQL_DATABASE=dock-php
        - MYSQL_USER=root
        - MYSQL_PASSWORD=secret
      ports:
            - 3306:3306
      
volumes:
    mysqldata: {}
```
နောက်ဆုံး step အနေနဲ့ MySQL ကို installation လုပ်ပါမယ်။ MySQL အတွက် image အသစ်တစ်ခုထပ်ထည့်ပါမယ်။ volumes အတွက်ကိုတော့ Local FS မသုံးဘဲ volumes သီးသန့်ဆောက်ထားပါတယ်၊ environment တစ်ခုနဲ့တစ်ခုအပြောင်းအလဲမှာ data တွေ overwrite မဖြစ်သွားစေဖို့ပါ။ ကျန်တာတွေကတော့ပုံမှန်အတိုင်းအားလုံးသိတဲ့ MySQL setting တွေပါပဲ။


PHP Code ဘက်မှာလည်း MySQL နဲ့ connect ဖြစ်လားမဖြစ်လားသိစေနိုင်မယ့် code တစ်ချို့update လုပ်လိုက်ပါမယ်။
index.php
```
<?php 

try {
	$conn = new PDO("mysql:host=mysql;dbname=dock-php", 'root', 'secret');
	// set the PDO error mode to exception
	$conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
	echo "Connected successfully";
} catch(PDOException $e) {
	echo "Connection failed: " . $e->getMessage();
}
```
Server restart ချပြီး Connected successfully လို့ပြပြီဆိုရင်တော့ setting တွေအားလုံးမှန်ကန်စွာအလုပ်လုပ်ပြီဆိုတာသိနိုင်ပြီဖြစ်ပါတယ်။
ဒီမှာတင်ပဲ conclude လုပ်ပါရစေ။ တစ်ခြားသော phpmyadmin တို့ဘာတို့သွင်းချင်တယ်ဆိုရင်လည်း ကိုယ့်ဘာသာ image လေးရှာပြီး challenge အနေနဲ့သွင်းကြည့်ပေါ့။ docker နဲ့ PHP environment setup လုပ်ဖို့ရှာနေသူပဲဖြစ်ဖြစ်၊ docker ကို getting started လုပ်ဖို့စဉ်းစားနေသူပဲဖြစ်ဖြစ် အသုံးဝင်သွားမယ်လို့ထင်ပါတယ်။

ကျေးဇူးတင်ပါတယ်။

