Detta projekt är en multiapplikations container där endast en AstroMain applikationen är nåbar från internet.
AstroMain agerar också som reverse proxy och då AstroMain kan kommunicera med AstroSecondary kan vi se den andra 
applikationen om vi följer länken som finns på AstroMain.

# Starta båda containrarna genom Docker Run
Bygg ett nätverk:
* docker network create myappnet

För att bygga AstroMain(Gå ner i mappen AstroMain):
* docker build -t astromain .

För att bygga AstroMain(Gå ner i mappen AstroSecondary):
* docker build -t astrosecondary .

För att starta AstroSecondary:
* docker container run --name astrosecondary --network myappnet -d astrosecondary 

För att starta AstroMain:
* docker container run -p 80:80 -d --name astromain --network myappnet astromain

För att ta bort AstroMain:
* docker container rm -f astromain

För att ta bort AstroSecondary:
* docker container rm -f astrosecondary

# Starta båda containrarna genom docker compose
För att bygga och starta:
* I rootmappen | docker compose up -d

För att stänga ner och ta bort:
* I rootmappen | docker compose down



Hemsidan går att besöka på localhost:80