Aqui está um código HTML/CSS completo para um site interativo de criação de roupas de festa com design automático.
```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Ateliê Glamour - Crie sua Roupa de Festa</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #0a0a0a 0%, #1a1a2e 100%);
            font-family: 'Poppins', 'Segoe UI', 'Montserrat', sans-serif;
            color: #f0f0f0;
            min-height: 100vh;
            padding: 2rem 1.5rem;
        }

        /* fundo com glitter sutil */
        body::before {
            content: "";
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: radial-gradient(circle at 20% 40%, rgba(255, 192, 203, 0.03) 1px, transparent 1px);
            background-size: 25px 25px;
            pointer-events: none;
            z-index: 0;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            position: relative;
            z-index: 2;
        }

        /* cabeçalho */
        .hero {
            text-align: center;
            margin-bottom: 3rem;
            position: relative;
        }

        .hero h1 {
            font-size: 3rem;
            background: linear-gradient(135deg, #ffffff, #e0b0ff, #ff99cc);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: -0.5px;
            text-shadow: 0 2px 10px rgba(0,0,0,0.3);
        }

        .hero p {
            font-size: 1.2rem;
            color: #cdcdcd;
            margin-top: 0.5rem;
            border-bottom: 2px solid rgba(192, 192, 192, 0.3);
            display: inline-block;
            padding-bottom: 0.5rem;
        }

        /* grid principal */
        .designer-grid {
            display: grid;
            grid-template-columns: 1fr 1.2fr;
            gap: 2rem;
            background: rgba(10, 10, 20, 0.55);
            backdrop-filter: blur(3px);
            border-radius: 2rem;
            padding: 2rem;
            border: 1px solid rgba(192, 192, 192, 0.25);
            box-shadow: 0 25px 40px rgba(0,0,0,0.5), inset 0 1px 1px rgba(255,255,255,0.1);
        }

        /* painel de controles */
        .controls-panel {
            background: rgba(0,0,0,0.6);
            border-radius: 1.5rem;
            padding: 1.8rem;
            border: 1px solid silver;
            box-shadow: 0 8px 20px rgba(0,0,0,0.4);
        }

        .controls-panel h2 {
            font-size: 1.8rem;
            font-weight: 600;
            background: linear-gradient(120deg, #fff, #e6b3d9);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            margin-bottom: 1.5rem;
            border-left: 5px solid #ff69b4;
            padding-left: 15px;
        }

        .grupo {
            margin-bottom: 1.8rem;
        }

        label {
            display: block;
            font-weight: 500;
            margin-bottom: 0.5rem;
            color: #f2f2f2;
            letter-spacing: 0.5px;
        }

        select, input[type="color"] {
            width: 100%;
            padding: 12px 15px;
            background: #1e1e2a;
            border: 1px solid #b0b0b0;
            border-radius: 40px;
            color: white;
            font-weight: 500;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        select:hover, input:hover {
            border-color: #ff99cc;
            box-shadow: 0 0 8px rgba(255,105,180,0.4);
        }

        .cor-row {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        .cor-row input {
            flex: 1;
        }
        .cor-row span {
            background: #2a2a35;
            padding: 6px 12px;
            border-radius: 30px;
            font-size: 0.85rem;
            font-family: monospace;
        }

        .detalhe-botoes {
            display: flex;
            gap: 12px;
            margin-top: 8px;
            flex-wrap: wrap;
        }
        .btn-det {
            background: rgba(50,50,70,0.9);
            border: 1px solid silver;
            padding: 8px 16px;
            border-radius: 50px;
            font-size: 0.85rem;
            font-weight: 500;
            color: #ffd9f0;
            cursor: pointer;
            transition: all 0.2s;
        }
        .btn-det:hover {
            background: #ff69b4;
            color: black;
            border-color: white;
            transform: scale(0.97);
        }

        .btn-criar {
            background: linear-gradient(95deg, #b13b6b, #ff80b3);
            width: 100%;
            border: none;
            padding: 14px;
            font-size: 1.2rem;
            font-weight: bold;
            color: white;
            border-radius: 60px;
            margin-top: 1rem;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
        }
        .btn-criar:hover {
            background: linear-gradient(95deg, #ff69b4, #ff4d8c);
            transform: scale(1.01);
            letter-spacing: 1px;
        }

        /* área de exibição da roupa */
        .visual-area {
            background: #0f0f17cc;
            border-radius: 1.5rem;
            backdrop-filter: blur(4px);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 1rem;
            border: 1px solid rgba(192,192,192,0.5);
        }

        .canvas-container {
            background: radial-gradient(circle at 30% 20%, #111111, #000000);
            border-radius: 2rem;
            padding: 1rem;
            box-shadow: 0 20px 30px -10px black, inset 0 1px 2px rgba(255,255,255,0.1);
        }

        canvas {
            display: block;
            width: 100%;
            height: auto;
            background: #1a1a1a;
            border-radius: 1.2rem;
            box-shadow: 0 0 0 3px rgba(255,255,240,0.1), 0 0 0 6px rgba(255,105,180,0.2);
            cursor: pointer;
        }

        .info-vestido {
            margin-top: 1rem;
            text-align: center;
            background: rgba(0,0,0,0.5);
            padding: 0.8rem;
            border-radius: 2rem;
            width: 100%;
        }

        .info-vestido span {
            color: #ffb7d2;
            font-weight: bold;
        }

        footer {
            text-align: center;
            margin-top: 3rem;
            font-size: 0.8rem;
            color: #a0a0c0;
        }

        @media (max-width: 900px) {
            .designer-grid {
                grid-template-columns: 1fr;
                gap: 1.5rem;
                padding: 1.2rem;
            }
            body {
                padding: 1rem;
            }
            .hero h1 {
                font-size: 2.2rem;
            }
        }
    </style>
</head>
<body>
<div class="container">
    <div class="hero">
        <h1>✨ ATELIÊ SILVER ROSE ✨</h1>
        <p>especifique seu vestido de festa • design automático sob medida</p>
    </div>

    <div class="designer-grid">
        <!-- painel de especificações -->
        <div class="controls-panel">
            <h2>🎨 Crie sua peça única</h2>
            <div class="grupo">
                <label>👗 Modelo da roupa</label>
                <select id="modeloSelect">
                    <option value="ballgown">Vestido Princesa (Ball Gown)</option>
                    <option value="sirena">Sereia / Mermaid</option>
                    <option value="evase">Evase / A-line</option>
                    <option value="curto">Vestido Curto Festa</option>
                </select>
            </div>

            <div class="grupo">
                <label>🎨 Cor Principal (Tecido Base)</label>
                <div class="cor-row">
                    <input type="color" id="corPrincipal" value="#ff69b4">
                    <span id="corPrincipalHex">#ff69b4</span>
                </div>
            </div>

            <div class="grupo">
                <label>✨ Cor de Detalhe (Prata / Brilho)</label>
                <div class="cor-row">
                    <input type="color" id="corDetalhe" value="#c0c0c0">
                    <span id="corDetalheHex">#c0c0c0</span>
                </div>
            </div>

            <div class="grupo">
                <label>💎 Acabamentos e enfeites</label>
                <div class="detalhe-botoes">
                    <div class="btn-det" data-detalhe="renda">Renda</div>
                    <div class="btn-det" data-detalhe="lantejoulas">Lantejoulas</div>
                    <div class="btn-det" data-detalhe="pedraria">Pedraria</div>
                    <div class="btn-det" data-detalhe="plumas">Plumas</div>
                    <div class="btn-det" data-detalhe="fitas">Fitas prateadas</div>
                </div>
                <p style="font-size: 0.7rem; margin-top: 8px; color: #ddd;">* selecione um acabamento para estilizar</p>
                <input type="hidden" id="detalheEscolhido" value="renda">
            </div>

            <button class="btn-criar" id="gerarBtn">✦ DESENHAR MEU VESTIDO ✦</button>
            <div style="margin-top: 1rem; font-size: 0.75rem; text-align: center; color: #b9b9d9;">
                ⚡ prata + rosa | tecnologia de desenho automático
            </div>
        </div>

        <!-- canvas da roupa gerada dinamicamente -->
        <div class="visual-area">
            <div class="canvas-container">
                <canvas id="roupaCanvas" width="500" height="600" style="width:100%; height:auto; max-width:500px; aspect-ratio:500/600"></canvas>
            </div>
            <div class="info-vestido">
                🛍️ <span id="estiloAtual">Vestido Princesa</span> • Acabamento: <span id="acabamentoMostrado">Renda</span>
                <br>💖 tons predominantes: preto, prata e rosa vibrante
            </div>
        </div>
    </div>
    <footer>
        🌹 especifique modelo, cor principal, detalhe prateado e acabamento — o design é gerado automaticamente com efeitos artísticos
    </footer>
</div>

<script>
    (function() {
        // Referências DOM
        const canvas = document.getElementById('roupaCanvas');
        const ctx = canvas.getContext('2d');
        
        // elementos UI
        const modeloSelect = document.getElementById('modeloSelect');
        const corPrincipalInput = document.getElementById('corPrincipal');
        const corDetalheInput = document.getElementById('corDetalhe');
        const corPrincipalHex = document.getElementById('corPrincipalHex');
        const corDetalheHex = document.getElementById('corDetalheHex');
        const botoesDet = document.querySelectorAll('.btn-det');
        const detalheHidden = document.getElementById('detalheEscolhido');
        const gerarBtn = document.getElementById('gerarBtn');
        const estiloAtualSpan = document.getElementById('estiloAtual');
        const acabamentoMostradoSpan = document.getElementById('acabamentoMostrado');
        
        // Estado atual
        let modeloAtual = 'ballgown';
        let corPrincipal = '#ff69b4';
        let corDetalhe = '#c0c0c0';
        let acabamento = 'renda';   // padrão
        
        // Atualizar hex labels
        corPrincipalInput.addEventListener('input', (e) => {
            corPrincipal = e.target.value;
            corPrincipalHex.innerText = corPrincipal;
            desenharRoupa();
        });
        corDetalheInput.addEventListener('input', (e) => {
            corDetalhe = e.target.value;
            corDetalheHex.innerText = corDetalhe;
            desenharRoupa();
        });
        
        modeloSelect.addEventListener('change', (e) => {
            modeloAtual = e.target.value;
            let nomeModelo = modeloSelect.options[modeloSelect.selectedIndex].text;
            estiloAtualSpan.innerText = nomeModelo;
            desenharRoupa();
        });
        
        // eventos dos botões de acabamento
        botoesDet.forEach(btn => {
            btn.addEventListener('click', () => {
                const tipo = btn.getAttribute('data-detalhe');
                acabamento = tipo;
                detalheHidden.value = tipo;
                let nomeAcabamento = '';
                switch(tipo) {
                    case 'renda': nomeAcabamento = 'Renda delicada'; break;
                    case 'lantejoulas': nomeAcabamento = 'Lantejoulas brilhantes'; break;
                    case 'pedraria': nomeAcabamento = 'Pedraria cintilante'; break;
                    case 'plumas': nomeAcabamento = 'Plumas sofisticadas'; break;
                    case 'fitas': nomeAcabamento = 'Fitas prateadas'; break;
                    default: nomeAcabamento = 'Detalhe especial';
                }
                acabamentoMostradoSpan.innerText = nomeAcabamento;
                desenharRoupa();
            });
        });
        
        // botão gerar força redesenho
        gerarBtn.addEventListener('click', () => {
            desenharRoupa();
            // efeito sutil: piscar canvas
            canvas.style.transform = 'scale(0.99)';
            setTimeout(() => { canvas.style.transform = ''; }, 150);
        });
        
        // Função principal que desenha a roupa com base nas especificações, tons preto, prata e rosa predominantes (background escuro, elementos prateados e rosa)
        function desenharRoupa() {
            if (!ctx) return;
            const w = 500, h = 600;
            canvas.width = w;
            canvas.height = h;
            
            // Fundo com gradiente preto/prata (predominante preto com toques prateados)
            const gradBg = ctx.createLinearGradient(0, 0, w*0.8, h);
            gradBg.addColorStop(0, '#0b0b12');
            gradBg.addColorStop(0.6, '#1a1a24');
            gradBg.addColorStop(1, '#2a1e2a');
            ctx.fillStyle = gradBg;
            ctx.fillRect(0, 0, w, h);
            
            // acrescentar pontos prateados brilhantes (glitter elegante)
            ctx.save();
            ctx.globalCompositeOperation = 'lighter';
            for(let i = 0; i < 180; i++) {
                if(Math.random() > 0.65) continue;
                ctx.fillStyle = `rgba(192,192,255,${Math.random() * 0.4 + 0.2})`;
                ctx.beginPath();
                ctx.arc(Math.random() * w, Math.random() * h, Math.random() * 2 + 0.8, 0, Math.PI*2);
                ctx.fill();
            }
            ctx.restore();
            
            // sombra ambiente suave
            ctx.shadowColor = 'rgba(0,0,0,0.5)';
            ctx.shadowBlur = 8;
            
            // --- desenhar silhueta baseada no modelo ---
            // coordenadas auxiliares: corpo a partir de y=120 até y=480
            const corpoTopo = 130;
            const ombroX = w/2;
            
            // função para aplicar degradê de cor principal + toques prata no vestido
            function aplicarDegradeVestido(x, y, wVest, hVest, angle = 0) {
                const grad = ctx.createLinearGradient(x, y, x + wVest*0.6, y + hVest);
                grad.addColorStop(0, corPrincipal);
                grad.addColorStop(0.7, corDetalhe);
                grad.addColorStop(1, '#4a2a3a');
                return grad;
            }
            
            // Desenhar de acordo modelo
            ctx.save();
            ctx.shadowBlur = 6;
            ctx.shadowColor = "rgba(0,0,0,0.4)";
            
            if(modeloAtual === 'ballgown') {
                // Saia ampla princesa
                ctx.beginPath();
                // corpete
                ctx.moveTo(ombroX - 45, corpoTopo);
                ctx.quadraticCurveTo(ombroX - 25, corpoTopo+30, ombroX - 40, corpoTopo+80);
                ctx.lineTo(ombroX - 55, corpoTopo+110);
                ctx.lineTo(ombroX - 90, corpoTopo+250);
                ctx.quadraticCurveTo(ombroX - 50, corpoTopo+360, ombroX, corpoTopo+380);
                ctx.quadraticCurveTo(ombroX + 50, corpoTopo+360, ombroX + 90, corpoTopo+250);
                ctx.lineTo(ombroX + 55, corpoTopo+110);
                ctx.lineTo(ombroX + 40, corpoTopo+80);
                ctx.quadraticCurveTo(ombroX + 25, corpoTopo+30, ombroX + 45, corpoTopo);
                ctx.fillStyle = aplicarDegradeVestido(ombroX-90, corpoTopo, 180, 300);
                ctx.fill();
                ctx.strokeStyle = corDetalhe;
                ctx.lineWidth = 2;
                ctx.stroke();
                // cintura prateada
                ctx.beginPath();
                ctx.ellipse(ombroX, corpoTopo+110, 48, 15, 0, 0, Math.PI*2);
                ctx.fillStyle = corDetalhe;
                ctx.fill();
                // laço ou faixa
                ctx.fillStyle = corDetalhe;
                ctx.beginPath();
                ctx.moveTo(ombroX-15, corpoTopo+100);
                ctx.lineTo(ombroX, corpoTopo+125);
                ctx.lineTo(ombroX+15, corpoTopo+100);
                ctx.fill();
            } 
            else if (modeloAtual === 'sirena') {
                // modelo sereia justo até joelho e depois abertura
                ctx.beginPath();
                ctx.moveTo(ombroX - 35, corpoTopo);
                ctx.quadraticCurveTo(ombroX - 25, corpoTopo+40, ombroX - 32, corpoTopo+110);
                ctx.lineTo(ombroX - 25, corpoTopo+250);
                ctx.quadraticCurveTo(ombroX - 20, corpoTopo+310, ombroX - 45, corpoTopo+370);
                ctx.lineTo(ombroX - 30, corpoTopo+400);
                ctx.lineTo(ombroX, corpoTopo+420);
                ctx.lineTo(ombroX + 30, corpoTopo+400);
                ctx.lineTo(ombroX + 45, corpoTopo+370);
                ctx.quadraticCurveTo(ombroX + 20, corpoTopo+310, ombroX + 25, corpoTopo+250);
                ctx.lineTo(ombroX + 32, corpoTopo+110);
                ctx.quadraticCurveTo(ombroX + 25, corpoTopo+40, ombroX + 35, corpoTopo);
                ctx.fillStyle = aplicarDegradeVestido(ombroX-45, corpoTopo, 90, 320);
                ctx.fill();
                // barbatana / cauda efeito prata
                ctx.fillStyle = corDetalhe;
                ctx.beginPath();
                ctx.moveTo(ombroX-20, corpoTopo+395);
                ctx.quadraticCurveTo(ombroX-35, corpoTopo+430, ombroX-10, corpoTopo+445);
                ctx.lineTo(ombroX, corpoTopo+460);
                ctx.lineTo(ombroX+10, corpoTopo+445);
                ctx.quadraticCurveTo(ombroX+35, corpoTopo+430, ombroX+20, corpoTopo+395);
                ctx.fill();
            }
            else if (modeloAtual === 'evase') {
                // Evasê (A-line) mais simples e elegante
                ctx.beginPath();
                ctx.moveTo(ombroX - 40, corpoTopo);
                ctx.quadraticCurveTo(ombroX - 20, corpoTopo+45, ombroX - 35, corpoTopo+90);
                ctx.lineTo(ombroX - 70, corpoTopo+280);
                ctx.quadraticCurveTo(ombroX - 40, corpoTopo+360, ombroX, corpoTopo+370);
                ctx.quadraticCurveTo(ombroX + 40, corpoTopo+360, ombroX + 70, corpoTopo+280);
                ctx.lineTo(ombroX + 35, corpoTopo+90);
                ctx.quadraticCurveTo(ombroX + 20, corpoTopo+45, ombroX + 40, corpoTopo);
                ctx.fillStyle = aplicarDegradeVestido(ombroX-70, corpoTopo, 140, 300);
                ctx.fill();
                // cinto prata destacado
                ctx.beginPath();
                ctx.rect(ombroX-42, corpoTopo+95, 84, 14);
                ctx.fillStyle = corDetalhe;
                ctx.fill();
            }
            else if (modeloAtual === 'curto') {
                // vestido curto festa (mini)
                ctx.beginPath();
                ctx.moveTo(ombroX - 38, corpoTopo);
                ctx.quadraticCurveTo(ombroX - 20, corpoTopo+35, ombroX - 35, corpoTopo+70);
                ctx.lineTo(ombroX - 50, corpoTopo+190);
                ctx.quadraticCurveTo(ombroX - 30, corpoTopo+260, ombroX, corpoTopo+270);
                ctx.quadraticCurveTo(ombroX + 30, corpoTopo+260, ombroX + 50, corpoTopo+190);
                ctx.lineTo(ombroX + 35, corpoTopo+70);
                ctx.quadraticCurveTo(ombroX + 20, corpoTopo+35, ombroX + 38, corpoTopo);
                ctx.fillStyle = aplicarDegradeVestido(ombroX-50, corpoTopo, 100, 200);
                ctx.fill();
                // babado prateado
                ctx.beginPath();
                ctx.ellipse(ombroX, corpoTopo+265, 55, 12, 0, 0, Math.PI*2);
                ctx.fillStyle = corDetalhe;
                ctx.fill();
            }
            
            // adicionar decote e detalhes gerais (alças finas prateadas)
            ctx.beginPath();
            ctx.moveTo(ombroX-32, corpoTopo-5);
            ctx.lineTo(ombroX-20, corpoTopo+12);
            ctx.lineTo(ombroX-8, corpoTopo+5);
            ctx.fillStyle = corDetalhe;
            ctx.fill();
            ctx.beginPath();
            ctx.moveTo(ombroX+32, corpoTopo-5);
            ctx.lineTo(ombroX+20, corpoTopo+12);
            ctx.lineTo(ombroX+8, corpoTopo+5);
            ctx.fill();
            
            // APLICAÇÃO DO ACABAMENTO ESCOLHIDO (dinâmico)
            ctx.globalCompositeOperation = 'source-over';
            ctx.shadowBlur = 3;
            if(acabamento === 'renda') {
                // padrões renda nas bordas
                ctx.beginPath();
                ctx.strokeStyle = corDetalhe;
                ctx.lineWidth = 1.8;
                for(let i = 0; i < 12; i++) {
                    let offY = corpoTopo + 80 + i*25;
                    ctx.beginPath();
                    ctx.ellipse(ombroX-55 + (i%3)*8, offY, 7, 4, 0.5, 0, Math.PI*2);
                    ctx.stroke();
                    ctx.beginPath();
                    ctx.ellipse(ombroX+55 - (i%3)*8, offY, 7, 4, -0.5, 0, Math.PI*2);
                    ctx.stroke();
                }
            } else if(acabamento === 'lantejoulas') {
                for(let i=0;i<80;i++) {
                    let x = ombroX - 45 + Math.random() * 90;
                    let y = corpoTopo + 40 + Math.random() * 320;
                    if(y < corpoTopo+400) {
                        ctx.fillStyle = `rgba(255,215,0,${Math.random() * 0.7+0.3})`;
                        ctx.beginPath();
                        ctx.arc(x, y, 2+Math.random()*2, 0, Math.PI*2);
                        ctx.fill();
                    }
                }
            } else if(acabamento === 'pedraria') {
                for(let i=0;i<50;i++) {
                    let x = ombroX - 38 + Math.random() * 76;
                    let y = corpoTopo + 50 + Math.random() * 300;
                    ctx.fillStyle = `rgba(255,255,255,0.9)`;
                    ctx.beginPath();
                    ctx.rect(x-2, y-1, 3, 3);
                    ctx.fill();
                    ctx.fillStyle = `rgba(192,192,255,0.8)`;
                    ctx.beginPath();
                    ctx.rect(x-1, y-2, 2, 2);
                    ctx.fill();
                }
            } else if(acabamento === 'plumas') {
                ctx.fillStyle = corDetalhe;
                for(let i=0;i<18;i++) {
                    let ang = i * 0.7;
                    let xOff = Math.sin(ang)*20;
                    let yOff = corpoTopo+280 + i*6;
                    ctx.beginPath();
                    ctx.moveTo(ombroX-40 + xOff, yOff);
                    ctx.quadraticCurveTo(ombroX-55 + xOff, yOff+12, ombroX-48 + xOff, yOff+20);
                    ctx.fill();
                    ctx.beginPath();
                    ctx.moveTo(ombroX+40 + xOff, yOff);
                    ctx.quadraticCurveTo(ombroX+55 + xOff, yOff+12, ombroX+48 + xOff, yOff+20);
                    ctx.fill();
                }
            } else if(acabamento === 'fitas') {
                for(let s=0; s<4; s++) {
                    ctx.beginPath();
                    ctx.moveTo(ombroX-45 + s*12, corpoTopo+180);
                    ctx.lineTo(ombroX-30 + s*10, corpoTopo+210);
                    ctx.lineTo(ombroX-42 + s*12, corpoTopo+220);
                    ctx.fillStyle = corDetalhe;
                    ctx.fill();
                    ctx.beginPath();
                    ctx.moveTo(ombroX+45 - s*12, corpoTopo+180);
                    ctx.lineTo(ombroX+30 - s*10, corpoTopo+210);
                    ctx.lineTo(ombroX+42 - s*12, corpoTopo+220);
                    ctx.fill();
                }
            }
            
            // toque final: brilho prata (cintilação)
            ctx.globalCompositeOperation = 'lighter';
            for(let g=0; g<30; g++) {
                ctx.fillStyle = `rgba(220,220,255,${Math.random()*0.4})`;
                ctx.beginPath();
                ctx.arc(ombroX - 28 + Math.random()*56, corpoTopo+70+Math.random()*340, 1.2+Math.random()*2, 0, Math.PI*2);
                ctx.fill();
            }
            
            ctx.restore();
            
            // borda decorativa estilo prata + rosa
            ctx.strokeStyle = '#ff99cc';
            ctx.lineWidth = 2;
            ctx.strokeRect(8, 8, w-16, h-16);
            ctx.strokeStyle = '#c0c0c0';
            ctx.lineWidth = 1;
            ctx.strokeRect(10, 10, w-20, h-20);
        }
        
        // inicializar valores e desenhar padrão
        function init() {
            corPrincipal = corPrincipalInput.value;
            corDetalhe = corDetalheInput.value;
            modeloAtual = modeloSelect.value;
            acabamento = 'renda';
            detalheHidden.value = 'renda';
            acabamentoMostradoSpan.innerText = 'Renda delicada';
            estiloAtualSpan.innerText = modeloSelect.options[modeloSelect.selectedIndex].text;
            desenharRoupa();
        }
        
        init();
        window.addEventListener('resize', () => desenharRoupa());
    })();
</script>
</body>
</html>
```
