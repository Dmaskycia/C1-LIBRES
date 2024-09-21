<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Calculadora de Puntuación para Opositores</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
            background-color: #f4f4f9;
        }

        label {
            margin-right: 10px;
        }

        input, button {
            margin-bottom: 20px;
        }

        button {
            cursor: pointer;
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
        }

        #result {
            margin-top: 20px;
            font-size: 20px;
        }

        .logo {
            background-color: red;
            color: white;
            padding: 10px;
            text-align: center;
            font-size: 24px;
        }

        img {
            height: 50px;
        }

        .bolsa-status {
            color: green;
        }

        .no-bolsa {
            color: red;
        }

        .congrats {
            color: blue;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="logo">
        <img src="13471.png" alt="Logo">
    </div>
    <h1>Calculadora de Puntuación para Opositores C1 ADMINISTRATIVO LIBRE , esta simulación puede contener errores y no tiene valor documental</h1>
    <form id="calculatorForm">
        <label for="correct1">Aciertos en la primera parte (70 preguntas):</label>
        <input type="number" id="correct1" required><br>

        <label for="wrong1">Errores en la primera parte:</label>
        <input type="number" id="wrong1" required><br>

        <label for="correct2">Aciertos en la segunda parte (30 preguntas):</label>
        <input type="number" id="correct2" required><br>

        <label for="wrong2">Errores en la segunda parte:</label>
        <input type="number" id="wrong2" required><br>

        <button type="button" onclick="calculateScore()">Calcular Nota y Elegibilidad para la Bolsa</button>
    </form>
    <div id="result"></div>

    <script>
        function calculateScore() {
            const correct1 = parseFloat(document.getElementById('correct1').value);
            const wrong1 = parseFloat(document.getElementById('wrong1').value);
            const correct2 = parseFloat(document.getElementById('correct2').value);
            const wrong2 = parseFloat(document.getElementById('wrong2').value);

            // Calculo para la primera parte (70 preguntas, vale 4 puntos)
            const penalties1 = wrong1 * (1/3);
            const netCorrect1 = correct1 - penalties1;
            const score1 = (netCorrect1 * 4) / 70;

            // Calculo para la segunda parte (30 preguntas, vale 4 puntos)
            const penalties2 = wrong2 * (1/3);
            const netCorrect2 = correct2 - penalties2;
            const score2 = (netCorrect2 * 4) / 30;

            // Puntuación total (suma de ambas partes)
            const totalCorrect = correct1 + correct2;
            const totalWrong = wrong1 + wrong2;
            const totalPenalties = totalWrong * (1/3);
            const totalNetCorrect = totalCorrect - totalPenalties;
            const adjustedTotalNetCorrect = Math.max(0, totalNetCorrect);
            const totalScore = score1 + score2; // Suma de las dos partes

            const resultDiv = document.getElementById('result');

            // El umbral para la bolsa es 1.2, que es el 30% de 4
            const isInBolsa = score1 >= 1.2;
            let bolsaStatus = isInBolsa ? 
                `<span class='bolsa-status'>Sí calificas para entrar en la bolsa con la nota de la primera parte.</span>` : 
                `<span class='no-bolsa'>No calificas para entrar en la bolsa con la nota de la primera parte.</span>`;
            
            let congratsMessage = totalScore > 4 ? `<div class='congrats'>¡Enhorabuena! Ha superado el ejercicio</div>` : '';

            resultDiv.innerHTML = `Tu puntuación en la primera parte es ${score1.toFixed(3)}, en la segunda parte es ${score2.toFixed(3)}, y tu puntuación total es ${totalScore.toFixed(4)}. ${bolsaStatus} ${congratsMessage}`;
        }
    </script>
</body>
</html>
