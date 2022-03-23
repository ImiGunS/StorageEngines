# StorageEngines

## Activitat 1

- Indica quins són els storage engines que pots utilitzar i quins estan actius.

Mitjançant la comanda ``SHOW ENGINES``, podem saber tots els storage engines que suporta, i a la vegada saber quin està activat de forma predeterminada i altres característiques.

![image](https://user-images.githubusercontent.com/79653853/157505340-f1787a81-b9b7-4ee2-b548-8c8c03a1c48b.png)

Obtindrem un resultat com el següent, on podem veure que tenim InnoDB com a storage engine per defecte.

![image](https://user-images.githubusercontent.com/79653853/157505438-7e9310da-0ae7-4b5c-aac1-3fde00421226.png)

- Mostra com canviar l'storage engine per defecte a ``MyISAM``.

Podem canviar l’storage engine desde l’arxiu de configuració my.cnf o podem canviar l’storage engine per la sessió actual mitjançant una comanda SQL.

En el nostre cas, editarem l'arxiu de configuració my.cnf i afegirem la linea ``default-storage-engine = myisam``.

![image](https://user-images.githubusercontent.com/79653853/157506171-c69b2e5a-ce13-429f-a043-ac016fd01a09.png)

Com podem veure, després de reiniciar el servei, ha canviat el default storage engine al ``MyISAM``.

![image](https://user-images.githubusercontent.com/79653853/157506275-4e7f73cf-cb50-4714-8bf9-4d307029b9a5.png)

- Instal·la i activa MyRocks engine.

Instal·larem el MyRocks engine de la següent manera.

![image](https://user-images.githubusercontent.com/79653853/157506951-95ec7b72-2fd5-4a7e-8f63-fe511230abac.png)

![image](https://user-images.githubusercontent.com/79653853/157507289-68c2f6dc-4f7a-4d53-84a4-b81d8de69f8b.png)

Ara fem Run al següent script per activar el MyRocks Engine.

![image](https://user-images.githubusercontent.com/79653853/157507465-9c38c8c8-a833-4795-b2bf-b5b82925f5cd.png)

Surt un error en la instal·lació

![image](https://user-images.githubusercontent.com/79653853/159785859-4454547a-3705-4f52-9aaa-e8fca94ecd45.png)

Reproduim la comanda de nou i surt això. Sembla que activa l'storage engine igualment.

![image](https://user-images.githubusercontent.com/79653853/157510547-b32731d6-1e16-45ce-9815-8816d03e092d.png)

![image](https://user-images.githubusercontent.com/79653853/157511052-b7e70dcb-8ca4-4ed2-a9ad-2af70bf44311.png)

- Importa SakilaDB com a taules MyISAM, fes els canvis necessaris.

Canviarem l'engine amb un replace i a continuació executarem l'script.

![image](https://user-images.githubusercontent.com/79653853/157512159-aba8c39a-17c4-4c9d-9dde-04a7ec633d99.png)

Com podem veure, les tables tenen l'storage engine MyISAM

![image](https://user-images.githubusercontent.com/79653853/157513037-1f9e9d85-3ee4-4643-a1aa-58f0f83bb434.png)


- Mira els arxius físics que ha creat, quant ocupa i quines són les seves extensions

Aquests arxius tenen tres extensions diferents, ``.MYD, .MYI i .sdi``

Sembla que els arxius s'empaqueten amb la mida de 4K que es va incrementant.

![image](https://user-images.githubusercontent.com/79653853/157517268-13612a35-9274-436d-b1f7-6b807d202e3a.png)

- Mostra que conté cada fitxer.

Els arxius ``.sdi`` contenen la configuració de les taules, com camps, data type, storage engines i altre informació.

![image](https://user-images.githubusercontent.com/79653853/157515436-36bf0dd3-6890-4838-8723-9e70ef169d35.png)

Els arxius ``MYD`` contenen el contigut o dades de les taules.

![image](https://user-images.githubusercontent.com/79653853/157518802-778db8d1-cb60-4569-a4f1-0b3419b458b4.png)

Els arxius `MYI` contenen la informació de la indexació de les taules.

![image](https://user-images.githubusercontent.com/79653853/157519667-fb4152dd-f0c1-4942-ba4c-d502c073a4a6.png)

- Torna a deixar InnoDB com a default storage engine.

![image](https://user-images.githubusercontent.com/79653853/157522077-8b2cc66e-51ea-4a1a-b126-a22dd9695040.png)

![image](https://user-images.githubusercontent.com/79653853/157521974-622f9323-b2ae-43c8-b045-a39c74ef11b9.png)

- Busca informació dels schemas de metadata i l'objectiu de cadascun d'ells. Posa un exemple d'ús.


- Posa un exemple de com es produeix un Deadlock.

Tindrem 2 clients, client A i client B. On client A començarà una transacció que farà un LOCK a nivell de registre, aleshores el client B començarà una transacció en la mateixa taula.

CLIENT A

![image](https://user-images.githubusercontent.com/79653853/158664500-63a57a72-5cd9-4a29-88c2-d54f18e79261.png)

CLIENT B

![image](https://user-images.githubusercontent.com/79653853/158664536-733e9152-e030-47cf-913b-839bcd691fda.png)

Mentres CLIENT B executa la comanda, el servidor retorna el següent error

![image](https://user-images.githubusercontent.com/79653853/158665358-29acbb72-fa5c-47f2-b7ad-bc9cd1d42034.png)


## Activitat 2

- Desactiva l’opció que ve per defecte de `innodb_file_per_table`

Per fer això, anirem a l'arxiu de configuració `my.cnf` i afegirem la següent linea.

![image](https://user-images.githubusercontent.com/79653853/158666155-c520d96d-a6d5-4672-ab0f-17f4cf7aa99e.png)

Això ha creat dos fitxers

![image](https://user-images.githubusercontent.com/79653853/158670028-073a8b06-f3f5-4997-b419-4d832afd8719.png)

On a `mysql.ibd` guarda tota les dades de la creació de tota la estructura de taules. I a `ibdata1` guarda tot el contingut de totes les taules.

MYSQL.IDB

![image](https://user-images.githubusercontent.com/79653853/158671465-817c9cce-0982-408f-95de-d0148b314993.png)

![image](https://user-images.githubusercontent.com/79653853/158671622-624e8d18-e5f8-4971-b769-10127804235e.png)


IBDATA1

![image](https://user-images.githubusercontent.com/79653853/158672732-3b2f02b6-f674-4c10-a71a-afb35aeebe54.png)


- Canvia la localització del tablespace per defecte a `/discs-mysql`

Creació directoris.

![image](https://user-images.githubusercontent.com/79653853/159730036-d0f362e3-bd0f-40f6-ad22-7ca44f2c38b1.png)

Primerament, apaguem el servei de `mysqld`.

![image](https://user-images.githubusercontent.com/79653853/159722983-2b04da66-dcfb-4289-9177-3a7752b8fa45.png)

Aleshores mentres el servei està apagat, canviarem la localització de la següent manera.

![image](https://user-images.githubusercontent.com/79653853/159735498-118ec5d2-d554-43a8-a8a2-79d306f30558.png)


![image](https://user-images.githubusercontent.com/79653853/159733478-809b92a2-718b-4f49-aafb-751245e2bc9c.png)

Ara, reiniciem el servei.

![image](https://user-images.githubusercontent.com/79653853/159724156-21e090c8-77b5-4744-8ba4-95d319889ea8.png)

## ACTIVITAT 7

- Util·lització de `CSV ENGINE`.

Abans de començar, crearem una base de dades i taules amb aquest engine.

![image](https://user-images.githubusercontent.com/79653853/159772514-cd8539f8-3407-4572-8090-7fcf85082ad9.png)

Com podem veure, ens ha generat uns arxius del tipus `.sdi`, `.csm`, `.csv`. On dins de l'arxiu CSV trobem el següent.

![image](https://user-images.githubusercontent.com/79653853/159772892-8d2ec566-c41e-4821-a9f7-c7e2d0990d0a.png)


## ACTIVITAT 8

- Ara documenta i poso un exemple de com utilitzar `MyRocks` com a engine.

Crearem la nostre Base de Dades

![image](https://user-images.githubusercontent.com/79653853/159775582-a847f6ab-14fb-41f6-811e-c1a257209ae7.png)

I comprovem que les noves taules estan utilitzan el MyRocks com a storage engine.

![image](https://user-images.githubusercontent.com/79653853/159776083-a12691bc-e121-401e-9190-c60635ae01ba.png)

Ara tenim els següents fitxers al nostre servidor, `nomDataBase` i `.rocksdb`.

Aquí tenim els arxius `.sdi` com els que ha hem vist anteriorment que contenen tota l'estructura de les taules.

![image](https://user-images.githubusercontent.com/79653853/159775979-36eeaccc-fdcc-4746-9317-16c70fa9c488.png)

En aquests arxius tenim la informació relacionada a les dades de les nostres taules, com les pròpies dades, indexs i altres.

![image](https://user-images.githubusercontent.com/79653853/159778640-733d158d-5286-4df2-bba4-784a28449e04.png)

![image](https://user-images.githubusercontent.com/79653853/159778713-bcf8ddd0-9d32-4c51-a979-e51cf512c91f.png)


Com podem veure, dins d'aquest fitxer `.log`, tenim totes les dades de les nostres taules.

![image](https://user-images.githubusercontent.com/79653853/159778300-e3f64a37-96cc-44c2-91e4-21df55ac6f78.png)

- Quina és la compressió per defecte?


