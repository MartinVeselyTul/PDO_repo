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

Tato dokumentace obsahuje instrukce pro servisování a údržbu konzole. Dokumentace je rozdělena na dvě kategorie, software a hardware. 

## 1. Správa softwaru
Kapitola zabývající se systémovým prostředím, správou her, nastavením systému v Raspberry Pi a propojením hardwaru se softwarem.

### 1.1 Struktura adresáře
Zobrazení struktury adresáře se zdrojovými kódy herního prostředí, her a vstupů.

BP_console_menu
├── games
│   └── snake
│       ├── ...
│       │   └── ...
│       ├── ...
│       └── main.py
├── pict
│   ├── 0.jpg
│   ├── 1.jpg
│   └── 2.jpg
├── sounds
│   └── button
│       ├── button1.mp3
│       ├── button2.mp3
│       ├── ...
│       └── button7.mp3
├── menu_rpi.py
├── db_admin.py
├── game.py
├── games_list.py
├── games.txt
├── grove_controls.py
├── keyboard_tk.py
└── config.ini


### 1.2 Správa her
V této kapitole naleznete, jak přidat, odebrat, či editovat hru. 
Hry se nachází v adresáři /games/název hry.

#### 1.2.1 Přidání nové hry
Pro přidání nové hry postupujte dle následujících kroků.
1.	Hra musí splňovat
•	Napsaná v jazyce Python (verze 3.9 a vyšší)
•	Podporované knihovny: PyGame, Tkinter
•	Opakovatelně spustitelný main.py soubor (především opakovaná inicializace)
•	Hra nesmí zapisovat a vytvářet nové soubory 
2.	Ve složce /games vytvořte novou složku, název bez mezer a diakritiky či speciálních znaků
3.	Obsah nové hry vložte do vytvořené složky
4.	Do složky /pict vložte miniaturu (úvodní obrázek) hry
•	Formát obrázku .jpg
•	Ideální poměr obrázku 1:1
•	Název zvolte číslo, které následuje po již existujících souborech (např. 3.jpg dle struktury našeho adresáře) 
5.	Do souboru games.txt vložte nový řádek, na který napište
•	Název hry, cestu k main.py souboru, cestu k miniatuře obrázku
•	Cesty začínají od adresáře BP_console_menu (k adresáři games se odkážete /games, k adresáři pict dále /pict)
•	Soubor uložte
6.	Otestujte
•	Hra by se měla zobrazit v úvodním menu
•	Po jejím otevření otestujte opakované spuštění
•	Po úspěšném otestování zavřete hlavní skript
7.	Otevřete terminál a zadejte následující příkazy
•	git pull
•	git add .
•	git commit -m „název hry“
•	git push
8.	Hra je nyní úspěšně přidaná do konzole i jejího online repozitáře






