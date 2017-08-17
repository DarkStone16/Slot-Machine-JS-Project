<html lang="en">
    <head>

        <meta charset="UTF-8">
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
        <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
        <link rel="stylesheet" href="Styles/index2.css">
        <title>Machine à sous</title>

        <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
        <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous">
        </script>
        
    </head>

    <body>

        <div class="container">

            <div class="row">

                <div class="col-md-7">

                    <h1 id="first">Machine à sous en JS</h1>

                    <div class="lol">

                        <form onsubmit="cred(); return false;">

                            <br>

                            <table>

                                <td><img src="Images/0.png" id="slot1" width="100"></td>

                                <td><img src="Images/1.png" id="slot2" width="100"></td>

                                <td><img src="Images/2.png" id="slot3" width="100"></td>

                                <td><img src="Images/3.png" id="slot4" width="100"></td>

                            </table>
                            <br><br>

                            Crédits: <br><input id="credits" type="text" disabled="disabled"> <br><br>

                            Highscore: <br><input id="highscore" type="text" disabled="disabled"> <br><br><br>

                            <button type="submit">Jouer</button>

                            <br><br>

                        </form>    


                    </div>
                </div>

                <div class="col-md-5">

                    <br>

                    <span class="append"></span>

                </div>

            </div>

        </div>

        <script>

            //Déclaration d'un tableau
            var tabcarte = [0, 1, 2, 3];

            // Valeur initiale des crédits
            document.querySelector('#credits').value = 20;

            //Valeur highscore initiale
            document.querySelector('#highscore').value = document.querySelector('#credits').value;


            function cred() {

                //On regarde si le joueur possède des crédits, si oui on passe à l'étape suivante, sinon on affiche une alerte
                if (document.querySelector('#credits').value <= 0) {
                    alert("Crédits insuffisants pour continuer à jouer.");
                    return;
                }

                compt = 0;


                //On retire le crédit pour jouer
                document.querySelector('#credits').value--;

                //On lance la fonction suivante
                tourner();

            }

            function tourner(e) {

                //Animation en JS avec sélection d'une carte au hasard pour les 4 slots

                turns1 = Math.floor(Math.random() * 5);

                for (a = 0; a < turns1; a++) {
                    document.querySelector('#slot1').src = "Images/" + tabcarte[a] + ".png";
                }

                turns2 = Math.floor(Math.random() * 5);

                for (b = 0; b < turns2; b++) {
                    document.querySelector('#slot2').src = "Images/" + tabcarte[b] + ".png";
                }

                turns3 = Math.floor(Math.random() * 5);

                for (c = 0; c < turns3; c++) {
                    document.querySelector('#slot3').src = "Images/" + tabcarte[c] + ".png";
                }

                turns4 = Math.floor(Math.random() * 5);

                for (d = 0; d < turns4; d++) {
                    document.querySelector('#slot4').src = "Images/" + tabcarte[d] + ".png";
                }

                compt++;

                if (compt < 25) {
                    setTimeout("tourner(compt);", 50);
                } else {

                    //Fin de l'animation, on check les combinaisons obtenues


                    //Si les 4 symboles sont identiques, on obtient 5 crédits
                    if ((document.querySelector('#slot1').src == document.querySelector('#slot2').src) 
                        && (document.querySelector('#slot1').src == document.querySelector('#slot3').src) 
                        && (document.querySelector('#slot1').src == document.querySelector('#slot4').src)) 

                    {
                        document.querySelector('span.append').innerHTML = '4 symboles identiques - Vous avez gagné 5 crédits <br>' + document.querySelector('span.append').innerHTML;

                        document.querySelector('#credits').value = Math.floor(document.querySelector('#credits').value) + 5;
                    }


                    //Sinon, si 3 symboles sont identiques, on obtient 2 crédits
                    else if (((document.querySelector('#slot1').src == document.querySelector('#slot2').src) 
                              && (document.querySelector('#slot2').src == document.querySelector('#slot3').src)) 

                             ||((document.querySelector('#slot1').src == document.querySelector('#slot3').src) 
                              && (document.querySelector('#slot3').src == document.querySelector('#slot4').src)) 
                             
                             ||((document.querySelector('#slot2').src == document.querySelector('#slot3').src) 
                              && (document.querySelector('#slot3').src == document.querySelector('#slot4').src)) 
                             
                             ||((document.querySelector('#slot1').src == document.querySelector('#slot2').src) 
                              && (document.querySelector('#slot2').src == document.querySelector('#slot4').src))){

                        document.querySelector('span.append').innerHTML = '3 symboles identiques - Vous avez gagné 2 crédits <br>' + document.querySelector('span.append').innerHTML;

                        document.querySelector('#credits').value = Math.floor(document.querySelector('#credits').value) + 2;


                    }


                    //Sinon, il n'y a aucune combinaisons gagnantes
                    else {
                        document.querySelector('span.append').innerHTML = "Pas de combinaisons gagnantes - Vous avez perdu 1 crédit <br>" + document.querySelector('span.append').innerHTML;
                    }

                    //Si les crédits sont supérieurs au highscore, alors highscore prend la valeur de crédit
                    if(document.querySelector('#credits').value > document.querySelector('#highscore').value){
                        document.querySelector('#highscore').value = document.querySelector('#credits').value;
                    }

                }

            }

        </script>

    </body>

</html>
