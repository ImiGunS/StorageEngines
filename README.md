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

Podem obtenir totes les metadades mitjançant la comanda `SHOW TABLES FROM INFORMATION SCHEMA`, però com aquesta comanda és antiga (utilitzada comunment en versions anteriors a MySQL 5.0), utilitzarem `SELECT * FROM information_schema.tables` donat que mostra més dades.

![image](https://user-images.githubusercontent.com/79653853/162052249-7cbad0e1-f2a6-4501-afdf-0b461c6a080c.png)

![image](https://user-images.githubusercontent.com/79653853/162052311-06d3988b-6fb7-4516-a8ec-b810a0f856b9.png)

![image](https://user-images.githubusercontent.com/79653853/162052361-78c7915f-6683-46fb-bf03-6c88d09483b0.png)

No es poden explicar tantes metadades ja que a més de tenir l'information_schema, també es generen metadades de totes les base de dades creades al servidor, en aquest cas tenim un total de 338 metadades possibles a consultar.

![image](https://user-images.githubusercontent.com/79653853/162052726-a63d4345-324a-485c-8c26-3d23431625b3.png)

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

![image](https://user-images.githubusercontent.com/79653853/161594590-5c9d1ef6-5963-4142-b627-7d6f8ad1217f.png)

Primerament, apaguem el servei de `mysqld`.

![image](https://user-images.githubusercontent.com/79653853/159722983-2b04da66-dcfb-4289-9177-3a7752b8fa45.png)

Aleshores mentres el servei està apagat, canviarem la localització de la següent manera.

![image](https://user-images.githubusercontent.com/79653853/161097293-8f981910-aaf4-40a0-a33f-319245b6543e.png)

Ara, copiarem tot el contingut de `/var/lib/mysql/*` al nostre nou directori.

![image](https://user-images.githubusercontent.com/79653853/161595104-c50762c4-286a-40a5-b764-6d0191150668.png)

Abans de continuar, instal·larem la següent llibreria de manera que poguem continuar els següents passos de manera exitosa.

![image](https://user-images.githubusercontent.com/79653853/161595695-b8d2b380-6d4d-49f5-9db2-bd656c851c32.png)

Una vegada hem instal·lat això, procedirem mitjançant el semanage.

![image](https://user-images.githubusercontent.com/79653853/161595911-d03ea618-7f3b-455c-a5e8-2859a6cebacc.png)

![image](https://user-images.githubusercontent.com/79653853/161596003-d0e22d4c-7b12-4369-bad3-b794c4b7f9d8.png)

Ara, reiniciem el servei.

![image](https://user-images.githubusercontent.com/79653853/159724156-21e090c8-77b5-4744-8ba4-95d319889ea8.png)

Una vegada restablert el servei, entrarem al mysql i comprovarem ls canvis realitzats, en aquest cas, el `DATADIR` i el `innodb_data_file_path`.

![image](https://user-images.githubusercontent.com/79653853/161606671-9aa16888-55f9-4dab-82b9-2e18610ffe90.png)

![image](https://user-images.githubusercontent.com/79653853/161607970-69b71852-c1b2-439a-8fb5-b26d04375f1b.png)


Comprovarem l'espai dins dels disks mitjançant la comanda `du`. Veiem que de forma default tenen 10M com a mida inicial.

![image](https://user-images.githubusercontent.com/79653853/161607797-8c15dff6-7583-44a5-873b-686216d06b33.png)

Finalment hem aconseguit el que estàvem buscant.

## ACTIVITAT 3

- Configura el Percona Server de forma que cada taula generi el seu propi tablespace en una carpeta anomenada `tspaces`.

Abans de començar, habilitarem un altre cop el `innodb_file_per_table` que abans hem deshabilitat.

![image](https://user-images.githubusercontent.com/79653853/161612693-a7938388-8aea-493a-b318-ad48729eb4aa.png)

Ara, crearem la carpeta `tspaces` amb els permisos corresponents.

![image](https://user-images.githubusercontent.com/79653853/161612980-106a57bf-fdba-4643-b8ad-94064b800b2b.png)

Ara pararem el servei `mysqld` per continuar de forma segura.

![image](https://user-images.githubusercontent.com/79653853/161613839-82fec957-e5fd-4e13-873f-229c340c7f29.png)

Ara copiarem tots els fitxers dins de `/var/lib/mysql` a `/tspaces`.

![image](https://user-images.githubusercontent.com/79653853/161614066-979840e0-bec4-4900-b65d-78189b595f04.png)

Després de copiar tots els arxius, aplicarem el semanage en la nostre carpeta `tspaces` d'igual manera que hem fet abans.

![image](https://user-images.githubusercontent.com/79653853/161614475-14bb3d53-6ea7-41bd-b6fa-554dd8856055.png)

Seguidament, canviarem el `my.cnf` de la següent manera.

![image](https://user-images.githubusercontent.com/79653853/161615382-1916f3cd-cbe6-46cd-9900-1df1d78d9336.png)

Un cop feta la modificació, reiniciarem el servei mysqld.

![image](https://user-images.githubusercontent.com/79653853/161615428-6473080e-f86e-4528-9b38-605822293c79.png)

Finalment, comprovarem el datadir mitjançant una consulta mysql.

![image](https://user-images.githubusercontent.com/79653853/161615605-342be837-98aa-49ca-a07d-6258b6f2237a.png)

## ACTIVITAT 4

- Crea un tablespace `ts1` situat en `/discs-mysql/disk1` i col·loca les taules actor, address i category de Sakila DB.

Abans de fer res, ens assegurem que tenim el `innodb_file_per_table=ON`.

![image](https://user-images.githubusercontent.com/79653853/161794244-7155a426-64b0-4ba8-bc85-c59eb4ddc594.png)

Ara mitjançant comandes MySQL crearem un nou tablespace i canviarem el tablespace de les taules abans anomenades.

![image](https://user-images.githubusercontent.com/79653853/161796340-b7e142cf-f6fb-44c4-a932-6e1938f55951.png)

Comprovarem el contingut del nostre ts1 mitjançant la comanda strings.

![image](https://user-images.githubusercontent.com/79653853/161805295-fc4706b0-b045-48dd-9e6c-af3c382ab1ae.png)

![image](https://user-images.githubusercontent.com/79653853/161805426-09844a7c-559b-44eb-9b20-bdb9013ccbbf.png)

- Ara crea un tablespace `ts2` situat en `/discs-mysql/disk2` i col·loca-hi la resta de taules.

Farem el mateix que abans, primerament crearem el tablespace i seguidament possarem les taules que ens interessa.

![image](https://user-images.githubusercontent.com/79653853/161809229-2eaba7fa-a46e-473b-8549-9311eff6c1fa.png)

Finalment comprovarem el contingut del ts2 mitjançant la comanda strings.

![image](https://user-images.githubusercontent.com/79653853/161809538-62a13f7f-bee4-4b08-b4ff-e031acf85842.png)

![image](https://user-images.githubusercontent.com/79653853/161809724-ecb9ab0c-4deb-4227-8400-11e4318f4606.png)

## ACTIVITAT 5

- Comprova InnoDB Log Checkpointing (LSN Number, últim LSN actualitzat a disc, últim LSN amb checkpoint).

Per comprovar InnoDB Log Checkpointing farem una consulta MySQL mitjançant la comanda `SHOW`

![image](https://user-images.githubusercontent.com/79653853/161813610-76440308-bb91-445c-ba75-a571dfde557f.png)

![image](https://user-images.githubusercontent.com/79653853/161813567-f5c65004-acec-47a8-b99b-48e2f8181852.png)

- Proposa un exemple on es vegi lús de `Redolog`

El `Redolog` és basat en desar dades en disc i aquest és utilitzat durant un crash recovery per tal de corregir la incosistencia de dades en transaccions incompletes.
Durant operacions normals, el redolog codifica les queries de canviar les dades de les taules mitjançant SQL statements o trucades d'APIs de baix nivell.
Les modificacions dels arxius de dades que no s'han acabat de realitzar abans d'una pèrdua d'alimentació són repetides durant l'inicialització.

En les actuals base de dades que nosaltres utilitzem ara mateix, no podem replicar un exemple d'ús ja que tractem amb base de dades relativament petites i no hi hauria cap resultat clar. De qualsevol manera, prefereixo explicar el funcionament del `Redolog` abans que fer un exemple absurd com altres companys han fet, perquè canviar la mida dels fitxers i afegir més fitxers de logs no és `CAP EXEMPLE D'ÚS`.


webgrafia d'aquest apartat és la següent: <br>
https://dev.mysql.com/doc/refman/5.7/en/innodb-redo-log.html
https://docs.oracle.com/cd/B19306_01/server.102/b14231/onlineredo.htm
https://web.stanford.edu/dept/itss/docs/oracle/10gR2/backup.102/b14191/recoscen008.htm
https://www.percona.com/blog/2014/03/28/innodb-redo-log-archiving/
https://www.percona.com/blog/2011/02/03/how-innodb-handles-redo-logging/
https://dev.mysql.com/doc/refman/8.0/en/innodb-redo-log.html

- Com podem saber el número de pàgines modificades (dirty pages) i el número total de pàgines?

Per veure el numero de dirty pages farem l'anterior comanda `SHOW` però ara anirem a l'apartat `BUFFER POOL AND MEMORY`.

![image](https://user-images.githubusercontent.com/79653853/162045241-7f505594-ce26-4783-8536-c5b22011f80a.png)

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

Com podem veure amb el següent `SELECT`, la compressió per defecte és `kLZ4`

![image](https://user-images.githubusercontent.com/79653853/160897642-f37fd088-ca19-43f9-a3a6-92c87943a52f.png)

Altrament, podem utilitzar el següent `SELECT` per veure-ho de manera més maca.

![image](https://user-images.githubusercontent.com/79653853/162036024-7e3e81a1-da68-469a-8a97-f386f9eb2cf0.png)

- Com ho faries per canviar-lo?

Com la variable global `rocksdb_default_cf_options` no és dinàmica, canviarem aquesta variable des de l'arxiu `my.cnf`

![image](https://user-images.githubusercontent.com/79653853/162047825-eccffdc0-66aa-4d4e-92de-cf97bb4ff1fe.png)

Una vegada fet anem a comprovar els canvis.

![image](https://user-images.githubusercontent.com/79653853/162048468-9152d88e-c5fa-4d9f-8fb2-ee6106f471e6.png)
