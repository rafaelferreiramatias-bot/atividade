<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de Alunos</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 30px;
        }

        input {
            display: block;
            margin-bottom: 10px;
            padding: 5px;
        }

        button {
            padding: 5px 15px;
            cursor: pointer;
        }

        li {
            margin-bottom: 10px;
        }

        .erro {
            color: red;
        }

        .sucesso {
            color: green;
        }
    </style>
</head>
<body>

    <h1>Cadastro de Alunos</h1>

    <form id="formulario" novalidate>

        <label for="nome">Nome:</label>
        <input type="text" id="nome" required>

        <label for="email">E-mail:</label>
        <input type="email" id="email" required>

        <label for="ra">Registro Acadêmico (6 números):</label>
        <input type="text" id="ra" inputmode="numeric"
               pattern="[0-9]{6}" maxlength="6" required>

        <label for="telefone">Telefone:</label>
        <input type="tel" id="telefone"
               placeholder="00 0000-0000"
               pattern="[0-9]{2} [0-9]{5}-[0-9]{4}" required>

        <button type="submit">Enviar</button>
    </form>

    <p id="mensagem" aria-live="polite"></p>

    <h2>Alunos Cadastrados</h2>
    <ol id="listaAlunos"></ol>

    <script>
        let alunos = [];

        const formulario = document.getElementById("formulario");
        const lista = document.getElementById("listaAlunos");
        const mensagem = document.getElementById("mensagem");
        const emailCampo = document.getElementById("email");
        const raCampo = document.getElementById("ra");
        const telefoneCampo = document.getElementById("telefone");

        formulario.addEventListener("submit", function(event) {
            event.preventDefault();

            let nome = document.getElementById("nome").value.trim();
            let email = emailCampo.value.trim();
            let ra = raCampo.value.trim();
            let telefone = telefoneCampo.value.trim();

            if (nome === "" || email === "" || ra === "" || telefone === "") {
                mensagem.textContent = "Erro: preencha todos os campos.";
                mensagem.className = "erro";

            } else if (nome.length < 3) {
                mensagem.textContent = "Erro: o nome deve ter pelo menos 3 caracteres.";
                mensagem.className = "erro";

            } else if (!emailCampo.checkValidity()) {
                mensagem.textContent = "Erro: digite um e-mail válido.";
                mensagem.className = "erro";

            } else if (!raCampo.checkValidity()) {
                mensagem.textContent = "Erro: o RA deve conter exatamente 6 números.";
                mensagem.className = "erro";

            } else if (!telefoneCampo.checkValidity()) {
                mensagem.textContent = "Erro: use o formato 00 0000-0000.";
                mensagem.className = "erro";

            } else {
                let aluno = {
                    nome: nome,
                    email: email,
                    ra: ra,
                    telefone: telefone
                };

                alunos.push(aluno);

                let item = document.createElement("li");
                item.textContent = nome + " - " + email +
                    " - RA: " + ra + " - Telefone: " + telefone;

                lista.appendChild(item);

                mensagem.textContent = "Aluno cadastrado com sucesso!";
                mensagem.className = "sucesso";

                console.log(alunos);

                formulario.reset();
            }
        });
    </script>

</body>
</html>
