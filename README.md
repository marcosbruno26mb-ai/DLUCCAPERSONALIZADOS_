<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Papelaria D'Lucca - Orçamento Online</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; padding: 10px; background: #faf8f5; color: #333; }
        .container { max-width: 500px; margin: auto; background: white; padding: 20px; border-radius: 25px; box-shadow: 0 10px 25px rgba(184,134,11,0.2); border-top: 10px solid #b8860b; }
        
        .logo-container { text-align: center; margin-bottom: 15px; }
        .logo-img { width: 140px; height: auto; border-radius: 15px; border: 2px solid #b8860b; }

        .header { text-align: center; margin-bottom: 25px; }
        .header h1 { color: #b8860b; margin: 0; font-size: 1.6em; text-transform: uppercase; }
        .header p { font-weight: bold; color: #5d4037; margin-top: 5px; }

        /* GRID DE PRODUTOS */
        .grid-produtos { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 30px; }
        .card-produto { background: #fff; border: 1px solid #eee; border-radius: 15px; padding: 10px; text-align: center; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .foto-produto { width: 100%; height: 140px; border-radius: 10px; object-fit: cover; background: #f9f9f9; margin-bottom: 10px; }
        .nome-produto { font-weight: bold; font-size: 0.9em; display: block; margin-bottom: 5px; color: #5d4037; height: 35px; overflow: hidden; }
        .preco-produto { color: #556b2f; font-weight: bold; display: block; margin-bottom: 10px; }
        
        .btn-add { background: #556b2f; color: white; border: none; width: 100%; padding: 10px; border-radius: 10px; cursor: pointer; font-weight: bold; font-size: 0.8em; transition: 0.2s; }
        .btn-add:active { transform: scale(0.9); }

        /* SEÇÃO DE ORÇAMENTO */
        .form-section { background: #fffcf0; padding: 15px; border-radius: 15px; border: 1px solid #d2b48c; }
        .form-section h3 { color: #b8860b; text-align: center; margin-top: 0; }
        label { font-weight: bold; display: block; margin-top: 10px; font-size: 0.8em; color: #b8860b; }
        input, textarea { width: 100%; padding: 12px; margin-top: 5px; border: 1px solid #d2b48c; border-radius: 8px; box-sizing: border-box; font-family: inherit; }
        
        .resumo { margin-top: 15px; font-size: 0.85em; background: white; padding: 10px; border-radius: 8px; border: 1px solid #eee; }
        .item-resumo { display: flex; justify-content: space-between; padding: 5px 0; border-bottom: 1px solid #f9f9f9; }
        .total-box { text-align: right; font-size: 1.3em; color: #b8860b; font-weight: bold; margin-top: 15px; }
        
        .btn-enviar { background: #25d366; color: white; border: none; width: 100%; padding: 18px; border-radius: 12px; font-size: 1.1em; font-weight: bold; cursor: pointer; margin-top: 15px; box-shadow: 0 5px 10px rgba(37,211,102,0.2); }
    </style>
</head>
<body>

<div class="container">
    <div class="logo-container">
        <img src="https://i.ibb.co/Vgn2bJg/b95e3479-ca56-4c91-ab3b-9e42502f9011.png" alt="Papelaria D'Lucca" class="logo-img">
    </div>

    <div class="header">
        <h1>Papelaria D'Lucca</h1>
        <p>Personalizados</p>
    </div>
    
    <div class="grid-produtos">
        <div class="card-produto">
            <img src="https://i.ibb.co/YyYfP70/1001061216.jpg" class="foto-produto">
            <span class="nome-produto">Maletinha</span>
            <span class="preco-produto">R$ 2,99</span>
            <button class="btn-add" onclick="adicionar('Maletinha', 2.99)">ADICIONAR</button>
        </div>

        <div class="card-produto">
            <img src="https://i.ibb.co/YyYfP70/1001061216.jpg" class="foto-produto">
            <span class="nome-produto">Caixa Xuxinha</span>
            <span class="preco-produto">R$ 2,99</span>
            <button class="btn-add" onclick="adicionar('Caixa Xuxinha', 2.99)">ADICIONAR</button>
        </div>

        <div class="card-produto">
            <img src="https://i.ibb.co/YyYfP70/1001061216.jpg" class="foto-produto">
            <span class="nome-produto">Triângulo</span>
            <span class="preco-produto">R$ 2,99</span>
            <button class="btn-add" onclick="adicionar('Triângulo', 2.99)">ADICIONAR</button>
        </div>

        <div class="card-produto">
            <img src="https://i.ibb.co/17Rz8P0/1001061215.jpg" class="foto-produto">
            <span class="nome-produto">Triângulo 3D</span>
            <span class="preco-produto">R$ 3,50</span>
            <button class="btn-add" onclick="adicionar('Triângulo 3D', 3.50)">ADICIONAR</button>
        </div>
    </div>

    <div class="form-section">
        <h3>📍 Finalizar Orçamento</h3>
        <label>Seu Nome:</label>
        <input type="text" id="cliente_nome" placeholder="Digite seu nome completo">

        <label>Endereço / Retirada:</label>
        <input type="text" id="cliente_endereco" placeholder="Onde entregar ou Retirar?">

        <label>🎨 Detalhes da Personalização:</label>
        <textarea id="observacoes" placeholder="Nomes, temas, cores desejadas..."></textarea>

        <div id="resumo-itens" class="resumo">Nenhum item selecionado.</div>
        <div class="total-box">Total: R$ <span id="valor-total">0.00</span></div>

        <button class="btn-enviar" onclick="enviarWhatsApp()">🚀 Enviar para D'LUCCA</button>
    </div>
</div>

<script>
    let carrinho = [];
    let total = 0;
    // SEU NÚMERO ATUALIZADO:
    const MEU_WHATS = "5592994621099"; 

    function adicionar(nome, preco) {
        carrinho.push({nome, preco});
        total += preco;
        renderizar();
    }

    function remover(index) {
        total -= carrinho[index].preco;
        carrinho.splice(index, 1);
        renderizar();
    }

    function renderizar() {
        const div = document.getElementById('resumo-itens');
        if (carrinho.length === 0) {
            div.innerHTML = "Nenhum item selecionado.";
            total = 0;
        } else {
            div.innerHTML = "<b>Itens no Orçamento:</b><br>";
            carrinho.forEach((item, index) => {
                div.innerHTML += `<div class="item-resumo">${item.nome} <span onclick="remover(${index})" style="color:#d32f2f; cursor:pointer; font-weight:bold;">[X]</span></div>`;
            });
        }
        document.getElementById('valor-total').innerText = Math.abs(total).toFixed(2);
    }

    function enviarWhatsApp() {
        const nome = document.getElementById('cliente_nome').value;
        const endereco = document.getElementById('cliente_endereco').value;
        const obs = document.getElementById('observacoes').value;

        if (!nome || carrinho.length === 0) {
            alert("Por favor, preencha seu nome e escolha os itens!");
            return;
        }

        let msg = `*SOLICITAÇÃO DE ORÇAMENTO - PAPELARIA D'LUCCA* 🎨%0A%0A`;
        msg += `*Cliente:* ${nome}%0A`;
        msg += `*Entrega/Retirada:* ${endereco}%0A%0A`;
        msg += `*ITENS ESCOLHIDOS:*%0A`;
        
        carrinho.forEach(i => {
            msg += `- ${i.nome} (R$ ${i.preco.toFixed(2)})%0A`;
        });

        if(obs.trim() !== "") {
            msg += `%0A*DETALHES DA PERSONALIZAÇÃO:*%0A_${obs}_%0A`;
        }

        msg += `%0A*TOTAL ESTIMADO: R$ ${total.toFixed(2)}*%0A%0A_Aguardando confirmação da D'Lucca!_`;

        window.open(`https://wa.me/${MEU_WHATS}?text=${msg}`);
    }
</script>

</body>
</html>
