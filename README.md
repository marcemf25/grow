<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Memotest Masculinidades</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
        .grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            width: 300px;
            margin: 20px auto;
        }
        .card {
            width: 100px;
            height: 100px;
            background-color: lightgray;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            border: 1px solid #333;
            font-size: 12px;
            text-align: center;
            padding: 5px;
            transition: background-color 0.3s ease;
        }
        .flipped {
            background-color: white;
        }
        .hidden {
            visibility: hidden;
        }
        .problema { background-color: #6ec2b7; }
        .desafio { background-color: #ed9045; }
        .oportunidad { background-color: #4f448a; color: white; }
    </style>
</head>
<body>
    <h1>REÚNE PROBLEMAS, DESAFÍOS Y OPORTUNIDADES. ¡A JUGAR!</h1>
    
    <div class="grid" id="gameBoard"></div>
    <script>
        const cardsData = [
            { type: "Problema", text: "Las resistencias al cambio dificultan la transformación hacia espacios laborales más equitativos." },
            { type: "Problema", text: "Los estereotipos de masculinidad limitan la participación de los hombres en temas de género y diversidad." },
            { type: "Desafío", text: "Generar espacios de sensibilización donde los hombres puedan reflexionar sobre su rol en la equidad de género." },
            { type: "Desafío", text: "Involucrar a los hombres como sujetos de género y agentes de cambio en sus ámbitos laborales." },
            { type: "Oportunidad", text: "Promover liderazgos masculinos comprometidos con la Diversidad, Equidad e Inclusión." },
            { type: "Oportunidad", text: "Crear entornos de trabajo más diversos y equitativos, fortaleciendo la convivencia y el bienestar organizacional." }
        ];
        
        let shuffledCards = [...cardsData, ...cardsData].sort(() => Math.random() - 0.5);
        let selectedCards = [];

        function createCard(data, index) {
            const card = document.createElement("div");
            card.classList.add("card", data.type.toLowerCase());
            card.dataset.index = index;
            card.dataset.type = data.type;
            card.innerHTML = "?";
            card.addEventListener("click", flipCard);
            return card;
        }
        
        function flipCard(event) {
            let card = event.target;
            let index = card.dataset.index;
            
            if (selectedCards.includes(card) || card.classList.contains("hidden")) return;
            
            card.classList.add("flipped");
            card.innerHTML = shuffledCards[index].text;
            selectedCards.push(card);
            
            if (selectedCards.length === 2) {
                setTimeout(checkMatch, 1000);
            }
        }
        
        function checkMatch() {
            if (selectedCards[0].dataset.type === selectedCards[1].dataset.type) {
                selectedCards.forEach(card => card.classList.add("hidden"));
            } else {
                selectedCards.forEach(card => {
                    card.classList.remove("flipped");
                    card.innerHTML = "?";
                });
            }
            selectedCards = [];
        }
        
        const gameBoard = document.getElementById("gameBoard");
        shuffledCards.forEach((data, index) => gameBoard.appendChild(createCard(data, index)));
    </script>
</body>
</html>
