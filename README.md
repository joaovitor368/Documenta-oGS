UrbanSense — Monitoramento Inteligente de Luminosidade Urbana
  
Global Solution 2026.2 — CitizenTech | Edge Computing & Computer Systems

Desenvolvedor: João Vitor Batista De Mattos
RM: 571389
Instituição: FIAP  
Projeto funcionando no Wokwi
Abrir e testar o UrbanSense no Wokwi
O protótipo foi desenvolvido e testado em simulação. As medições e os limiares são experimentais; não representam certificação de segurança ou de acessibilidade de uma rota real.

Sobre o projeto
O UrbanSense é um protótipo de monitoramento de luminosidade em espaços urbanos. O objetivo é fornecer uma indicação local das condições de iluminação por meio de um display LCD 16x2 I2C, LEDs coloridos e alerta sonoro, como contribuição inicial para a discussão de acessibilidade e deslocamento urbano.

A solução se relaciona à proposta CitizenTech e, de forma temática, aos ODS 11 — Cidades e Comunidades Sustentáveis e 10 — Redução das Desigualdades.

Escopo atual: o dispositivo mede luminosidade; não identifica buracos, obstáculos físicos, rampas ou a segurança geral de um trajeto.
Componentes
Componente	Função
ESP32 DevKit V1	Processamento e controle
Sensor LDR (fotoresistor)	Leitura de luminosidade
LCD 16x2 I2C	Exibição do estado e da leitura
LED verde	Estado normal
LED amarelo	Estado de atenção
LED vermelho	Estado de alerta ou falha
3 resistores de 220 Ω	Limitação de corrente dos LEDs
Buzzer	Alerta sonoro
Botão	Ativação/desativação de falha simulada


Conexões do ESP32
Componente	Conexão
LCD VCC / GND	5V / GND
LCD SDA / SCL	GPIO 21 / GPIO 22
LDR VCC / GND	3V3 / GND
LDR AO	GPIO 34
LED verde	GPIO 18
LED amarelo	GPIO 19
LED vermelho	GPIO 25
Buzzer	GPIO 23
Botão (INPUT_PULLUP)	GPIO 27 e GND


Cada LED utiliza um resistor de 220 Ω em série.
Estados do sistema
Estado	Luminosidade estimada	Indicação
NORMAL	≥ 150 lux	LED verde
ATENÇÃO	50 a menos de 150 lux	LED amarelo
ALERTA	Menos de 50 lux	LED vermelho e buzzer intermitente
FALHA SIMULADA	Acionamento do botão ou leitura inválida	LED vermelho e buzzer contínuo


Os valores de lux são aproximados e dependem da simulação e da conversão da leitura analógica. Os limites são didáticos, não normativos.
Funcionamento do software
O ESP32 realiza leituras periódicas do LDR, aplica suavização para reduzir oscilações, classifica o nível de luminosidade e atualiza os indicadores. O sistema utiliza millis() para organizar as tarefas sem depender de pausas longas com delay().

O botão possui tratamento de debounce e alterna o modo de falha simulada. O Serial Monitor registra as leituras e os estados para facilitar a depuração.
Como executar
1. Abra o projeto UrbanSense no Wokwi.
2. Clique em Start Simulation.
3. Clique no sensor LDR e altere a luminosidade para observar os estados.
4. Observe o LCD, os LEDs e o buzzer.
5. Pressione o botão azul para ativar a falha simulada; pressione novamente para retornar ao monitoramento.
6. Confira as mensagens no Serial Monitor.
Se desejar recriar o projeto, utilize os arquivos sketch.ino, diagram.json e libraries.txt deste repositório.
Roteiro de testes
- NORMAL: ajustar a luminosidade para um valor acima de 150 lux e aguardar a estabilização.
- ATENÇÃO: ajustar entre 50 e 150 lux.
- ALERTA: ajustar abaixo de 50 lux e observar o buzzer.
- FALHA: pressionar o botão azul e verificar o aviso no LCD; pressionar novamente para sair.
Validação: o funcionamento dos componentes foi confirmado pelo desenvolvedor na simulação do Wokwi. Capturas de tela e vídeo podem ser adicionados posteriormente como evidências.
Estrutura do repositório
UrbanSense/
├── README.md
├── sketch.ino
├── diagram.json
├── libraries.txt
└── ROTEIRO_VIDEO.md
Demonstração
- Simulador: https://wokwi.com/projects/480078211156907009
- Vídeo demonstrativo (YouTube): a adicionar após a gravação.
Limitações e evolução
Esta versão implementa o monitoramento local no ESP32. Ainda não possui integração com backend/nuvem nem dashboard conectado. Uma evolução prevista é transmitir as leituras para uma API e apresentá-las no painel web do UrbanSense. Essa integração não deve ser considerada implementada nesta versão.
Referências
- FIAP — Global Solution 2026.2, desafio CitizenTech, disciplina Edge Computing & Computer Systems.
- Wokwi — Simulador de eletrônica e ESP32.
UrbanSense © 2026 — João Vitor Batista De Mattos | RM 571389 | FIAP
