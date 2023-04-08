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
# struktura dokumentace - jak spravovat konzoli (příručka pro servis)
Tato dokumentace obsahuje instrukce pro servisování a údržbu konzole. Dokumentace je rozdělena na dvě kategorie, software a hardware. 

## 1. Správa softwaru
Tato kapitola obsahuje instrukce pro správu a nastavení softwaru konzole. Aktualizace konzole jak her, tak samotného herního prostředí jsou automatizovány, aby se děly samostatně. Kompletní software je napsát v jazyce Python za použití knihoven Tkinter a PyGame. Tkinter slouží pro manipulaci s okny a hlavní cyklus. Pomocí knihovny PyGame jsou realizovány hry. Operační systém na konzoli je Linux pro Raspberry Pi 64 bit, desktop verze. 

### 1.1 Správa systémového prostředí (hlavní program)
Řídícím programem pro spuštění je soubor menu_rpi.py ve kterém je inicializováno herní prostředí (menu, nastavení, žebříčky). Tento skript dále volá ostatní. Na následující seznamu jsou popsány role jednotlivých vedlejších skriptů. Jejich detailní popis naleznete níže.

- db_admin.py - správa a volání databáze, mazání a zapisování záznamů, slouží pro uchování skóre pro jednotlivé hry a hráče
- game.py - třída pro inicializaci her, využívaná souborem games_list.py
- games_list.py - třídy pro inicializaci herního seznamu, manipulaci se hrami, spouštění her
- grove_controls.py - mapování jednotlivých vstupů systému Grove pro jednotlivé klávesy
- keyboard_tk.py - inicializace klávesnice pro zápis přezdívky hráče

#### 1.1.1 db_admin.py
Tento skript slouží pro editaci připojené databáze. Databáze obsahuje jednu tabulku "score", ve které jsou parametry "hra", "hráč", "skóre". Tabulka obsahuje pro každou hru 3 záznamy. Přístupové údaje k databázi jsou obsaženy v souboru config.ini. Databáze je typu pSQL. Jazyk pro práci s databází je SQL. Tento soubor obsahuje testovací main metodu, kde je možné testovat jednotlivé funkce.

#### 1.1.2 game.py
Soubor game.py obsahuje informace o jednotlivých hrách. Konkrétně název, cesta k main metodě hry, cesta k miniatuře (obrázku) hry. Obě cesty začínají v kořenovém adresáři BP_console_menu. 

#### 1.1.3 games_list.py
Soubor games_list.py slouží pro inicializaci her. Prvnotní inicializace probíhá čtením parametrů ze souboru games.txt. Bude více rozebráno v kapitole 1.2. 

#### 1.1.4 grove_controls.py
V tomto souboru probíhá naslouchání a převod vstupů na konkrétní klávesy. Pro naslouchájí vstupů slouží knihovny gpiozero a grove. Knihovna pyautogui zajišťuje simulaci stisku kláves. Např. po zjištění stisku tlačítka soubor vyvolá stisk klávesy "p". 


Třída Button_controller je využita pro Grove Dual button. Na konzoli naleznete dvě. 
Pro přidání třídy do nové hry je třeba vytvořit novou instanci této třídy. Nejprve je třeba importovat soubor grove_controls.py příkazem "import grove_controls". Dále vytvoříme instanci příkazem button = grove_controls.Button_controller("číslo pinu" (int), "klávesa" (str)). Ćíslo pinu odpovídá pinu, na kterém je tlačítko zapojené. Informace o zapojení v kapitole 2.2.1. Klávesa odpovídá klávese, jejíž stisk se zmáčknutím tlačítka vyvolá. 
Chcete-li připojit tlačítko na pinu 6, které bude simulovat stisk klávesy "p". Button = grove_controls.Button_controller(6, "p").

Třída Joystick_controller slouží pro řízení vstupů z analogového Grove Thumb Joysticku, jež je zapojen na konektoru A0. V případě špatné reakce joysticku je možné v této metodě změnit toleranci pohybu ve směru x,y. Uživatel totiž nikdy nebude s joystickem hýbat přesně v jednotlivých osách. 

#### 1.1.5 keyboard_tk.py
Soubor keyboard_tk.py obsahuje třídu pro vytvoření instance klávesnice, jež se zobrazuje na displeji. Tato klávesnice slouží pro zapsání přezdívky hráče. Využívá knihovnu Tkinter. 

### 1.2 Správa her
#### 1.2.1 Přidání nové hry
Nová hra musí splňovat následující parametry. Kód v jazyce python. Po spuštění se otevře nové okno knihovny Tkinter. Ideální knihovna pro psaní hry PyGame. Hra musí být spustitelná x-krát za sebou (musí být ošetřená inicializace a následné smazání instance po skončení cyklu hry). 
Do nové hry je třeba přidat třídu grove_controls pomocí příkazu "import grove_controls". Tuto třídu následně využijte v sekci ovládání hry. Detailní použití této třídy naleznete v kapitole 1.1.4. 

#### 1.2.2 Odebrání hry

#### 1.2.3 Editace hry

### 1.3 Nastavení vstupů
#### 1.3.1 Konfigurace tlačítek

#### 1.3.2 Konfigurace joysticku

#### 1.3.3 Připojení a nastavení senzorů (pohybový a na snímání vzdálenosti)

### 1.4 Nastavení výstupů

#### 1.4.1 Konfigurace displeje

## 2 Správa hardwaru

### 2.1 Demontáž krytu

### 2.2 Zapojení modulů (vstupů)

#### 2.2.1 Zapojení tlačítek

#### 2.2.2 Zapojení joysticku

#### 2.2.3 Zapojení senzorů

#### 2.2.4 Zapojení displeje

#### 2.2.5 Seznam všech připojených komponent

### 2.3 Připojení k elektrické síti a LAN
