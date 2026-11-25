# Inhoud voor de repo `maluku-nick.github.io` (GitHub Pages, user site)

Tesla Fleet API vereist een publieke sleutel op de **root** van een domein. Daarom een user site (`<naam>.github.io`),
geen project site (`<naam>.github.io/PikoeOS/`).

Bestanden:
- `.nojekyll` – anders slaat GitHub Pages mappen die met een punt beginnen (`.well-known`) over
- `.well-known/appspecific/com.tesla.3p.public-key.pem` – **de publieke sleutel** (zie hieronder; niet de private!)
- `callback/index.html` – toont na het inloggen bij Tesla de code om in `node tesla.js login` te plakken. Geen netwerkverkeer
- `index.html` – korte uitleg

Sleutelpaar maken (op de NAS, via SSH):
```
cd /volume1/docker/pikoeos
sudo openssl ecparam -name prime256v1 -genkey -noout -out state/tesla-private-key.pem
sudo chmod 600 state/tesla-private-key.pem
sudo openssl ec -in state/tesla-private-key.pem -pubout -out tesla-pages/.well-known/appspecific/com.tesla.3p.public-key.pem
```
De private sleutel blijft in `state/` (versleutelde back-up). PikoeOS gebruikt hem niet (alleen nodig voor commando's
naar de auto); deel hem nooit en zet hem nooit in GitHub.

In de Tesla-app-aanvraag:
- Allowed origin: `https://maluku-nick.github.io`
- Redirect URI: `https://maluku-nick.github.io/callback/`
