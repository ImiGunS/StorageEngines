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

Surt un error, però igualment activa l'storage engine que volem.

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

- Busca informació dels schemas de metadata i l'objectiu de cadascun d'ells. Posa un exemple d'us.


