G00: Movimento rápido - move a ferramenta rapidamente para uma posição sem cortar material.
G01: Movimento linear interpolado - move a ferramenta em linha reta de um ponto inicial para um ponto final a uma velocidade constante, cortando material no processo.
G02: Movimento circular interpolado no sentido horário - move a ferramenta em um arco circular no sentido horário de um ponto inicial para um ponto final.
G03: Movimento circular interpolado no sentido anti-horário - semelhante ao G02, mas move a ferramenta em um arco circular no sentido anti-horário.
G17, G18, G19: Seleção do plano de trabalho - determina o plano de trabalho no qual os movimentos serão executados (G17 para o plano XY, G18 para o plano XZ e G19 para o plano YZ).
G20, G21: Unidades de medida - define as unidades de medida como polegadas (G20) ou milímetros (G21).
G28: Retorno à posição de referência - move a ferramenta de volta à posição de referência da máquina.
G40, G41, G42: Compensação de raio da ferramenta - ajusta o caminho da ferramenta para compensar o raio da própria ferramenta.
G90, G91: Modo absoluto e relativo - G90 define o modo absoluto, onde os movimentos são medidos a partir do ponto de origem da máquina, enquanto G91 define o modo relativo, onde os movimentos são relativos à posição atual da ferramenta.
M06: Troca de ferramenta - utilizada para trocar automaticamente a ferramenta de corte

-----------------------------------------------------------------------------------------------------
RAIO
G02 X3 Z3 R10 ; Movimento circular interpolado no sentido horário com raio 10mm até a posição X3, Z3
CHANFRO

Exemplo de perfuração
G01 Z-5 F100  ; Desça até uma profundidade de corte de 5 mm com uma taxa de avanço de 100 mm/min
G01 X10 Y10  ; Movimento linear para a primeira posição de perfuração
G01 Z-10  ; Desça mais 5 mm para perfurar completamente a peça
G00 Z5  ; Levantar para uma altura segura

Exemplo de fresagem
G01 Z0 F200  ; Desça até a superfície da peça com uma taxa de avanço de 200 mm/min
G01 X20 Y20  ; Movimento linear para a primeira posição de fresagem
G01 Z-2  ; Desça 2 mm para iniciar o processo de fresagem

-----------------------------------------------------------------------------------------------------

BASE DE CODIGO:

G21 ; Define unidades métricas (milímetros)
G17 ; Seleciona o plano XY
G90 ; Modo absoluto
; Movimento para a posição inicial
G00 X0 Z0 ; Move rapidamente para a posição inicial (X=0, Z=0)
; Movimento para uma nova posição
G01 X50 Z10 F100 ; Move linearmente para a posição X=50, Z=10 com uma taxa de avanço de 100 mm/min
; Outro movimento para uma nova posição
G01 X30 Z-5 F50 ; Move linearmente para a posição X=30, Z=-5 com uma taxa de avanço de 50 mm/min
; Retorno à posição inicial
G00 X0 Z0 ; Move rapidamente de volta para a posição inicial (X=0, Z=0)


-----------------------------------------------------------------------------------------------------
Início do programa principal

G21  // Seleciona unidades métricas (milímetros)
G17  // Seleciona o plano de trabalho XY
G90  // Define o modo absoluto

T1 M06  // Seleciona a ferramenta T1 e executa a troca de ferramenta
G54  // Seleciona o sistema de coordenadas de trabalho

M03 S1000  // Inicia o fuso a 1000 RPM (ajuste conforme necessário)
G00 X0 Y0 Z10  // Move rapidamente para a posição inicial de segurança

// Início do programa de usinagem da peça
G01 Z-5 F100  // Move linearmente para baixo até uma profundidade de corte de 5mm a uma taxa de avanço de 100 mm/min

// Aqui você colocaria o código para realizar as operações de usinagem necessárias, como fresamento, furação, etc.

G00 Z10  // Move rapidamente para cima após a conclusão da usinagem
G00 X0 Y0  // Retorna rapidamente à posição inicial
M05  // Desliga o fuso
M30  // Fim do programa
-----------------------------------------------------------------------------------------------------


