# Case_study_1

# Vulnerability Coverage Study Cases – Aruba a Arista

> Pracovní poznámky k vyhodnocování zranitelností síťových zařízení.
>
> Cíl: umět identifikovat výrobce, operační systém, verzi zařízení a porovnat je s informacemi v security advisory.

---

# Study Case 1 – Aruba

## 1. Rychlý průzkum Aruba

### Jaké typy zařízení Aruba vyrábí

Společnost Aruba (dnes součást HPE) vyrábí především:

* Wi‑Fi access pointy
* Switche
* Gateway a controllery
* SD‑WAN zařízení
* Zařízení pro správu přístupu do sítě (NAC)
* Cloud management platformy

### Jak ovlivnila akvizice Aruba společností HPE zdroj informací o zranitelnostech

Aruba byla koupena společností HPE. Z tohoto důvodu už nejsou informace o zranitelnostech publikovány pouze na původních Aruba stránkách, ale často na:

* HPE Security Bulletin
* HPE Support Center
* Aruba Support Portal

Praktický důsledek:

* při hledání advisories je potřeba hledat jak „Aruba security advisory“, tak „HPE Aruba security bulletin“
* některé starší odkazy vedou na Aruba web, novější advisories jsou často pod HPE

### Používá Aruba jeden nebo více operačních systémů?

Aruba nepoužívá jeden univerzální operační systém.

Používá více OS podle typu zařízení:

* ArubaOS / AOS-8
* ArubaOS 10 / AOS-10
* ArubaOS-CX
* InstantOS

Pro správné vyhodnocení zranitelnosti je potřeba vždy zjistit:

1. model zařízení
2. typ operačního systému
3. konkrétní verzi OS

---

## 2. Security Advisory

> POZNÁMKA: V zadání chybí konkrétní odkaz na advisory. Níže je připraven postup a místo pro doplnění výsledků.

### Advisory pokrývá:

* [ ] jednu CVE
* [ ] více CVE

### Identifikované CVE

* CVE-........
* CVE-........

### Dotčené operační systémy

| Operační systém | Zranitelné verze         |
| --------------- | ------------------------ |
| AOS-8           | doplnit podle advisory   |
| AOS-10          | doplnit podle advisory   |
| ArubaOS-CX      | doplnit pokud je uvedeno |

### Evidence

Do poznámek vložit citaci z advisory, například:

```text
„Affected versions: ArubaOS 10.7.x prior to 10.7.0.2“
```

Zdroj:

* vložit odkaz na advisory

---

## 3. Výběr CLI příkazu

Cílem je získat model zařízení a verzi operačního systému.

### AOS-8

Vybraný příkaz:

```text
show version
```

Důvod:

* vypisuje model zařízení
* vypisuje verzi ArubaOS
* poskytuje dostatek informací pro porovnání s advisory

Příklad očekávaného výstupu:

```text
ArubaOS Version 8.x.x.x
MODEL: Aruba7005
```

### AOS-10

Vybraný příkaz:

```text
show version
```

nebo

```text
show inventory
```

Důvod:

* „show version“ většinou obsahuje verzi OS
* „show inventory“ může pomoci ověřit přesný model zařízení

Příklad:

```text
ArubaOS Version 10.7.0.1
MODEL: Aruba7005
```

### Proč je tento příkaz vhodný

Security advisory obvykle obsahuje:

* seznam zranitelných modelů
* seznam zranitelných verzí

Proto je právě kombinace „model + verze“ nejdůležitější.

---

## 4. SNMP – základní informace

### Jaké typy požadavků SNMP podporuje

SNMP podporuje zejména:

* GET – získání hodnoty
* GETNEXT – získání další hodnoty v MIB stromu
* GETBULK – získání více hodnot najednou
* SET – změna hodnoty
* TRAP – zařízení samo odešle upozornění
* INFORM – potvrzené upozornění

### Co je OID

OID (Object Identifier) je jednoznačný identifikátor určité informace v SNMP stromu.

Například:

```text
1.3.6.1.2.1.1.1
```

odpovídá sysDescr.

### Existuje OID pro získání systémového popisu zařízení?

Ano.

```text
sysDescr = 1.3.6.1.2.1.1.1.0
```

Tento OID často vrací:

* výrobce
* model
* verzi operačního systému

### Jaký port používá SNMP standardně

* UDP 161 – běžné dotazy
* UDP 162 – trap zprávy

---

## 5. Vyhodnocení SNMP výstupu

Výstup:

```text
ArubaOS (MODEL: Aruba7005), Version 10.7.0.1 SSR (91033)
```

### Co z výstupu zjistím

* výrobce / OS: ArubaOS
* model: Aruba7005
* verze: 10.7.0.1

### Lze z toho určit, zda je zařízení zranitelné?

Ano, ale pouze po porovnání s advisory.

Možné scénáře:

* pokud advisory uvádí, že jsou zranitelné verze například do 10.7.0.1 včetně, zařízení je pravděpodobně zranitelné
* pokud advisory uvádí, že opravená verze je od 10.7.0.2, zařízení s verzí 10.7.0.1 je stále zranitelné
* pokud advisory uvádí, že zranitelné jsou pouze verze 8.x, zařízení není zranitelné

### Evidence

```text
Model: Aruba7005
Version: 10.7.0.1
```

Toto je dostatečný důkaz pro porovnání s advisory.

---

## 6. Závěr

### Jaké zdroje lze použít k identifikaci výrobce a OS zařízení

| Zdroj                   | Co zjistím               | Vyžaduje přihlašovací údaje? | Spolehlivost                 |
| ----------------------- | ------------------------ | ---------------------------- | ---------------------------- |
| SNMP sysDescr           | výrobce, model, verze OS | ne vždy                      | rychlé, ale nemusí být úplné |
| CLI show version        | model, OS, verze         | ano                          | nejspolehlivější             |
| Web management rozhraní | model, verze             | ano                          | dobré                        |
| Banner služby           | někdy výrobce / verze    | ne                           | méně spolehlivé              |
| MAC adresa / OUI        | výrobce                  | ne                           | jen výrobce                  |

### Nejrychlejší zdroj

SNMP sysDescr.

### Nejspolehlivější zdroj

CLI příkaz `show version`.

### Který zdroj vyžaduje credentials

CLI a web management.

### Postup pro ověření známé zranitelnosti

1. zjistit výrobce
2. zjistit model zařízení
3. zjistit OS a verzi
4. otevřít vendor security advisory
5. porovnat model a verzi s affected versions
6. ověřit, zda nejsou potřeba další podmínky (například zapnutá konkrétní služba)
7. navrhnout mitigaci nebo upgrade

---

---

# Study Case 2 – Arista

## Part 1

## 1. Rychlý průzkum Arista

### Jaké typy zařízení Arista vyrábí

Arista vyrábí hlavně:

* datacentrové switche
* routery
* cloud networking zařízení
* síťová zařízení pro enterprise prostředí

### Co je EOS

EOS = Extensible Operating System.

Jde o operační systém Arista zařízení založený na Linuxu.

### Kde Arista publikuje security advisories

Arista advisories bývají na:

* Arista Security Advisories
* Arista Product Security Center

---

## 2. Security Advisory

> V zadání chybí konkrétní odkaz na advisory pro CVE-2025-8872. Níže je připraven prostor pro doplnění.

### CVE

```text
CVE-2025-8872
```

### Zranitelné EOS verze

| EOS verze              | Stav       |
| ---------------------- | ---------- |
| doplnit podle advisory | vulnerable |
| doplnit podle advisory | fixed      |

### Dotčené hardware řady

* DCS-....
* 7050X
* 7150S
* ...

### Je potřeba speciální konfigurace?

* [ ] Ano
* [ ] Ne

Pokud ano, doplnit:

```text
Například musí být zapnutá konkrétní služba, protokol nebo feature.
```

### Zmíněný síťový protokol

* doplnit podle advisory

### Doporučená mitigace

* upgrade EOS
* vypnutí zranitelné služby
* ACL / omezení přístupu

---

## 3. Analýza výstupu show version

Výstup:

```text
Arista DCS-7150S-64-CL-F
Software image version: 4.32.2F
Architecture: i386
```

### Relevantní informace

* `Arista DCS-7150S-64-CL-F`

  * důležité pro porovnání s affected hardware

* `Software image version: 4.32.2F`

  * nejdůležitější údaj
  * porovnává se s vulnerable / fixed verzemi

### Potenciálně relevantní informace

* `Architecture: i386`

  * může být relevantní pouze pokud advisory uvádí, že je zranitelnost omezená na konkrétní architekturu
  * nutné ověřit v advisory

* `Internal build version`

  * může být užitečný, pokud advisory rozlišuje buildy stejné verze

### Irrelevantní informace

* Serial number
* System MAC address
* Uptime
* Total memory
* Free memory

Tyto údaje běžně neovlivňují, zda je zařízení zranitelné.

### Nejrelevantnější údaj pro další průzkum

```text
Software image version: 4.32.2F
```

### Plán dalšího ověření

1. otevřít advisory
2. zjistit affected versions
3. porovnat, zda 4.32.2F spadá do seznamu
4. ověřit, zda model 7150S patří mezi affected hardware
5. ověřit, zda je vyžadována konkrétní konfigurace

---

## 4. Vyhodnocení zranitelnosti

### Evidence, že zařízení je zranitelné

Zařízení je pravděpodobně zranitelné, pokud:

* model `DCS-7150S-64-CL-F` je uveden mezi affected products
* verze `4.32.2F` je uvedena mezi vulnerable versions
* jsou splněny případné další podmínky z advisory

### Evidence, že zařízení není zranitelné

Zařízení pravděpodobně není zranitelné, pokud:

* model není mezi affected products
* verze je novější než fixed version
* není zapnutá požadovaná služba

### Evidence, která zatím chybí

* konkrétní advisory
* seznam affected versions
* informace, zda je aktivní potřebná služba / protokol

---

## 5. Návrh řešení

### Krátkodobé řešení

* omezit přístup k postižené službě
* použít ACL nebo firewall
* vypnout zranitelnou funkci
* naplánovat upgrade co nejdříve

### Dlouhodobé řešení

* zavést pravidelné sledování vendor advisories
* inventarizovat zařízení a verze OS
* pravidelně skenovat zranitelnosti
* mít patch management proces

### Preventivní opatření

Pokud zařízení aktuálně není zranitelné:

* nastavit monitoring nových advisories
* evidovat verze zařízení
* před upgradem ověřovat kompatibilitu a bezpečnostní opravy

---

# Part 2 – Další průzkum CVE

## 1. Rapid7 / Tenable / KEV

### Rapid7 a Tenable

Při hledání CVE je vhodné zkontrolovat:

* CVSS skóre
* detailnější popis útoku
* exploitability
* odkazy na workaround

### KEV – Known Exploited Vulnerabilities

Pokud by bylo CVE v KEV katalogu, znamenalo by to:

* zranitelnost je aktivně zneužívána
* priorita opravy by byla velmi vysoká
* zařízení by mělo být opraveno okamžitě

---

## 2. Druhé Arista advisory

> Opět chybí konkrétní odkaz. Po doplnění advisory zopakovat stejný postup.

### Zranitelné verze EOS

| Verze   | Stav       |
| ------- | ---------- |
| doplnit | vulnerable |
| doplnit | fixed      |

### Dotčený hardware

* doplnit

### Změna relevance údajů ze show version

Ve většině případů zůstává nejdůležitější:

* model zařízení
* Software image version

Další údaje mohou být relevantní pouze tehdy, pokud advisory pracuje s konkrétní architekturou, buildem nebo konfigurací.

### Doporučená akce

* ověřit verzi
* ověřit model
* provést upgrade na fix verzi
* pokud upgrade není možný, aplikovat mitigaci z advisory
