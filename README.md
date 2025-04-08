<?php
include 'header.php';
?>

<!DOCTYPE html>
<html lang="sk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jednoduchá kalkulačka</title>
    <script>
        function vypocitaj() {
            let vyraz = document.getElementById("vyraz").value;
            try {
                let vysledok = eval(vyraz);
                document.getElementById("vysledok").innerText = "Výsledok: " + vysledok;
                
                fetch("uloz_vypocet.php", {
                    method: "POST",
                    headers: { "Content-Type": "application/x-www-form-urlencoded" },
                    body: "vyraz=" + encodeURIComponent(vyraz) + "&vysledok=" + vysledok
                });
            } catch (e) {
                document.getElementById("vysledok").innerText = "Neplatný výraz!";
            }
        }
    </script>
</head>
<body>

    <form onsubmit="event.preventDefault(); vypocitaj();">
        <input type="text" id="vyraz" required placeholder="Zadajte výraz, napr. 5+3">
        <button type="submit">=</button>
    </form>
    
    <h2 id="vysledok"></h2>



</body>
</html>

<?php
include 'footer.php';
?>
