[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=22715135)
> ** Come leggere questa guida:** per visualizzare correttamente il contenuto di questo file, nell'Explorer di VS Code fai **tasto destro** su `README.md` e scegli **"Open Preview"**.

---

# Lezione Bash02 - Gestione dei file

## Obiettivo

In questa lezione imparerai a **visualizzare, copiare, spostare, eliminare file**, a usare i **caratteri jolly** per lavorare su più file contemporaneamente, e a collegare i comandi tra loro con **reindirizzamento** e **pipeline**. Alla fine sarai in grado di combinare questi strumenti per risolvere problemi reali dalla riga di comando.

---

## ⚠️ Prima di iniziare: crea l'ambiente

Apri il terminale e lancia lo script di setup per creare i file e le cartelle necessarie agli esercizi:

```bash
cd /workspaces/*Lezione_Bash02*
bash setup.sh
```

> **Nota:** il nome esatto della tua cartella potrebbe essere diverso da `Lezione_Bash02` (ad esempio `Lezione_Bash02-tuonome`). Il carattere jolly `*` nel comando `cd` seleziona automaticamente la cartella giusta — lo imparerai nel Blocco 5!

Se durante gli esercizi combini qualche guaio e vuoi ricominciare, puoi rilanciare lo script in qualsiasi momento: cancellerà tutto e ricreerà l'ambiente da zero.

---

## Blocco 1 - Visualizzare il contenuto dei file

### Obiettivo

Leggere il contenuto di un file di testo direttamente dal terminale, visualizzando tutto il file oppure solo le prime o ultime righe.

### Ingredienti

| Comando | Descrizione |
|---------|-------------|
| `cat <file>` | Stampa l'intero contenuto del file |
| `head <file>` | Mostra le prime 10 righe |
| `head -n <N> <file>` | Mostra le prime N righe |
| `tail <file>` | Mostra le ultime 10 righe |
| `tail -n <N> <file>` | Mostra le ultime N righe |
| `less <file>` | Apre il file in un visualizzatore scorrevole (esci con `q`) |

### Come combinarli

```bash
cat appunti_reti.txt                 # leggi tutto il file
head -n 5 appunti_reti.txt          # solo le prime 5 righe
tail -n 3 appunti_reti.txt          # solo le ultime 3 righe
less appunti_reti.txt               # scorri il file (frecce su/giù, q per uscire)
```

`cat` è perfetto per file corti. Per file lunghi usa `less`, che ti permette di scorrere avanti e indietro senza riempire il terminale.

### Esercizio 1.1

1. Vai nella cartella `esercizi/documenti`
2. Visualizza l'intero contenuto di `appunti_reti.txt`
3. Visualizza solo le prime 3 righe di `appunti_sicurezza.txt`
4. Visualizza solo le ultime 5 righe di `todo.txt`

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/documenti

cat appunti_reti.txt

head -n 3 appunti_sicurezza.txt
# Output:
# Sicurezza Informatica - Concetti Base
#
# La triade CIA:

tail -n 5 todo.txt
# Output:
# Scadenze:
# - Backend: 15 marzo
# - Frontend: 30 marzo
# - Consegna finale: 15 aprile
```

</details>

---

### Esercizio 1.2

1. Vai nella cartella `esercizi/log`
2. Visualizza le prime 5 righe di `server.log`
3. Visualizza le ultime 3 righe dello stesso file
4. Apri `accessi.log` con `less`, scorri il contenuto, poi esci

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/log

head -n 5 server.log
# Output:
# 2024-01-15 08:00:01 [INFO] Server avviato sulla porta 8080
# 2024-01-15 08:00:02 [INFO] Connessione al database stabilita
# 2024-01-15 08:05:15 [INFO] Richiesta GET /index.html - 200 OK
# 2024-01-15 08:05:16 [INFO] Richiesta GET /style.css - 200 OK
# 2024-01-15 08:10:30 [WARNING] Tentativo di accesso non autorizzato da 192.168.1.100

tail -n 3 server.log
# Output:
# 2024-01-15 10:00:00 [INFO] Server in fase di arresto
# 2024-01-15 10:00:01 [INFO] Connessione al database chiusa
# 2024-01-15 10:00:02 [INFO] Server arrestato correttamente

less accessi.log
# (scorri con le frecce, esci con q)
```

</details>

---

## Blocco 2 - Copiare file e directory

### Obiettivo

Creare copie di file e directory per avere un duplicato su cui lavorare senza modificare l'originale.

### Ingredienti

| Comando | Descrizione |
|---------|-------------|
| `cp <sorgente> <destinazione>` | Copia un file |
| `cp <file1> <file2> <directory>` | Copia più file in una directory |
| `cp -r <dir_sorgente> <dir_dest>` | Copia una directory e tutto il suo contenuto |

### Come combinarli

```bash
cp file.txt copia_file.txt           # copia con nuovo nome (stessa cartella)
cp file.txt /altra/cartella/         # copia in un'altra cartella (stesso nome)
cp file.txt /altra/cartella/nuovo.txt  # copia in un'altra cartella con nuovo nome
cp -r progetti/ backup_progetti/     # copia un'intera directory
```

**Attenzione:** se la destinazione esiste già, `cp` la sovrascrive **senza chiedere conferma**!

### Esercizio 2.1

1. Vai nella cartella `esercizi/documenti`
2. Crea una copia di `appunti_reti.txt` chiamata `appunti_reti_backup.txt`
3. Copia `todo.txt` nella cartella `esercizi/backup`
4. Verifica con `ls` che le copie esistano

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/documenti

cp appunti_reti.txt appunti_reti_backup.txt

cp todo.txt ../backup/

ls
# Output: appunti_database.txt  appunti_reti.txt  appunti_reti_backup.txt  appunti_sicurezza.txt  todo.txt

ls ../backup/
# Output: todo.txt
```

</details>

---

### Esercizio 2.2

1. Copia l'intera cartella `esercizi/progetti` dentro `esercizi/backup`
2. Verifica che la struttura sia stata copiata correttamente

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi

cp -r progetti/ backup/progetti

ls backup/
# Output: progetti  todo.txt

ls backup/progetti/
# Output: mobile  webapp

ls backup/progetti/webapp/
# Output: app.js  index.html  style.css
```

**Nota:** senza `-r` il comando fallirebbe con un errore, perché `cp` di default non copia le directory.

</details>

---

## Blocco 3 - Spostare e rinominare

### Obiettivo

Spostare file da una cartella all'altra e rinominarli. In Bash, spostare e rinominare sono la **stessa operazione**: il comando `mv`.

### Ingredienti

| Comando | Descrizione |
|---------|-------------|
| `mv <sorgente> <destinazione>` | Sposta o rinomina un file/directory |
| `mv <file1> <file2> <directory>` | Sposta più file in una directory |

### Come combinarli

```bash
mv vecchio.txt nuovo.txt              # rinomina (stessa cartella)
mv file.txt /altra/cartella/          # sposta (stesso nome)
mv file.txt /altra/cartella/nuovo.txt # sposta e rinomina
mv *.txt /cartella/                   # sposta tutti i .txt
```

**La differenza rispetto a `cp`:** dopo `mv` il file originale **non esiste più** nella posizione originale. Con `cp` invece l'originale resta al suo posto.

### Esercizio 3.1

1. Vai nella cartella `esercizi/documenti`
2. Rinomina `todo.txt` in `attivita.txt`
3. Verifica con `ls`
4. Sposta `attivita.txt` nella cartella `esercizi/archivio`
5. Verifica che il file non sia più in `documenti` e che sia in `archivio`

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/documenti

mv todo.txt attivita.txt

ls
# Output: appunti_database.txt  appunti_reti.txt  appunti_sicurezza.txt  attivita.txt

mv attivita.txt ../archivio/

ls
# Output: appunti_database.txt  appunti_reti.txt  appunti_sicurezza.txt
# (attivita.txt non c'è più)

ls ../archivio/
# Output: ... attivita.txt ... (insieme agli altri file dell'archivio)
```

</details>

---

### Esercizio 3.2

1. Vai nella cartella `esercizi/progetti/webapp`
2. Rinomina `app.js` in `main.js`
3. Sposta `style.css` nella cartella `esercizi/backup` rinominandolo `style_old.css` in un solo comando
4. Verifica i risultati

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/progetti/webapp

mv app.js main.js

mv style.css ../../backup/style_old.css

ls
# Output: index.html  main.js

ls ../../backup/
# Output: style_old.css  (e altri file se hai fatto gli esercizi precedenti)
```

**Nota:** `mv style.css ../../backup/style_old.css` sposta **e** rinomina in un solo passaggio.

</details>

---

## Blocco 4 - Eliminare file

### Obiettivo

Rimuovere file e directory in modo sicuro, con consapevolezza di cosa succede.

### Ingredienti

| Comando | Descrizione |
|---------|-------------|
| `rm <file>` | Elimina un file (irreversibile!) |
| `rm -i <file>` | Chiede conferma prima di eliminare |
| `rm -r <directory>` | Elimina una directory e tutto il suo contenuto |
| `rm -ri <directory>` | Elimina directory chiedendo conferma per ogni file |

### Come combinarli

```bash
rm file.txt                  # elimina senza chiedere
rm -i file_importante.txt    # chiede "remove file_importante.txt?" → rispondi y o n
rm -r cartella/              # elimina cartella e tutto il contenuto
```

**⚠️ Attenzione:** `rm` non ha un cestino! Una volta eliminato, il file è **perso per sempre**. Usa `-i` quando non sei sicuro.

### Esercizio 4.1

1. Vai nella cartella `esercizi/archivio`
2. Elimina il file `note.txt`
3. Elimina il file `readme.md` chiedendo conferma (rispondi `y`)
4. Verifica con `ls` che siano stati eliminati

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/archivio

rm note.txt

rm -i readme.md
# Output: rm: remove regular empty file 'readme.md'? y

ls
# Output: (note.txt e readme.md non ci sono più)
```

</details>

---

### Esercizio 4.2

> **Nuovo comando:** `touch <file>` crea un file vuoto. Se il file esiste già, ne aggiorna la data di modifica senza cambiarne il contenuto.

1. Crea una directory temporanea `esercizi/temp` con dentro due file (`a.txt` e `b.txt`)
2. Elimina l'intera directory `temp` con un solo comando
3. Verifica che sia stata rimossa

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi

mkdir temp
touch temp/a.txt temp/b.txt

rm -r temp

ls
# Output: (temp non c'è più)
```

**Nota:** `rm -r` è potente e pericoloso. Controlla sempre il percorso prima di premere Invio!

</details>

---

## Blocco 5 - Caratteri jolly (wildcards)

### Obiettivo

Selezionare più file contemporaneamente usando dei pattern, senza doverli elencare uno per uno.

### Ingredienti

| Wildcard | Significato | Esempio |
|----------|-------------|---------|
| `*` | Qualsiasi sequenza di caratteri (anche vuota) | `*.txt` → tutti i file .txt |
| `?` | Esattamente un carattere qualsiasi | `file?.txt` → file1.txt, fileA.txt |
| `[...]` | Uno dei caratteri tra parentesi | `file[123].txt` → file1.txt, file2.txt, file3.txt |
| `[!...]` | Qualsiasi carattere **tranne** quelli tra parentesi | `file[!0-9].txt` → fileA.txt, ma non file1.txt |

### Come combinarli

```bash
ls *.txt                    # tutti i file che finiscono con .txt
ls foto_*                   # tutti i file che iniziano con foto_
ls *.jpg *.png              # tutti i file .jpg e .png
ls documento_???.pdf        # documento_ seguito da esattamente 3 caratteri, poi .pdf
ls foto_*_202[34].jpg       # foto del 2023 o 2024
```

Le wildcards funzionano con qualsiasi comando: `ls`, `cp`, `mv`, `rm`, `cat`, ecc.

### Esercizio 5.1

1. Vai nella cartella `esercizi/archivio`
2. Elenca solo i file `.jpg`
3. Elenca solo i file `.pdf`
4. Elenca tutti i file che contengono `2024` nel nome

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/archivio

ls *.jpg
# Output: foto_milano_2023.jpg  foto_napoli_2024.jpg  foto_roma_2023.jpg  foto_roma_2024.jpg

ls *.pdf
# Output: documento_febbraio.pdf  documento_gennaio.pdf  documento_marzo.pdf

ls *2024*
# Output: budget_2024.xlsx  foto_napoli_2024.jpg  foto_roma_2024.jpg
```

</details>

---

### Esercizio 5.2

1. Resta nella cartella `esercizi/archivio`
2. Copia tutti i file `.jpg` nella cartella `esercizi/backup`
3. Elenca tutti i file che iniziano con `relazione`
4. Elenca tutti i file `.xlsx` e `.docx` (due pattern in un solo comando `ls`)

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/archivio

cp *.jpg ../backup/

ls ../backup/
# Output: foto_milano_2023.jpg  foto_napoli_2024.jpg  foto_roma_2023.jpg  foto_roma_2024.jpg  (e altri file precedenti)

ls relazione*
# Output: relazione_finale.docx  relazione_intermedia.docx

ls *.xlsx *.docx
# Output: budget_2023.xlsx  budget_2024.xlsx  relazione_finale.docx  relazione_intermedia.docx
```

</details>

---

### Esercizio 5.3

1. Elenca le foto di Roma (qualsiasi anno)
2. Elenca i file `budget` del 2023 o 2024 usando le parentesi quadre
3. Elenca tutti i file `documento_` che hanno esattamente 7 lettere dopo l'underscore prima di `.pdf` (suggerimento: usa `?`)

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
ls foto_roma*
# Output: foto_roma_2023.jpg  foto_roma_2024.jpg

ls budget_202[34].xlsx
# Output: budget_2023.xlsx  budget_2024.xlsx

ls documento_???????.pdf
# Output: documento_gennaio.pdf  documento_febbraio.pdf
# (documento_marzo.pdf ha solo 5 lettere dopo _ quindi non compare)
```

**Spiegazione:** `documento_???????.pdf` richiede esattamente 7 caratteri tra `documento_` e `.pdf`. "gennaio" e "febbraio" hanno 7 lettere, "marzo" ne ha 5 e non corrisponde.

</details>

---

## Blocco 6 - Reindirizzamento

### Obiettivo

Salvare l'output di un comando in un file, oppure usare un file come input per un comando, invece di lavorare solo sullo schermo.

### Ingredienti

| Operatore / Comando | Descrizione |
|-----------|-------------|
| `echo <testo>` | Stampa una riga di testo sul terminale |
| `>` | Redirige l'output in un file (**sovrascrive** se esiste) |
| `>>` | Redirige l'output in un file (**aggiunge in coda** se esiste) |
| `<` | Usa un file come input per un comando |

### Come combinarli

```bash
ls > elenco.txt              # salva l'elenco dei file in elenco.txt
echo "ciao" > saluto.txt     # scrive "ciao" in saluto.txt
echo "mondo" >> saluto.txt   # aggiunge "mondo" a saluto.txt (senza cancellare "ciao")
cat < saluto.txt             # legge saluto.txt come input di cat
```

**Differenza fondamentale:**
- `>` **cancella** il contenuto precedente del file e lo riscrive
- `>>` **aggiunge** alla fine del file, senza toccare il contenuto precedente

### Esercizio 6.1

1. Vai nella cartella `esercizi/sandbox`
2. Crea un file `frutti.txt` che contenga la parola "mela" usando `echo` e `>`
3. Aggiungi "banana" al file usando `>>`
4. Aggiungi "arancia" al file usando `>>`
5. Visualizza il contenuto del file con `cat`

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/sandbox

echo "mela" > frutti.txt
echo "banana" >> frutti.txt
echo "arancia" >> frutti.txt

cat frutti.txt
# Output:
# mela
# banana
# arancia
```

</details>

---

### Esercizio 6.2

1. Vai nella cartella `esercizi/archivio`
2. Salva l'elenco di tutti i file `.jpg` in un file chiamato `elenco_foto.txt` nella cartella `sandbox`
3. Aggiungi allo stesso file l'elenco dei file `.pdf`
4. Visualizza il contenuto di `elenco_foto.txt`

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/archivio

ls *.jpg > ../sandbox/elenco_foto.txt
ls *.pdf >> ../sandbox/elenco_foto.txt

cat ../sandbox/elenco_foto.txt
# Output:
# foto_milano_2023.jpg
# foto_napoli_2024.jpg
# foto_roma_2023.jpg
# foto_roma_2024.jpg
# documento_febbraio.pdf
# documento_gennaio.pdf
# documento_marzo.pdf
```

</details>

---

### Esercizio 6.3

1. Vai nella cartella `esercizi/log`
2. Salva le prime 5 righe di `server.log` in un file `log_estratto.txt` nella cartella `sandbox`
3. Aggiungi le ultime 3 righe di `server.log` allo stesso file
4. Visualizza `log_estratto.txt`

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/log

head -n 5 server.log > ../sandbox/log_estratto.txt
tail -n 3 server.log >> ../sandbox/log_estratto.txt

cat ../sandbox/log_estratto.txt
# Output:
# 2024-01-15 08:00:01 [INFO] Server avviato sulla porta 8080
# 2024-01-15 08:00:02 [INFO] Connessione al database stabilita
# 2024-01-15 08:05:15 [INFO] Richiesta GET /index.html - 200 OK
# 2024-01-15 08:05:16 [INFO] Richiesta GET /style.css - 200 OK
# 2024-01-15 08:10:30 [WARNING] Tentativo di accesso non autorizzato da 192.168.1.100
# 2024-01-15 10:00:00 [INFO] Server in fase di arresto
# 2024-01-15 10:00:01 [INFO] Connessione al database chiusa
# 2024-01-15 10:00:02 [INFO] Server arrestato correttamente
```

</details>

---

## Blocco 7 - Pipeline

### Obiettivo

Collegare l'output di un comando all'input del successivo, creando catene di comandi potenti. È il superpotere della riga di comando.

### Ingredienti

| Operatore/Comando | Descrizione |
|-----------|-------------|
| `\|` | Collega l'output di un comando all'input del successivo |
| `grep <pattern>` | Filtra le righe che contengono il pattern |
| `wc -l` | Conta il numero di righe |
| `sort` | Ordina le righe alfabeticamente |
| `uniq` | Rimuove le righe duplicate consecutive (da usare dopo `sort`) |

### Come combinarli

```bash
cat file.txt | grep "errore"           # mostra solo le righe che contengono "errore"
ls | wc -l                             # conta quanti file ci sono
cat log.txt | grep "ERROR" | wc -l     # conta quante righe di errore ci sono
cat nomi.txt | sort                    # ordina i nomi alfabeticamente
cat nomi.txt | sort | uniq             # ordina e rimuovi duplicati
```

La pipeline è come una catena di montaggio: ogni comando prende il risultato del precedente, ci lavora sopra, e lo passa al successivo.

### Esercizio 7.1

1. Vai nella cartella `esercizi/log`
2. Mostra solo le righe di `server.log` che contengono `ERROR`
3. Conta quante righe contengono `WARNING`
4. Mostra le righe che contengono `INFO` e salvale in un file `solo_info.txt` nella cartella `sandbox`

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/log

cat server.log | grep "ERROR"
# Output:
# 2024-01-15 08:20:45 [ERROR] Connessione al database persa
# 2024-01-15 08:20:46 [ERROR] Timeout nella riconnessione al database
# 2024-01-15 08:45:10 [ERROR] File non trovato: /images/logo.png - 404
# 2024-01-15 09:45:00 [ERROR] Impossibile inviare email di notifica

cat server.log | grep "WARNING" | wc -l
# Output: 3

cat server.log | grep "INFO" > ../sandbox/solo_info.txt
cat ../sandbox/solo_info.txt
# (mostra tutte le righe con [INFO])
```

</details>

---

### Esercizio 7.2

1. Vai nella cartella `esercizi/log`
2. Dal file `accessi.log`, mostra solo i login falliti
3. Conta quanti login di successo ci sono
4. Estrai tutti gli utenti che hanno fatto login (successo o fallito), ordinali e rimuovi i duplicati

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi/log

cat accessi.log | grep "fallito"
# Output:
# 2024-01-15 08:10:30 admin login fallito 192.168.1.100
# 2024-01-15 08:10:31 admin login fallito 192.168.1.100
# 2024-01-15 08:35:00 guest login fallito 192.168.1.50

cat accessi.log | grep "successo" | wc -l
# Output: 5

cat accessi.log | grep "login" | awk '{print $3}' | sort | uniq
# Output:
# admin
# anna.verdi
# guest
# luca.bianchi
# mario.rossi
# sara.neri
```

**Nota sull'ultimo comando:** `awk '{print $3}'` estrae la terza colonna (il nome utente). È un comando avanzato che vedrai nelle prossime lezioni. Per ora nota come la pipeline permette di concatenare operazioni complesse!

</details>

---

### Esercizio 7.3

1. Conta quanti file `.jpg` ci sono nella cartella `esercizi/archivio` (usa `ls` e `wc`)
2. Cerca in `esercizi/documenti/appunti_reti.txt` tutte le righe che contengono la parola "livello"
3. Conta quante volte compare la parola "database" nel file `esercizi/log/server.log` (quante righe la contengono)

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
ls /workspaces/*Lezione_Bash02*/esercizi/archivio/*.jpg | wc -l
# Output: 4

cat /workspaces/*Lezione_Bash02*/esercizi/documenti/appunti_reti.txt | grep "livello"
# Output:
# Ogni livello comunica solo con il livello adiacente.

grep "database" /workspaces/*Lezione_Bash02*/esercizi/log/server.log | wc -l
# Output: 4
```

**Nota:** `grep` può ricevere il file direttamente come argomento, senza bisogno di `cat |`. Entrambe le forme sono corrette:
- `cat file.txt | grep "parola"`
- `grep "parola" file.txt`

</details>

---

## Esercizi extra

### Extra 1 - Backup selettivo

Copia tutti i file di testo (`.txt`) dalla cartella `documenti` nella cartella `backup`, poi verifica il contenuto di `backup`.

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi

cp documenti/*.txt backup/

ls backup/
# Output: (tutti i file .txt copiati, più eventuali file precedenti)
```

</details>

---

### Extra 2 - Analisi dei log

In un solo comando (usando pipeline), conta quante righe di `accessi.log` riguardano l'indirizzo IP `192.168.1.100`.

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
grep "192.168.1.100" /workspaces/*Lezione_Bash02*/esercizi/log/accessi.log | wc -l
# Output: 4
```

</details>

---

### Extra 3 - Creare un report

Crea un file `report.txt` nella cartella `sandbox` che contenga, nell'ordine:
1. La scritta "=== REPORT ===" 
2. L'elenco dei file nella cartella `archivio`
3. Una riga vuota
4. Le prime 3 righe di `server.log`

Usa solo `echo`, `ls`, `head` e i reindirizzamenti `>` e `>>`.

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi

echo "=== REPORT ===" > sandbox/report.txt
ls archivio/ >> sandbox/report.txt
echo "" >> sandbox/report.txt
head -n 3 log/server.log >> sandbox/report.txt

cat sandbox/report.txt
# Output:
# === REPORT ===
# budget_2023.xlsx
# budget_2024.xlsx
# documento_febbraio.pdf
# documento_gennaio.pdf
# documento_marzo.pdf
# ...
#
# 2024-01-15 08:00:01 [INFO] Server avviato sulla porta 8080
# 2024-01-15 08:00:02 [INFO] Connessione al database stabilita
# 2024-01-15 08:05:15 [INFO] Richiesta GET /index.html - 200 OK
```

</details>

---

### Extra 4 - Indagine di sicurezza

Analizzando `accessi.log`:
1. Trova tutti i tentativi di login falliti
2. Conta quanti sono
3. Salva i risultati in un file `tentativi_falliti.txt` nella cartella `sandbox`

<details>
<summary>Solo dopo aver svolto l'esercizio, apri qui per vedere la soluzione</summary>

```bash
cd /workspaces/*Lezione_Bash02*/esercizi

grep "fallito" log/accessi.log > sandbox/tentativi_falliti.txt

echo "---" >> sandbox/tentativi_falliti.txt
echo -n "Totale tentativi falliti: " >> sandbox/tentativi_falliti.txt
grep "fallito" log/accessi.log | wc -l >> sandbox/tentativi_falliti.txt

cat sandbox/tentativi_falliti.txt
# Output:
# 2024-01-15 08:10:30 admin login fallito 192.168.1.100
# 2024-01-15 08:10:31 admin login fallito 192.168.1.100
# 2024-01-15 08:35:00 guest login fallito 192.168.1.50
# ---
# Totale tentativi falliti: 3
```

</details>

---

## Riepilogo comandi

| Comando | Descrizione |
|---------|-------------|
| `cat <file>` | Visualizza l'intero contenuto di un file |
| `head -n N <file>` | Mostra le prime N righe |
| `tail -n N <file>` | Mostra le ultime N righe |
| `less <file>` | Visualizzatore scorrevole (esci con `q`) |
| `cp <src> <dest>` | Copia un file |
| `cp -r <src> <dest>` | Copia una directory ricorsivamente |
| `mv <src> <dest>` | Sposta o rinomina |
| `rm <file>` | Elimina un file |
| `rm -i <file>` | Elimina con conferma |
| `rm -r <dir>` | Elimina directory e contenuto |
| `touch <file>` | Crea un file vuoto |
| `echo <testo>` | Stampa una riga di testo |
| `grep <pattern> <file>` | Filtra righe che contengono il pattern |
| `wc -l` | Conta le righe |
| `sort` | Ordina le righe |
| `uniq` | Rimuove duplicati consecutivi |

### Operatori

| Operatore | Descrizione |
|-----------|-------------|
| `>` | Redirige output in file (sovrascrive) |
| `>>` | Redirige output in file (aggiunge) |
| `<` | Usa file come input |
| `\|` | Pipeline: collega output → input |

### Wildcards

| Wildcard | Significato |
|----------|-------------|
| `*` | Qualsiasi sequenza di caratteri |
| `?` | Esattamente un carattere |
| `[...]` | Uno dei caratteri elencati |
| `[!...]` | Qualsiasi carattere tranne quelli elencati |