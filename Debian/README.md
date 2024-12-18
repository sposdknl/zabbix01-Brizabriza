# Instalace Zabbix serveru a následný monitoring webu sposdk

1. Úvod
Pro tuto práci jsem si zvolil automatizovanou instalaci Zabbix serveru.
Vytvořil jsem script, pomocí něhož se vše nainstaluje tak, jak má.
Měl jsem na výběr mezi Ansible a bash.
V tomto případě jsem zvolil "hádám" tu jednodušší možnost a to bash.
Nikdy jsem s ním nepracoval, takže jsem rád, že jsem nabyl nějakých nových zkušeností.

2. Vagrantfile
Začal jsem samotným vagrantfilem.
Nastavil jsem zde základní parametry jako velikost RAM, počet cpu atd.
Vybral jsem si linuxovou distribuci Debian, tudíž jsem ve vagrantfilu nastavil image name jako nejnovější verzi debianu.
Nesmím opomenout porty 22 a 80.
Do kategorie shell jsem pak umístil cestu k mému skriptu, aby se při instalaci stroje automaticky instaloval i zabbix server a aby se skript nemusel spouštět manuálně, ale o tom až později.

3. Skript zabbix_server.sh
Je to dělané pomocí bash, tudíž je nutnost na začátku #!/bin/bash.
Je zde instalace a konfigurace spousty věcí to je, ale popsané v samotném skriptu.
Například instalace MySQL serveru (MariaDB), instalace Zabbix serveru, konfigurace Zabbix serveru a další.
Zde jsem si chtěl ušetřit práci, čas a především úsilí a chtěl jsem příkazy psát pouze přes poznámkový blok.
To se mi vymstilo, jelikož vždy když jsem dal vagrant up, tak se mi objevilo asi "milion errorů" na každém řádku.
Když jsem příkazy psal manuálně do virtuálního stroje, vše šlapalo jak hodinky.
Tak jsem došel k analýze mého problému.
Celý kód jsem psal do poznámkového bloku ve Windows a Microsoft vkládá na konec řádku textového souboru znaky CRLF narozdíl od linuxu, který vkládá LF.
Abych tento problém obešel, editoval jsem skript v editoru PSpad, který má funkci zápisu ve formátu linux. (viz. obrázek č.1)
Po vyřešení problému probíhala dlouhá instalace cca 10 minut.
Po ní se nám nainstaloval zabbix server.

4. Zabbix server
Zadal jsem do webového prohlížeče adresu http://localhost:8080/zabbix/.
Ručně jsem nakonfiguroval připojení k databázi, kde jsem změnil pouze uživatele a heslo. (viz obrázek č.2)
Svůj Zabbix server jsem si pojmenoval brizik. (viz obrázek č.3)
V zabbix.conf.php můžeme vidět, že se mi název serveru propsal. (viz obrázek č.4)

5. Monitoring sposdk.cz
Ze souboru sposdk.cz_hosts.yaml jsem vytáhl nejdůležitější informace, pomocí níž jsem vytvořil nového hosta. (viz obrázek č.5)
Můžeme vidět, že agent komunikuje se serverem. (viz obrázek č.6)
Zde vidíme dva hosty, jednoho jsem si manuálně vytvořil a druhý se automaticky vytvořil při instalaci zabbix serveru. (viz obrázek č.7)

6. Závěr
S tímto projektem jsem strávil spoustu krásných chvil.
Přiučil jsem se nových praktik a dozvěděl se přehršel všelijakých možných nových informací. 




