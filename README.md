
# Lab med ssh lösenord, nycklar och tvåfaktor autentisering

I den här labben ska ni få testa olika sätt att logga in remote på en annan dator  med hjälp av [ssh](https://help.ubuntu.com/community/SSH)


## Installera och bygg maskinen

Vi kan behöva ändra hostname på era virtuella maskiner så att det är lättare att urskilja vad som är vad, det finns en plugin för det, installera denna med

	$ vagrant plugin install vagrant-hostmanager

Nu startar vi. Ladda ner projektet till er labfolder.

	git 

cd in till labben.

börja med att öppna Vagrantfilen,  hitta raden där det står
 
	 config.vm.hostname = "level42" 

ändra det till ett coolt personligt maskin namn


Nu kan ni bygga maskinen med 

	$ vagrant up

Logga in med

	$ vagrant ssh

## lägg till en användare och logga in med lösenord

börja med att kolla vilken  publik ip adress du har fått

	$ ifconfig eth1

skriv ner ip adressen och spara till senare

	$ sudo adduser <username> 

Logga ut och lämna servern med exit. Nu kan du logga in med  från din egen eller någon annans dator. Testa det.
Byt ut `<username>`  och `<public ip>`  mot riktiga värden

	$ ssh <username>@<public ip>



## Använd en nyckelbaserad autentisering

I den här delen ska vi använda en nyckelbaserad autentisering med en privat och en publik nyckel. Vi ska titta på det mer sen, men är någon nyfiken finns en wikipedia artikel [här ](https://en.wikipedia.org/wiki/Public-key_cryptography)

Först måste ni generara nycklar, det gör ni med följande kommando.

	$ ssh-keygen -t rsa

Förhoppningvis får ni följande resultat

	Generating public/private rsa key pair.
	Enter file in which to save the key (/home/<usernam>/.ssh/id_rsa): 

Tryck enter för standardvärdena

	Enter passphrase (empty for no passphrase): 

och skippa lösenord för filen

Nu har ni skapat två nycklar som sparats i ~/.ssh

Den privata nyckeln id_rsa, ska ni vara rädd om, det är nyckeln som ni använder er för att verifiera er. 
Den publika nyckeln id_rsa.pub är den publika och ska skickas till den som ska verifiera att ni är ni.

Vi kopierar över den till vår virtuella maskin

	$ ssh-copy-id <username>@<public ip>

Nu kan du logga in utan att behöva ange lösenord. Byt ut `<username>`  och `<public ip>`  mot riktiga värden

	$ ssh <username>@<public ip>

Om du vill logga in från en annan dator än den du skapade nycklarna på behöver du ta med dig dina nycklar, dom finns i ~/.ssh



##  Två faktor autentisering



> Written with [StackEdit](https://stackedit.io/).

