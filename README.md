# Fractais---Cultura-do-Script
Projeto para a matéria de Cultura do Script, do curso de Pós Graduação em Arquitetura Digital da Belas Artes, ministrado pelo Prof. Alexandre Villares

add_library('svg')

#### FractalPlant
save_frame = False
fator_escala = 3.78 # 255px -> ~255mm
tamanho = 3
angulo = radians(25) 
axioma = "X"
regras = {"X" : " F+[[X]-X]-F[-FX]+X",
          "F" : "FF",
          }

def setup():
    global resultado1, resultado2, output
    size(500, 1000, P3D)
    rectMode(CENTER)
    resultado1 = l_sytem(6)
    resultado2 = l_sytem(6)
    output = createGraphics(width, height, SVG, "3D.svg")
    # output = createGraphics(width, height, PDF, "3D.pdf")

def draw():
    if save_frame:
        beginRaw(output)
        output.background(0)
        
    background(0)
    translate(150, 400)
    stroke(36, 92, 255)
    desenhe(resultado1)
    stroke(36, 206, 255)    
    desenhe(resultado2) 
    lights()
    translate(width / 2, height / 2)
    rotateX(radians(frameCount))
    rotateY(radians(frameCount))
    noStroke()
    fill(255)
    caixa(100, -500, 50, 50, 50, 50)
    rotateX(120)
    rotateY(120)
    fill(255)
    caixa(200, -500, 50, 50, 50, 50)
    rotateX(40)
    rotateY(40)
    fill(255)
    caixa(-50, -500, 50, 50, 50, 50)
    rotateX(300)
    rotateY(300)
    fill(255)
    caixa(-50, -100, 50, 50, 50, 50)
    rotateX(300)
    rotateY(150)
    fill(255)
    caixa(-50, -200, 50, 50, 50, 50)
    rotateX(150)
    rotateY(300)
    fill(255)
    caixa(-50, -700, 50, 50, 50, 50)
    rotateX(150)
    rotateY(300)
    fill(255)
    caixa(400, -700, 50, 50, 50, 50)
    
    if save_frame:
        endRaw() 
        exit()  

  
            
def desenhe(frase):
    a = frameCount % 180 
    x = radians(a) * 100
    for letra in frase:
        if letra == "+":
            rotate(angulo)
        if letra == "-":
            rotate(-angulo)
        if letra == "[":
            pushMatrix()
        if letra == "]":
            popMatrix()    
        if letra == "F":
            line(x, 0, x, tamanho)
            translate(2, tamanho)

                            
                                            
def l_sytem(n):
    frase = axioma
    nova_frase = ""
    for i in range(n):
        for letra in frase:
            nova_frase += regras.get(letra, letra)
        frase = nova_frase
    return nova_frase


def caixa(x, y, z, *tam):
    pushMatrix()
    translate(x, y, z)
    box(*tam)
    popMatrix() 
    
def keyPressed():
    global save_frame
    if key == 'p':
        save_frame = True
