<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Painel Principal - Chat</title>
    <style>
        /* === ADICIONANDO O MESMO DEGRADÊ NO FUNDO === */
        
        * { box-sizing: border-box; font-family: Arial, sans-serif; }
        
        body { 
            /* Mesmo degradê da tela de login para consistência */
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%) no-repeat;
            margin: 0; 
            padding: 20px; 
            display: flex; 
            justify-content: center; 
            background-size: cover; 
            height: 100vh;
        }
        
        /* === MANTENDO O RESTO EXATAMENTE IGUAL === */

        .chat-container {
            width: 100%;
            max-width: 500px;
            /* Fundo branco transparente para deixar o degradê aparecer um pouco */
            background: rgba(255, 255, 255, 0.95); 
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2); /* Sombra mais visível */
            display: flex;
            flex-direction: column;
            height: 80vh;
            overflow: hidden; /* Mantém os cantos arredondados */
        }

        .chat-header {
            background-color: #007bff; /* Mantém a cor original */
            color: white;
            padding: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .chat-header h3 { margin: 0; font-size: 18px; }
        .chat-header button {
            background: #dc3545;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 4px;
            cursor: pointer;
            transition: background 0.3s;
        }
        .chat-header button:hover { background: #a71d2a; }

        .chat-messages {
            flex: 1;
            padding: 15px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 10px;
            background-color: #f8f9fa; /* Um cinza muito leve para as mensagens flutuarem */
        }

        .message {
            background: white;
            padding: 10px;
            border-radius: 8px;
            max-width: 80%;
            word-wrap: break-word;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05); /* Sombra leve nas mensagens */
        }

        .message strong {
            display: block;
            font-size: 12px;
            color: #555;
            margin-bottom: 3px;
        }

        .chat-input {
            display: flex;
            padding: 10px;
            border-top: 1px solid #ddd;
            background: white; /* Garante que o input tenha fundo branco */
        }

        .chat-input input {
            flex: 1;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            outline: none;
        }

        .chat-input button {
            padding: 10px 15px;
            background-color: #007bff; /* Mantém a cor original */
            color: white;
            border: none;
            border-radius: 4px;
            margin-left: 8px;
            cursor: pointer;
            transition: background 0.3s;
        }
        .chat-input button:hover { background-color: #0056b3; }

    </style>
</head>
<body>

<div class="chat-container">
    <div class="chat-header">
        <h3>Sala de Bate-papo</h3>
        <button onclick="sair()">Sair</button>
    </div>

    <div class="chat-messages" id="mensagensContainer">
        <!-- Mensagens aparecerão aqui -->
    </div>

    <form class="chat-input" id="formChat">
        <input type="text" id="inputMensagem" placeholder="Digite sua mensagem..." required autocomplete="off">
        <button type="submit">Enviar</button>
    </form>
</div>

<script>
    // Mesma lógica do chat
    const usuario = localStorage.getItem("usuarioLogado");
    if (!usuario) {
        window.location.href = "index.html"; 
    }

    const formChat = document.getElementById('formChat');
    const inputMensagem = document.getElementById('inputMensagem');
    const mensagensContainer = document.getElementById('mensagensContainer');

    function adicionarMensagem(autor, texto) {
        const msgDiv = document.createElement('div');
        msgDiv.classList.add('message');
        msgDiv.innerHTML = `<strong>${autor}</strong> ${texto}`;
        mensagensContainer.appendChild(msgDiv);
        mensagensContainer.scrollTop = mensagensContainer.scrollHeight;
    }

    formChat.addEventListener('submit', function(e) {
        e.preventDefault();
        const texto = inputMensagem.value.trim();
        if (texto !== "") {
            adicionarMensagem(usuario, texto);
            inputMensagem.value = "";
        }
    });

    function sair() {
        localStorage.removeItem("usuarioLogado");
        window.location.href = "index.html";
    }
</script>

</body>
</html>
