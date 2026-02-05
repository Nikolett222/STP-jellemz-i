# STP-jellemz-i
1. Beállításának menete (Haladó konfiguráció)
A alapbeállításokon túl érdemes finomhangolni a rendszert a maximális stabilitásért:

Mód megadása: 
  A spanning-tree mode rapid-pvst mellett létezik a modernebb MST (Multiple Spanning Tree), amely több VLAN-t csoportosít egy példányba, csökkentve a CPU terhelését.
Fő switch kijelölése: 
  A priority 4096 (vagy 0 a legmagasabb prioritáshoz) mellett használhatod a spanning-tree vlan [ID] root primary parancsot is, ami automatikusan az aktuális minimum alá lövi be az értéket.
Védelmi funkciók:
BPDU Guard: 
  A PortFast portokon kapcsold be (spanning-tree bpduguard enable). Ha valaki egy másik switchet dug a PC helyére, a port azonnal lekapcsol, megvédve a hálózatot a külső huroktól.
Root Guard: 
  Megakadályozza, hogy egy újonnan csatlakoztatott, véletlenül alacsonyabb prioritású switch átvegye a "főnök" (Root Bridge) szerepét.
3. További előnyök
Skálázhatóság: 
  A Rapid PVST+ segítségével minden VLAN külön fát építhet, így az egyik VLAN forgalma az egyik, a másiké a másik fizikai linket használhatja (terheléselosztás).
Dinamikus topológia-követés: 
  Nemcsak kábelszakadáskor, hanem új eszköz hozzáadásakor is azonnal újraszámolja az optimális útvonalat.
4. Hátrányok és korlátok
Erőforrás-igény: 
  Minden egyes VLAN-hoz tartozó STP példány CPU-t és memóriát fogyaszt a switchen.
Sub-optimális útvonalak: 
  Mivel az STP blokkolja a portokat, előfordulhat, hogy az adatcsomagok "kerülőúton" mennek, ami növeli a késleltetést (latency).
Broadcast vihar veszélye: 
  Egy hibás konfiguráció (pl. PortFast és BPDU Guard nélkül) továbbra is okozhat hálózati "megfagyást" a topológia változásakor.
5. Haladó gyakorlati példák
EtherChannel kombináció: 
  Az STP-t gyakran használják EtherChannel (Link Aggregation) mellett. Míg az EtherChannel összefogja a kábeleket egy logikai csatornába, az STP gondoskodik róla, hogy ha a teljes csatorna kiesik, legyen tartalék.
Mindenki "Edge" portja: WiFi hozzáférési pontoknál (AP) kritikus a PortFast, mert az AP-k gyakran újraindulnak, és a felhasználók nem várhatnak 30 másodpercet az IP-cím kérésével (DHCP timeout).
