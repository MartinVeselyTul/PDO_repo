# dokumentace - Retro herní konzole postavená na Raspberry Pi
## Jakou práci dokumentuji?
Dokumentuji svou bakalářskou práci, která se zabývá výrobou retro konzole, která vychází z Raspberry Pi. 
Vytvářený je jak software (OS, mapování vstupů a přizpůsobení stažených her pro náš OS), tak hardware (kabely, moduly a dřevěný kryt konzole).
Konzole slouží pro hraní retro her jako například had v retro podání malé dřevěné konzole. Vstupy jsou joystick a tlačítka, ve vývoji ještě další.

## Jaká je má cílová skupina?
Za svou cílovou skupinu mohu považovat buď skupinu nadšených programátorů, nebo hráčů, kteří svůj herní zážitek započali právě u her jako had, nebo Pacman.
Dále by má cílová skupina mohla být skupina dětí, kterým bude konzole svěřena. 
Pro psaní dokumentace bude ale ideální zvolit skupinu administrátorů, nebo lidí, jež budou konzoli servisovat, pokud se něco rozbije a bude potřeba vyměnit nějaký díl, nebo vyřešit softwarový problém.

## Jak si představit člena cílové skupiny a jaké bude mít úkoly?
Za člena cílové skupiny si představuji člověka, který má znalosti s Raspberry Pi a jeho OS, aby byl schopný vyřešit případný problém, pokud by v systému něco selhalo. Také by měl být schopen vyřešit případný problém s modulem (nereaguje tlačítko, nefunguje joystick), tudíž by měl být zručný, aby mohl moduly vyměnit.

#### -------------------------------------------------------------------------
# Jak spravovat konzoli (příručka pro servis)

## 1 Správa softwaru

Kapitola zabývající se systémovým prostředím, správou her, nastavením systému v Raspberry Pi a propojením hardwaru se softwarem.

### 1.1 Struktura adresáře

Zobrazení struktury adresáře se zdrojovými kódy herního prostředí, her a vstupů.

![image](https://user-images.githubusercontent.com/79989547/235484620-1575899d-d9e2-4856-8247-e65b512c0756.png)


## 1.2 Správa her

V této kapitole naleznete, jak přidat, odebrat, či editovat hru.

Hry se nachází v adresáři /games/název hry.

### 1.2.1 Přidání nové hry

Pro přidání nové hry postupujte dle následujících kroků.

1. Hra musí splňovat
    -  Napsaná v jazyce Python (verze 3.9 a vyšší)
    - Podporované knihovny: PyGame, Tkinter
    - Opakovatelně spustitelný main.py soubor (především opakovaná inicializace)
    - Hra nesmí zapisovat a vytvářet nové soubory
2. Ve složce /games vytvořte novou složku, název bez mezer a diakritiky či speciálních znaků
3. Obsah nové hry vložte do vytvořené složky
4. Do složky /pict vložte miniaturu (úvodní obrázek) hry
    - Formát obrázku .jpg
    - Ideální poměr obrázku 1:1
    - Název zvolte číslo, které následuje po již existujících souborech (např. 3.jpg dle struktury našeho adresáře)
5. Do souboru games.txt vložte nový řádek, na který napište
    - Název hry, cestu k main.py souboru, cestu k miniatuře obrázku
    - Cesty začínají od adresáře BP\_console\_menu (k adresáři games se odkážete /games, k adresáři pict dále /pict)
    - Soubor uložte
6. Otestujte
    - Hra by se měla zobrazit v úvodním menu
    - Po jejím otevření otestujte opakované spuštění
    - Po úspěšném otestování zavřete hlavní skript
7. Otevřete terminál a zadejte následující příkazy
    - git pull
    - git add .
    - git commit -m „název hry"
    - git push
8. Hra je nyní úspěšně přidaná do konzole i jejího online repozitáře

### 1.2.2 Odebrání hry

Pro odebrání hry postupujte následovně.

1. Vypněte hlavní skript konzole
2. Otevřete soubor games.txt a konkrétní řádek s názvem hry smažte, soubor uložte
3. Otevřete adresář /games a složku s názvem hry smažte
4. Otevřete adresář /pict a proveďte následovné
    - Najděte miniaturu zvolené hry a smažte ji
    - Přejmenujte ostatní .jpg soubory, aby čísla šla za sebou (dle ukázky adresáře, pokud smažete soubor 1.jpg, přejmujte soubor 2.jpg na 1.jpg, aby zbylo 0.jpg a nově přejmenovaný soubor 1.jpg)
5. Otevřete terminál a zadejte následující příkazy
    - git pull
    - git add .
    - git commit -m „deleting název hry"
    - git push
6. Hra je odstraněna z konzole i jejího online repozitáře

### 1.2.3 Editace hry

Pro editaci hry postupujte následovně.

1. Otevřete adresář /games
2. V adresáři otevřete složku s názvem hry
3. V tomto adresáři naleznete kompletní zdrojový kód
4. Po upravení hry vše uložte
5. Otevřete terminál a zadejte následující příkazy
    1. git pull
    2. git add .
    3. git commit -m „updating název hry"
    4. git push
6. Hra je nyní aktualizovaná v úložišti konzole i jejím online repozitáři

### 1.2.4 Aktualizace miniatury (obrázku hry)

Pro aktualizaci miniatury hry postupujte následovně.

1. Otevřete adresář /pict
2. Nalezněte miniaturu, jež chcete změnit
3. Nový soubor .jpg pojmenujte stejným názvem jako nalezenou miniaturu
4. Smažte starý soubor .jpg umístěný v adresáři /pict
5. Nahrajte nový soubor .jpg do adresáře /pict
6. Otevřete terminál a zadejte následující příkazy
    1. git pull
    2. git add .
    3. git commit -m „updating pict název hry"
    4. git push
7. Miniatura je nyní aktualizovaná v úložišti konzole i jejím online repozitáři

## 1.3 Nastavení vstupů

V této kapitole naleznete, jak nastavovat jednotlivé vstupy systému Grove. Konkrétně jak softwarově změnit jejich nastavený port a jak vstupy kalibrovat.

Třídy jednotlivých vstupů naleznete v souboru grove\_controls.py.

Ovládání herního prostředí – instance inicializovaná v souboru menu\_rpi.py

Ovládání jednotlivých her – instance inicializovaná v jednotlivých main souborech her (adresář /games)

## 1.4 Seznam jednotlivých vstupů

V tabulce je uveden seznam jednotlivých vstupních zařízení Grove. U každého modulu je uvedeno, na jakém portu je zapojen a co za signály využívá.

![image](https://user-images.githubusercontent.com/79989547/235484687-00f508b1-46ca-4d3c-8719-1aabda342aa4.png)

NC – not connected (není připojeno)

### 1.4.1 Konfigurace tlačítek

Pro **změnu portu** , v jakém je tlačítko zapojeno postupujte následovně.

1. V inicializační části souboru nalezněte vytváření instance zvoleného tlačítka.
2. Instance je vytvářena zadáním 2 čísel (int) – jedná se o GPIO piny, na kterých je tlačítko zapojeno.
3. Pro změnu konektoru číselné hodnoty změňte na požadovaný port.
    1. Ujistěte se, že daný port je digitální (označení písmenem D)
    2. Dbejte na správné číslování zadaného portu.
    3. Ujistěte se, že na zadaný port není nastaveno jiné zařízení.
4. Konzoli v sekci nastavení vypněte a odpojte od zdroje napájení
5. Připojte dvojité tlačítko na zadaný port
6. Zapojte zdroj napájení a otestujte funkcionalitu tlačítka
7. Při potížích kontaktujte výrobce

### 1.4.2 Konfigurace joysticku

Pro **změnu portu** , v jakém je joystick zapojený postupujte následovně.

1. V inicializační části souboru nalezněte vytváření instance joysticku.
2. Instance je vytvářena zadáním čísla (int) – jedná se o GPIO pin, na kterém je joystick zapojený
3. Pro změnu konektoru číselné hodnoty změňte na požadovaný port.
    1. Ujistěte se, že daný port je analogový (označení písmenem A)
    2. Dbejte na správné číslování zadaného portu.
    3. Ujistěte se, že na zadaný port není nastaveno jiné zařízení.
4. Konzoli v sekci nastavení vypněte a odpojte od zdroje napájení
5. Připojte joystick na zadaný port
6. Zapojte zdroj napájení a otestujte funkcionalitu joysticku
7. Při potížích kontaktujte výrobce

Pro **kalibraci** joysticku postupujte následovně.

1. Otevřete soubor grove\_controls.py
2. Ve třídě Joystick\_controller se přesuňte do funkce joystick\_handle().
3. Ve stavovém automatu této funkce změňte požadované hodnoty
    1. Hodnoty jsou umístěny v podmínkách, v každé podmínce lze vidět, jaký pohyb joysticku podmínka ovládá
    2. Pro kompletní seznámení s výstupními hodnotami joysticku vyhledejte stránku výrobce joysticku
    3. Poslední podmínku této funkce nenastavujte a nepřepisujte
4. Soubor uložte
5. V sekci nastavení restartujte konzoli
6. Otestujte změnu funkcionality joysticku
7. Při potížích kontaktujte výrobce

### 1.4.3 Nastavení PIR senzoru a režimu hibernace

Pro **změnu portu** , v jakém je PIR senzor zapojený postupujte následovně.

1. V inicializační části souboru nalezněte vytváření instance PIR senzoru.
2. Instance je vytvářena zadáním čísla (int) – jedná se o GPIO pin, na kterém je PIR senzor zapojený
3. Pro změnu konektoru číselné hodnoty změňte na požadovaný port.
    1. Ujistěte se, že daný port je digitální (označení písmenem D)
    2. Dbejte na správné číslování zadaného portu.
    3. Ujistěte se, že na zadaný port není nastaveno jiné zařízení.
4. Konzoli v sekci nastavení vypněte a odpojte od zdroje napájení
5. Připojte PIR senzor na zadaný port
6. Zapojte zdroj napájení a otestujte funkcionalitu senzoru
7. Při potížích kontaktujte výrobce

Pro **nastavení režimu hibernace** postupujte následovně.

1. Otevřete soubor grove\_controls.py
2. Ve třídě PIRMotionSensor se přesuňte do funkce get\_motion()
3. Pro změnu časové hodnoty změňte proměnnou sleep\_time na vámi zvolenou hodnotu (int)
4. V sekci nastavení konzoli restartujte

## 1.5 Nastavení výstupů

### 1.5.1 Konfigurace displeje

# 2 Správa hardwaru

## 2.1 Demontáž krytu – přístup do konzole

Tato kapitola obsahuje návod na demontáž krytu pro přístup do konzole. Výměnu jednotlivých modulů.

## 2.2 Výměna modulů

Pro výměnu konkrétního modulu nejprve podnikněte tyto kroky.

1. V sekci nastavení konzoli vypněte a odpojte od zdroje.
2. Za použití křížového šroubováku typu PH2 vyšroubujte ze zadní strany konzole 6 šroubů.
3. Zadní stěnu konzole odejměte
4. Pokračujte výměnou modulu v další kapitole

### 2.2.1 Výměna tlačítek

Pro výměnu tlačítka dodržujte následující postup.

1. Tlačítko odpojte z konektoru grove
    1. Pokud nebylo jeho umístění změněno, zapojení naleznete v kapitole 1.4
    2. Ověřte, že je konzole odpojená od napájení, hrozí nebezpečí úrazu elektrických proudem
2. Za použití šroubováku typu PH1 vyšroubujte 2 šrouby upevňující dané tlačítko ze spodní strany konstrukce
3. Nové tlačítko umístěte na místo starého tlačítka a stejným postupem přišroubujte
4. Zapojte konektor systému grove do konzole na místo starého tlačítka
5. Nasaďte zadní stranu konzole
6. Za použití šroubováku PH2 zajistěte 6 šroubů upevňující zadní stěnu konzole
7. Do konzole připojte napájecí kabel

### 2.2.2 Výměna joysticku

Pro výměnu joysticku dodržujte následující postup.

1. Joystick odpojte z konektoru grove
    1. Pokud nebylo jeho umístění změněno, zapojení naleznete v kapitole 1.4
    2. Ověřte, že je konzole odpojená od napájení, hrozí nebezpečí úrazu elektrických proudem
2. Za použití šroubováku typu PZ1 vyšroubujte 2 šrouby upevňující joystick ze spodní strany konstrukce
3. Nový joystick umístěte na místo starého joysticku a stejným postupem přišroubujte
4. Zapojte konektor systému grove do konzole na místo starého joysticku
5. Nasaďte zadní stranu konzole
6. Za použití šroubováku PH2 zajistěte 6 šroubů upevňující zadní stěnu konzole
7. Do konzole připojte napájecí kabel

### 2.2.3 Výměna displeje

Pro výměnu displeje postupujte následovně.

1. Ujistěte se, že je zařízení odpojeno z napájení, hrozí nebezpečí úrazu elektrickým proudem.
2. Odpojte z displeje oba kabely (HDMI a USB)
3. Za použití šroubováku PH2 vyšroubujte z rámu displeje 4 šrouby
4. Jemným tlakem do displeje z přední strany konzole zatlačte a vyjměte displej z konzole
5. Před umístěním nového displeje zkontrolujte
    1. Velikost displeje – musí být totožná se starým displejem
    2. Typ připojení displeje – musí využívat HDMI připojení a napájení přes microUSB či USB-A konektor
    3. Díry na uchycení displeje do konstrukce
6. Displej umístěte na místo starého displeje
7. Za použití šroubováku PH2 přišroubujte do rámu displeje 4 šrouby
8. Propojte kabely displej s konzolí (kabely HDMI a USB)
9. Nasaďte zadní stranu konzole
10. Za použití šroubováku PH2 zajistěte 6 šroubů upevňující zadní stěnu konzole
11. Do konzole připojte napájecí kabel






