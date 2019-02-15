# mySQL Workbench:
- Lag en tabell som heter 'Bestilling' med kolonnene 'Telefon', 'Navn', 'Burger', 'Drikke'. 
- Husk at databasen din har feidenavnet ditt (ikke myDB)
- Generer SQL ved hjelp av File | Export | Forward Engineer (next, next).

# Adminer på webkode.skit.no:
- Lim inn generert SQL-kode
- Nå har du en tom tabell på databaseserveren din

# Lag index.php basert på denne: 
'''
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>forslag fra TJC</title>
</head>
<body>
    <h1>Mal for enklest mulig tilkobling av database</h1>

    <form action="index.php" method="post">
        <label for="navn">Navn: </label>
        <input type="text" name="navn" required><br>
        <label for="alder">Alder: </label>
        <input type="text" name="alder" required><br>
        <button type="submit" name="sendknapp">Send data og lagre i databse</button>
    </form>

    <?php
        if(isset($_POST['navn']) && isset($_POST['navn'])){ //eller isset($_POST['sendknapp'])
            $navn = $_POST['navn'];
            $alder = $_POST['alder'];

            echo "<h2>Følgende data vil lagre i databasen:</h2>";
            echo "Navn: " . $navn . "<br>";
            echo "Alder: " . $alder . "<br>";


            //----------------------------------------------
            // Kode som lagrer data fra skjema i en databse
            // Koden er basert på eksempelet til Bitjungle
            //----------------------------------------------


            // Informasjon for å koble seg til DB
            $db_host = 'localhost'; 
            $db_navn = 'feidebruker';
            $db_bruker = 'feidebruker';
            $db_pass = '******** *** ********'; //NB NB NB!!!                                                        NB NB NB!!!
        
            //Vi forsøker først å opprette forbindelsen med databasen.
            //Se https://secure.php.net/manual/en/function.mysqli-connect.php
            $db_forbindelse = mysqli_connect($db_host, $db_bruker, $db_pass, $db_navn);
            //Vi sjekker om forbindelsen ble opprettet
            if (mysqli_connect_errno()) {
            die('Kunne ikke opprette forbindelse med databasen: ' . mysqli_connect_error()) ;
            }

            //Nå lager vi SQL-spørringen som skal kjøres (INSERT INTO...), og så
            //kjører vi den i databasen som vi har opprettet en forbindelse til.
            //Se https://secure.php.net/manual/en/mysqli.query.php
            $spørring = "INSERT INTO person(navn, alder) VALUES ('{$navn}', '{$alder}');";
            mysqli_query($db_forbindelse, $spørring);

            //Nå er vi ferdig, og kan lukke forbindelsen til databasen
            mysqli_close($db_forbindelse);
        }
        else{
            echo "Du må fylle ut alle felt!";
        }
        
    ?>
</body>
</html>
'''

# Når du nå fyller ut bestillingsskjemaet skal databasen din fylles opp av bestillinger. 
