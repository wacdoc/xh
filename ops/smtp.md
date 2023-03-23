# Yakha eyakho iseva yokuthumela imeyile yeSMTP

## intshayelelo

I-SMTP inokuthenga ngokuthe ngqo iinkonzo kubathengisi belifu, abanje:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali cloud email push](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Unokwakha eyakho iseva yemeyile-ukuthumela okungenamkhawulo, ixabiso eliphantsi lilonke.

Ngezantsi, sibonisa inyathelo ngenyathelo indlela yokwakha eyethu iseva yemeyile.

## Ukukhetha iseva

Umncedisi we-SMTP ozibambe ngokwakhe ufuna i-IP yoluntu enezibuko 25, 456, kunye ne-587 evulekile.

Amafu oluntu asetyenziswa ngokuqhelekileyo avale la mazibuko ngokungagqibekanga, kwaye kunokwenzeka ukuwavula ngokukhupha umyalelo womsebenzi, kodwa kunzima kakhulu emva koko.

Ndincoma ukuthenga kwinginginya enala mazibuko avulekileyo kwaye ixhasa ukuseta amagama esizinda esingasemva.

Apha, ndincoma [Contabo](https://contabo.com) .

I-Contabo ngumboneleli wokubamba osekelwe eMunich, eJamani, esekwe kwi-2003 ngamaxabiso akhuphisana kakhulu.

Ukuba ukhetha i-Euro njengemali yokuthenga, ixabiso liya kuba lincinci (iseva enememori ye-8GB kunye ne-4 CPUs ixabisa malunga ne-529 yuan ngonyaka, kwaye umrhumo wokuqala wokufakela ukhululekile unyaka omnye).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Xa ubeka iodolo, phawula `prefer AMD` , kwaye iseva ene-AMD CPU iya kuba nokusebenza okungcono.

Oku kulandelayo, ndiza kuthatha iVPS kaContabo njengomzekelo ukubonisa indlela yokwakha iseva yakho yeposi.

## Ubumbeko lwenkqubo ye-Ubuntu

Inkqubo yokusebenza apha ngu-Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Ukuba umncedisi kwi ssh ubonisa `Welcome to TinyCore 13!` (njengoko kubonisiwe kulo mfanekiso ungezantsi), kuthetha ukuba inkqubo ayikafakwa okwangoku. Nceda qhawula uqhagamshelwano lwe-ssh kwaye ulinde imizuzu embalwa ukuze ungene kwakhona.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Xa `Welcome to Ubuntu 22.04.1 LTS` ibonakala, ukuqaliswa kugqityiwe, kwaye ungaqhubeka nala manyathelo alandelayo.

### [Ngokhetho] Qalisa imeko-bume yophuhliso

Eli nyathelo liyakhethwa.

Ukwenzela lula, ndibeka ufakelo kunye noqwalaselo lwenkqubo ye-ubuntu software [kwi-github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Qalisa lo myalelo ulandelayo ukuyifaka ngonqakrazo olunye.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Abasebenzisi baseTshayina, nceda usebenzise lo myalelo ulandelayo endaweni yoko, kwaye ulwimi, indawo yexesha, njl.njl. ziya kumiselwa ngokuzenzekelayo.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### I-Contabo yenza i-IPV6

Vula i-IPV6 ukuze i-SMTP ikwazi nokuthumela ii-imeyile ngeedilesi ze-IPV6.

hlela `/etc/sysctl.conf`

Lungisa okanye wongeze le migca ilandelayo

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Landela [ngesifundo se-contabo: Ukongeza uqhagamshelo lwe-IPv6 kwiseva yakho](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Hlela `/etc/netplan/01-netcfg.yaml` , yongeza imigca embalwa njengoko kubonisiwe kumzobo ongezantsi (ifayile yoqwalaselo engagqibekanga yeContabo VPS sele inale migca, vele uyikhulule).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Emva koko `netplan apply` ukwenza ulungelelwaniso olulungisiweyo lusebenze.

Emva kokuba ubumbeko luphumelele, ungasebenzisa `curl 6.ipw.cn` ukujonga idilesi ye-ipv6 yenethiwekhi yakho yangaphandle.

## Cola uqwalaselo logcino lwe-op

```
git clone https://github.com/wactax/ops.soft.git
```

## Yenza isatifikethi sasimahla se-SSL segama lakho lesizinda

Ukuthumela imeyile kufuna isatifikethi se-SSL soguqulelo oluntsonkothileyo kunye nokusayina.

Sisebenzisa [i-acme.sh](https://github.com/acmesh-official/acme.sh) ukwenza izatifikethi.

i-acme.sh sisixhobo sokusayina sesatifikethi esivulelekileyo,

Ngenisa i-warehouse yoqwalaselo ops.soft, sebenzisa `./ssl.sh` , kunye nefolda ye `conf` iya kwenziwa **kulawulo oluphezulu** .

Fumana umboneleli wakho weDNS kwi [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , hlela `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Emva koko sebenzisa `./ssl.sh 123.com` ukwenza `123.com` kunye `*.123.com` izatifikethi zegama lakho lesizinda.

Ukuqhuba kokuqala kuya kufaka ngokuzenzekelayo [i-acme.sh](https://github.com/acmesh-official/acme.sh) kwaye yongeze umsebenzi ocwangcisiweyo wokuhlaziya ngokuzenzekelayo. Ungabona `crontab -l` , kukho umgca onjalo ngolu hlobo lulandelayo.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Umendo wesatifikethi esenziweyo yinto efana ne `/mnt/www/.acme.sh/123.com_ecc。`

Uhlaziyo lwesatifikethi luyakubiza `conf/reload/123.com.sh` iskripthi, uhlele esi script, unokongeza imiyalelo efana ne `nginx -s reload` ukulayisha kwakhona ukuhlaziya i-cache yesatifikethi sezicelo ezinxulumeneyo.

## Yakha iseva ye-SMTP nge-chasquid

[chasquid](https://github.com/albertito/chasquid) ngumthombo ovulekileyo we-SMTP umncedisi obhalwe ngolwimi lweGo.

Njengokuthatha indawo yeenkqubo zeseva yemeyile yamandulo ezifana nePostfix kunye neSendmail, i-chasquid ilula kwaye kulula ukuyisebenzisa, kwaye ikwalula kuphuhliso lwesibini.

Qhuba `./chasquid/init.sh 123.com` iya kufakwa ngokuzenzekelayo ngonqakrazo olunye (buyisela i-123.com ngegama lakho lesizinda sokuthumela).

## Qwalasela uMsayino we-imeyile we-DKIM

I-DKIM isetyenziselwa ukuthumela utyikityo lwe-imeyile ukuthintela iileta ekubeni ziphathwe njengogaxekile.

Emva kokuba umyalelo usebenze ngempumelelo, uya kucelwa ukuba usete irekhodi ye-DKIM (njengoko kubonisiwe ngezantsi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Yongeza nje irekhodi ye-TXT kwi-DNS yakho (njengoko kubonisiwe ngezantsi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Jonga ubume benkonzo kunye neelog

 `systemctl status chasquid` Jonga ubume benkonzo.

Ubume bokusebenza okuqhelekileyo njengoko kubonisiwe kumzobo ongezantsi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` okanye `journalctl -xeu chasquid` inokujonga ilog yempazamo.

## Buyisa ulungelelwaniso lwegama lesizinda

Igama lesizinda elibuyela umva kukuvumela idilesi ye-IP ukuba isonjululwe kwigama lesizinda elihambelanayo.

Ukuseta igama lesizinda esingasemva kunokuthintela ii-imeyile ukuba zichongwe njengogaxekile.

Xa i-imeyile ifunyenwe, umncedisi ofumanayo uya kwenza uhlalutyo lwegama le-domain elibuyela umva kwidilesi ye-IP yeseva yokuthumela ukuqinisekisa ukuba iseva yokuthumela inegama le-domain elibuyisela umva.

Ukuba iseva yokuthumela ayinalo igama le-domain ebuyela umva okanye ukuba igama le-domain elibuyela umva alihambelani nedilesi ye-IP yomncedisi wokuthumela, umncedisi ofumanayo unokubona i-imeyile njengogaxekile okanye uyale.

Ndwendwela [https://my.contabo.com/rdns](https://my.contabo.com/rdns) kwaye uqwalasele njengoko kubonisiwe ngezantsi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Emva kokumisela igama lesizinda elibuyela umva, khumbula ukuqwalasela isisombululo sangaphambili segama lesizinda ipv4 kunye ne-ipv6 kumncedisi.

## Hlela igama lomamkeli we chasquid.conf

Guqula `conf/chasquid/chasquid.conf` kwixabiso legama lesizinda esibuyela umva.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Emva koko sebenzisa `systemctl restart chasquid` ukuqala kwakhona inkonzo.

## Gcina i-conf kwindawo yokugcina i-git

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Umzekelo, ndigcina ifolda ye-conf kwinkqubo yam ye-github ngolu hlobo lulandelayo

Yenza indawo yokugcina yabucala kuqala

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Ngenisa i-directory ye-conf kwaye uyingenise kwindawo yokugcina impahla

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Yongeza umthumeli

baleka

```
chasquid-util user-add i@wac.tax
```

Ungongeza umthumeli

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Qinisekisa ukuba igama lokugqithisa libekwe ngokuchanekileyo

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Emva kokongeza umsebenzisi, `chasquid/domains/wac.tax/users` iya kuhlaziywa, khumbula ukuyingenisa kwindawo yokugcina impahla.

## I-DNS yongeza irekhodi ye-SPF

I-SPF (iSakhelo soMgaqo-nkqubo womThumeli) iteknoloji yokuqinisekisa i-imeyile esetyenziselwa ukukhusela ubuqhetseba be-imeyile.

Iqinisekisa isazisi somthumeli we-imeyile ngokujonga ukuba idilesi ye-IP yomthumeli ihambelana neerekhodi ze-DNS zegama lesizinda elibanga ukuba lilo, ukuthintela abakhohlisi ukuba bathumele ii-imeyile zomgunyathi.

Ukongeza iirekhodi ze-SPF kunokuthintela ii-imeyile ukuba zichongwe njengogaxekile kangangoko kunokwenzeka.

Ukuba iseva yegama lesizinda sakho ayiluxhasi uhlobo lwe-SPF, yongeza nje uhlobo lwerekhodi le-TXT.

Umzekelo, i-SPF `wac.tax` ihamba ngolu hlobo lulandelayo

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

I-SPF `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Qaphela ukuba ndiquka `include:_spf.google.com` apha, oku kungenxa yokuba ndiza kumisela `i@wac.tax` njengedilesi yokuthumela kwibhokisi yeposi kaGoogle kamva.

## DNS uqwalaselo DMARC

I-DMARC sisishunqulelo se (Domain-based Ungqinisiso lomyalezo, iNgxelo kunye nokuThobela).

Isetyenziselwa ukubamba ii-bounces ze-SPF (mhlawumbi zibangelwa ziimpazamo zoqwalaselo, okanye omnye umntu uzenza wena ukuthumela ugaxekile).

Yongeza irekhodi yeTXT `_dmarc` ,

Umxholo umi ngolu hlobo lulandelayo

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Intsingiselo yepharamitha nganye yile ilandelayo

### p (Umgaqo-nkqubo)

Ibonisa indlela yokusingatha ii-imeyile ezingaphumeleliyo kwi-SPF (iSakhelo soMgaqo-nkqubo womThumeli) okanye i-DKIM (i-DomainKeys Identified Mail) isiqinisekiso. IP parameter inokumiselwa kwelinye lamaxabiso amathathu:

* akukho: Akukho nyathelo lithathiweyo, sisiphumo soqinisekiso kuphela esibuyiselwa kumthumeli ngendlela yokunika ingxelo ye-imeyile.
* Uvalelo: Faka imeyile engakhange igqithise isiqinisekiso kwisiqulathi seefayili zespam, kodwa ayiyi kuyala imeyile ngqo.
* yala: Yala ngokuthe ngqo ii-imeyile ezisilelayo ekuqinisekiseni.

### fo (Ukhetho lokusilela)

Ichaza isixa solwazi olubuyiswe yindlela yokunika ingxelo. Isenokumiselwa kwelinye lala maxabiso alandelayo:

* 0: Ingxelo yokuqinisekisa iziphumo zayo yonke imiyalezo
* 1: Ingxelo kuphela yemiyalezo engaphumeleliyo ekuqinisekiseni
* d: Ingxelo kuphela yokusilela ukuqinisekiswa kwegama lesizinda
* s: xela kuphela iintsilelo zoqinisekiso lwe-SPF
* l: Xela kuphela ukungaphumeleli kokuqinisekiswa kwe-DKIM

### rua & ruf

* rua (Ingxelo ye-URI yeengxelo eziHlanganisiweyo): Idilesi ye-imeyile yokufumana iingxelo ezidityanisiweyo
* ruf (Ingxelo ye-URI yeengxelo zeForensic): idilesi ye-imeyile ukufumana iingxelo ezineenkcukacha

## Yongeza iirekhodi zeMX ukuthumela ii-imeyile kwiMeyile kaGoogle

Ngenxa yokuba andizange ndifumane ibhokisi yeposi yenkampani yasimahla exhasa iidilesi zendalo iphela (Catch-All, ingafumana naziphi na ii-imeyile ezithunyelwe kweli gama lesizinda, ngaphandle kwezithintelo kwizimaphambili), ndisebenzise i-chasquid ukuthumela zonke ii-imeyile kwibhokisi yeposi ye-Gmail.

**Ukuba unebhokisi yakho yeposi yeshishini elihlawulelwayo, nceda ungayiguquli i-MX kwaye utsibe eli nyathelo.**

Hlela `conf/chasquid/domains/wac.tax/aliases` , cwangcisa ugqithiso lwebhokisi yeposi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` Ibonisa zonke ii-imeyile, `i` sisimaphambili sedilesi ye-imeyile yomsebenzisi othumelayo owenziwe ngasentla. Ukudlulisa imeyile, umsebenzisi ngamnye ufuna ukongeza umgca.

Emva koko yongeza irekhodi ye-MX (ndikhomba ngokuthe ngqo kwidilesi yegama lesizinda esiphambeneyo apha, njengoko kuboniswe kumgca wokuqala kumfanekiso ongezantsi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Emva kokuba ulungelelwaniso lugqityiwe, ungasebenzisa ezinye iidilesi ze-imeyile ukuthumela ii-imeyile `i@wac.tax` kunye `any123@wac.tax` ukubona ukuba ungazifumana na ii-imeyile kwi-Gmail.

Ukuba akunjalo, khangela i-chasquid log ( `grep chasquid /var/log/syslog` ).

## Thumela i-imeyile ku-i@wac.tax ngeMeyile kaGoogle

Emva kokuba iMeyile kaGoogle ifumene le imeyile, bendinethemba lokuphendula `i@wac.tax` endaweni ye-i.wac.tax@gmail.com.

Ndwendwela [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) kwaye ucofe "Yongeza enye idilesi ye-imeyile".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Emva koko, faka ikhowudi yokuqinisekisa efunyenwe yi-imeyile ethunyelwe kuyo.

Ekugqibeleni, inokumiselwa njengedilesi yomthumeli engagqibekanga (kunye nokukhetha ukuphendula ngedilesi enye).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Ngale ndlela, sigqibe ukusekwa kweseva ye-imeyile ye-SMTP kwaye kwangaxeshanye sisebenzise i-imeyile kaGoogle ukuthumela nokufumana ii-imeyile.

## Thumela i-imeyile yovavanyo ukujonga ukuba ubumbeko luphumelele na

Faka i- `ops/chasquid`

Qhuba `direnv allow` ukufakela okuxhomekeke (i-direnv ifakiwe kwinkqubo yokuqalwa yesitshixo esinye kwaye ihuku yongezwe kwiqokobhe)

uze ubaleke

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Intsingiselo yeeparamitha ngolu hlobo lulandelayo

* umsebenzisi: igama lomsebenzisi le-SMTP
* ipasiwe: SMTP password
* ku: kumamkeli

Ungathumela i-imeyile yovavanyo.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Kuyacetyiswa ukuba usebenzise i-Gmail ukufumana ii-imeyile zovavanyo ukujonga ukuba ulungelelwaniso luphumelele na.

### Uguqulelo oluntsonkothileyo lwe-TLS

Njengoko kubonisiwe kulo mfanekiso ungezantsi, kukho esi sitshixo sincinci, nto leyo ethetha ukuba isatifikethi se-SSL senziwe sasebenza ngempumelelo.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Emva koko ucofe u-"Bonisa i-imeyile yoqobo"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### I-DKIM

Njengoko kubonisiwe kumzobo ongezantsi, iphepha le-imeyile lokuqala le-Gmail libonisa i-DKIM, okuthetha ukuba ubumbeko lwe-DKIM luphumelele.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Jonga i-Yamkelwe kwiheader ye-imeyile yoqobo, kwaye uyabona ukuba idilesi yomthumeli yi-IPV6, into ethetha ukuba i-IPV6 nayo iqwalaselwe ngempumelelo.
