# Aiven-Vercel

Installation av aiven/vercel!

VIKTIGT ÄR ATT NI ÄR INNE PÅ MAIN SOM DEFAULT BRANCH MASTER SKA INTE FINNAS

Följ pdfn till att ni skapat konton på både aiven och vercel. När ni har installerat och ni ser denna vy 
Då ska ni in i vercel och gå in på importera git repo 
importera till det repo ni ska jobba i.
När ni kommer in så kommer ni välja map i root directory så ni väljer edit och går in på rätt map.

Därefter ska ni trycka ner build and output settings så ni får upp dessa 3 alternativ

Viktigt! Ni ska BARA trycka på knappen overide på output directory och skriva api

sen skriver man in din key ni har i laravel projektet som finns i env filen kopiera allt efter = tecknet. har man inte den då ska man genera key. Skriv in nyckeln i keyfältet! 
trycker ni på deploy!
Detta kommer inte att fungera och ni kommer få ett error så va inte oroliga!
gå in på er adminer nu 

system ska vara: MySQL
server kommer vara eran host som finns i aiven och eran port detta kommer se ut t.ex. så här. blabla-blabla-blabla.bla.aivencloud.com:12345
så viktigt att inte glömma “:” mellan host och port “host:port”.
användarnamn är eran user 
och password är eran password 
databas är erat database name. 
Alla dessa finns i aiven!

Nu ska ni kunna logga in i adminer

Nu går ni tillbaka in i vercel och deployar igen. Ni kanske behöver fylla i uppgifterna igen. när den har deployat  då ska ni få upp det här! 

Nu har ni deployat i vercel som är en server och aiven är eran databas. 

Så nu inuti eran laravel root map skapa en folder som heter api.
inuti api foldern ska ni göra en index.php som har denna kod:
<?php
// Forward Vercel requests to normal index.php
require __DIR__ . '/../public/index.php';

samt att ni skapa i laravels root map end vercel.json fil som ska ha denna kod 
{
    "version": 2,
    "framework": null,
    "functions": {
    "api/index.php": { "runtime": "vercel-php@0.6.1" }
    },
    "routes": [{
    "src": "/(.*)",
    "dest": "/api/index.php"
    }],
    "env": {
    "APP_ENV": "production",
    "APP_DEBUG": "true",
    "APP_URL": "https://yourproductionurl.com",
    "APP_CONFIG_CACHE": "/tmp/config.php",
    "APP_EVENTS_CACHE": "/tmp/events.php",
    "APP_PACKAGES_CACHE": "/tmp/packages.php",
    "APP_ROUTES_CACHE": "/tmp/routes.php",
    "APP_SERVICES_CACHE": "/tmp/services.php",
    "VIEW_COMPILED_PATH": "/tmp",
    "CACHE_DRIVER": "array",
    "LOG_CHANNEL": "stderr",
    "SESSION_DRIVER": "cookie"
    }
    }


Så gå in på eran vercel, gå in på ert projekt, det vill säga den ni skapade.
gå in på settings 
tryck sedan på Environment variables

Skriv detta key = APP_KEY och value = eran env genererade key.	sen tryck save

Sen trycker ni på deployment och redeploy

Detta ska funka. Men om det inte fungerar så kan det vara för att ni är inne på en master branch.. Du måste ha main som default bransch. Om detta är fallet radera hela vercel projektet och skapa om det i main…
