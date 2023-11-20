#Declarações de variáveis.
import time
pecaPreta = 'x'
pecaBranca = 'o'
damaPreta = 'X'
damaBranca = 'O'
contador=0
vez=pecaBranca
movi=''
lugar=''
opcao=''
k=0
p=0
pecaPretaCapturada=[]
pecaBrancaCapturada=[]
at=-1



#O tabuleiro.
tabuleiro={"8a":'-',"8b":pecaPreta,"8c":'-',"8d":pecaPreta,"8e":'-',"8f":pecaPreta,"8g":'-',"8h":pecaPreta,
            "7a":pecaPreta,"7b":'-',"7c":pecaPreta,"7d":'-',"7e":damaBranca,"7f":'-',"7g":pecaPreta,"7h":'-',
            "6a":'-',"6b":pecaPreta,"6c":'-',"6d":pecaPreta,"6e":'-',"6f":pecaPreta,"6g":'-',"6h":pecaPreta,
            "5a":'-',"5b":'-',"5c":'-',"5d":'-',"5e":'-',"5f":'-',"5g":'-',"5h":'-',
            "4a":'-',"4b":pecaPreta,"4c":'-',"4d":'-',"4e":'-',"4f":'-',"4g":'-',"4h":'-',
            "3a":'-',"3b":'-',"3c":pecaBranca,"3d":'-',"3e":pecaBranca,"3f":'-',"3g":pecaBranca,"3h":'-',
            "2a":'-',"2b":pecaBranca,"2c":'-',"2d":pecaBranca,"2e":'-',"2f":pecaBranca,"2g":'-',"2h":pecaBranca,
            "1a":pecaBranca,"1b":'-',"1c":pecaBranca,"1d":'-',"1e":pecaBranca,"1f":'-',"1g":pecaBranca,"1h":'-'}
#Função de montar o  no print.
def montarBulero():
    listinha = {0:"a",1:"b",2:"c",3:"d",4:"e",5:"f",6:"g",7:"h"}
    for i in range(8):
        p = str(8-i)+" "
        for j in range(8):
            p += tabuleiro.get(str(8-i)+listinha.get(j))+" "
        print(p)
    a = "  "
    for i in range(8):
        a+=listinha.get(i)+" "
    print()
    print(a)
    print()
montarBulero()


 
#Restrição caso o formato do input (sintaxe) esteja incorreto.
def restricaoFormato(movimento,movi,lugar):
    if len(movimento)!=4 or movi[0] not in '12345678' or movi[1] not in 'abcdefgh' or lugar[0] not in '12345678' or lugar[1] not in 'abcdefgh' :
        print("Formato não identificado")
        print("Tente Novamente!!")
        print("")
        return False
    else:
        return True
   
#Restrição caso não haja peça no lugar selecionado.      
def restricaoMoviPeca(movi):
    if p==0 and tabuleiro[movi]=='-':
        print("Essa jogada não pode ser realizada pois não há nenhuma peça na posicão informada")
        print("Tente novamente!")
        print("")
        return False
    else:
        return True

#Restrição caso a posição informada não exista.  
def restricaoMoviIne(movi):
    if movi not in tabuleiro:
        print("A posição informada não existe.")
        print("Tente novamente!")
        print("")
        return False
    else:
        return True
   
#Restrição caso não seja a vez dessa peça jogar.
def restricaoMoviVez(movi):      
    if p==0 and tabuleiro[movi]!=vez:
        print("Essa jogada não pode ser realizada pois a peça escolhida é a oposta a sua cor.")
        print("Tente novamente!")
        print("")
        return False
    else:
        return True
    

#Funções da dama

#captura da dama
def capturaDama(movi,lugar):
    letras = {"a":1,"b":2,"c":3,"d":4,"e":5,"f":6,"g":7,"h":8}
    global cap
    cap=0
    
    # nesse if ele vê se vai pra frente ou pra trás
    if int(lugar[0]) > int(movi[0]):
        l = -1
    else:
        l = 1
    # e nesse ele vê se é pra esquerda ou pra direita  
    if letras[lugar[1]] > letras[movi[1]]:
        m = -1
    else:
        m = 1

    capturada = str(int(lugar[0]) + l*1)+str(chr(ord(lugar[1])+ m*1))
    if tabuleiro[capturada] and tabuleiro[movi]==damaPreta:
        pecaBrancaCapturada.append("o")
        tabuleiro[capturada]='-'
        print()
        print(f'A peça Branca da posição {capturada} foi capturada.')
        print(*pecaBrancaCapturada)
        print()
        cap+=1
        return True
    elif tabuleiro[capturada] and tabuleiro[movi]==damaBranca:
        pecaPretaCapturada.append("x")
        tabuleiro[capturada]='-'
        print()
        print(f'A peça Preta da posição {capturada} foi capturada.')
        print(*pecaPretaCapturada)
        print()
        cap+=1
        return True
    return False

#restrição de movimento para a dama    
def essadamapodevoarn(lugar,movi):
    letras = {"a":1,"b":2,"c":3,"d":4,"e":5,"f":6,"g":7,"h":8}
    # nesse if ele vê se vai pra frente ou pra trás
    if int(lugar[0]) > int(movi[0]):
        l = 1
    else:
        l = -1
    # e nesse ele vê se é pra esquerda ou pra direita  
    if letras[lugar[1]] > letras[movi[1]]:
        m = 1
    else:
        m = -1
    # vai passar cada lugar do tabuleiro no sentido que foi detectado e para se encontrar uma peça no caminho
    for i in range(abs(int(lugar[0])-int(movi[0]))):
        if  tabuleiro[str(int(movi[0]) + i*l)+str(chr(ord(movi[1]) + i*m))] != '-' and capturaDama(movi,lugar)==False :
            print("e meu fi quer voar é?")
            print("Tente novamente!")
            print("")
            return False
    return True
       
#Função de como se mover com a dama
def dancinhadadama(movi,lugar):
    letras = {"a":1,"b":2,"c":3,"d":4,"e":5,"f":6,"g":7,"h":8}
    if int(movi[0])-int(lugar[0]) != letras[movi[1]] - letras[lugar[1]]:
        print("A dama não é tão roubada assim!")
        print("Tente novamente!")
        print("")
        return False
    else:
        return True

#função para virar dama
def dama(lugar2,tabuleiro2,movi2):
    if lugar2[0]=='8' and tabuleiro2[movi2] == 'o':
        tabuleiro2[lugar2] = damaBranca
    if lugar2[0]=='1' and tabuleiro2[movi2] == 'x':
        tabuleiro2[lugar2] = damaPreta
    return tabuleiro2

#Restrição para jogar com a dama na vez da cor certa
def restricaoMoviDamaCor(movi):      
    if vez=='x' and tabuleiro[movi]==damaBranca:
        print("Essa jogada não pode ser realizada pois a peça escolhida é a oposta a sua cor.")
        print("Tente novamente!")
        print("")
        return False
    elif vez=='o' and tabuleiro[movi]==damaPreta:
        print("Essa jogada não pode ser realizada pois a peça escolhida é a oposta a sua cor.")
        print("Tente novamente!")
        print("")
        return False
    else:
        return True


#RESTRIÇÕES DOS LUGARES DA PEÇA

       
   
#Restrição de lugares já ocupados por outras peças.
def restricaoLugarOcupado(lugar):
    if tabuleiro[lugar] in 'ox':
        print("Não é possivel mover a peça para um lugar que já tenha outra peça!")
        print("Tente Novamente!!")
        print("")
        return False
    else:
        return True
#Restrição do lugar escolhido não poder ser movido
def restricaoLugarImpo(movi,lugar):
    letrasres = {"a":1,"b":2,"c":3,"d":4,"e":5,"f":6,"g":7,"h":8}
    if captura(movi,lugar)==False:
        if vez=='o' and int(letrasres[movi[1]])-int(letrasres[lugar[1]]) not in [-1,1] or vez=='x' and int(letrasres[movi[1]])-int(letrasres[lugar[1]]) not in [-1,1] :
            print("Impossível mover a peça para o local escolhido")
            print("Tente Novamente!!")
            print("")
            return False
        else:
            return True

   
#Restrição de lugares que não podem colocar peças no tabuleiro.      
def restricaoLugarPosicao(lugar):
    if int(lugar[0])%2==0 and lugar[1] in 'aceg' or int(lugar[0])%2!=0 and lugar[1] in 'bdfh' :
        print("Não é possível colocar peças nessa posição.")
        print("Tente Novamente!!")
        print("")
        return False
    else:
        return True
   
#Restrição das peças não poderem voltar casas  
def restricaoLugarFrente(lugar):
    if vez==pecaBranca and int(lugar[0])<=int(movi[0]) or vez==pecaPreta and int(lugar[0])>=int(movi[0]):
        print("Só é possível ir para frente com as peças!")
        print("Tente novamente!!")
        print("")
        return False
    else:
        return True
 
#Restrição sobre as peças só poderem ir para uma casa de cada vez.    
def restricaoLugarVez(lugar):
    if vez==pecaBranca and int(lugar[0])-int(movi[0])!=1 or vez==pecaPreta and int(lugar[0])-int(movi[0])!=-1 :
        print("Não é possível andar mais de uma casa por vez!")
        print("Tente novamente!!")
        print("")
        return False
    else:
        return True

   
#Função Captura de peças.  
def captura(movi,lugar):
    global cap
    cap=0
    numeros = {"1":1,"2":2,"3":3,"4":4,"5":5,"6":6,"7":7,"8":8}
    letras = {"a":1,"b":2,"c":3,"d":4,"e":5,"f":6,"g":7,"h":8}
    alfanum = {"1":"a","2":"b","3":"c","4":"d","5":"e","6":"f","7":"g","8":"h"}
    capturada = str(int(numeros[movi[0]]+numeros[lugar[0]])//2) + alfanum[str(int(letras[movi[1]]+letras[lugar[1]])//2)]
    if tabuleiro[lugar] == '-' and tabuleiro[capturada] in'xX' and vez==pecaBranca:
        pecaPretaCapturada.append("x")
        tabuleiro[capturada]='-'
        print()
        print(f'A peça Preta da posição {capturada} foi capturada.')
        print(*pecaPretaCapturada)
        print()
        cap+=1
        return True
    elif tabuleiro[lugar]== '-' and tabuleiro[capturada] in 'oO' and vez==pecaPreta:
        pecaBrancaCapturada.append("o")
        tabuleiro[capturada]='-'
        print()
        print(f'A peça Branca da posição {capturada} foi capturada.')
        print(*pecaBrancaCapturada)
        print()
        cap+=1
        return True
    return False
   


#Função Mover peças.
def mover(pecaMovida,pecaLugar):
    tabuleiro[pecaLugar]=tabuleiro[pecaMovida]
    dama(lugar,tabuleiro,movi)
    tabuleiro[pecaMovida]='-'
   
def capturaPossivel(movi,lugar):
    numeros = {"1":1,"2":2,"3":3,"4":4,"5":5,"6":6,"7":7,"8":8}
    letras = {"a":1,"b":2,"c":3,"d":4,"e":5,"f":6,"g":7,"h":8}
    alfanum = {"1":"a","2":"b","3":"c","4":"d","5":"e","6":"f","7":"g","8":"h"}
    capturada = str(int(numeros[movi[0]]+numeros[lugar[0]])//2) + alfanum[str(int(letras[movi[1]]+letras[lugar[1]])//2)]
    if tabuleiro[lugar] == '-' and tabuleiro[capturada] in 'xX' and vez==pecaBranca:
        return True
    elif tabuleiro[lugar]== '-' and tabuleiro[capturada] in 'oO' and vez==pecaPreta:
        return True
    return False
   
   
   
   
def capturaObrigatoria(tabuleiro, vez):
    for peca in tabuleiro:
        if tabuleiro[peca] == vez:
            movi = peca
            letras = {"a": 1, "b": 2, "c": 3, "d": 4, "e": 5, "f": 6, "g": 7, "h": 8}
            numeros = {"1": 1, "2": 2, "3": 3, "4": 4, "5": 5, "6": 6, "7": 7, "8": 8}
            for i in [-1, 1]:
                for j in [-1, 1]:
                    lugar = str(numeros[movi[0]] + i) + chr(ord(movi[1]) + j)
                    destino = str(numeros[movi[0]] + 2 * i) + chr(ord(movi[1]) + 2 * j)
                    if lugar in tabuleiro and destino in tabuleiro:
                        if tabuleiro[lugar] != vez and tabuleiro[lugar] != '-' and tabuleiro[destino] == '-':
                            print()
                            print("Você tem que capturar a peça.")
                            print()
                            return True
    return False



def capturaObrigatoriaSeguida(vez,lugar,tabuleiro):
    
    
    #verificar se há peças na ESQUERDA que podem ser capturadas (BRANCOS)
    if vez=='o' and lugar[0] not in '78' and lugar[1] not in 'ab' and tabuleiro[str(int(lugar[0])+1) + str(chr(ord(lugar[1])-1))] =='x' and  tabuleiro[str(int(lugar[0])+2) + str(chr(ord(lugar[1])-2))] == '-':
        print("Captura Obrigatória")
        return True
    #verificar se há peças na DIREITA que podem ser capturadas (BRANCOS)
    if vez=='o' and lugar[0] not in '78' and lugar[1] not in 'gh' and  tabuleiro[str(int(lugar[0])+1) + str(chr(ord(lugar[1])+1))] =='x' and  tabuleiro[str(int(lugar[0])+2) + str(chr(ord(lugar[1])+2))] == '-':
        print("Captura Obrigatória")
        return True

    #verificar se há peças na DIREITA que podem ser capturadas (PRETOS)
    if vez=='x' and lugar[0] not in '12' and lugar[1] not in 'gh' and tabuleiro[str(int(lugar[0])-1) + str(chr(ord(lugar[1])+1))] =='o' and  tabuleiro[str(int(lugar[0])-2) + str(chr(ord(lugar[1])+2))] == '-':
        print("Captura Obrigatória")
        return True
    #verificar se há peças na ESQUERDA que podem ser capturadas (PRETOS)
    if vez=='x' and lugar[0] not in '12' and lugar[1] not in 'ab' and tabuleiro[str(int(lugar[0])-1) + str(chr(ord(lugar[1])-1))] =='o' and  tabuleiro[str(int(lugar[0])-2) + str(chr(ord(lugar[1])-2))] == '-':
        print("Captura Obrigatória")
        return True
    return False
    
    
def capturaObrigatoriaSeguidaDama(lugar,tabuleiro):
    
    #BRANCO
    
    #verificar se há peças na ESQUERDA que podem ser capturadas CIMA DAMA
    if tabuleiro[lugar] =='O' and lugar[0] not in '78' and lugar[1] not in 'ab' and tabuleiro[str(int(lugar[0])+1) + str(chr(ord(lugar[1])-1))] =='x' and  tabuleiro[str(int(lugar[0])+2) + str(chr(ord(lugar[1])-2))] == '-':
        print("Captura Obrigatória")
        return True
    #verificar se há peças na DIREITA que podem ser capturadas CIMA DAMA
    if tabuleiro[lugar] == 'O' and lugar[0] not in '78' and lugar[1] not in 'gh' and  tabuleiro[str(int(lugar[0])+1) + str(chr(ord(lugar[1])+1))] =='x' and  tabuleiro[str(int(lugar[0])+2) + str(chr(ord(lugar[1])+2))] == '-':
        print("Captura Obrigatória")
        return True

    #verificar se há peças na DIREITA que podem ser capturadas BAIXO DAMA
    if tabuleiro[lugar] == 'O' and lugar[0] not in '12' and lugar[1] not in 'gh' and tabuleiro[str(int(lugar[0])-1) + str(chr(ord(lugar[1])+1))] =='x' and  tabuleiro[str(int(lugar[0])-2) + str(chr(ord(lugar[1])+2))] == '-':
        print("Captura Obrigatória")
        return True
    #verificar se há peças na ESQUERDA que podem ser capturadas BAIXO DAMA
    if tabuleiro[lugar] == 'O' and lugar[0] not in '12' and lugar[1] not in 'ab' and tabuleiro[str(int(lugar[0])-1) + str(chr(ord(lugar[1])-1))] =='x' and  tabuleiro[str(int(lugar[0])-2) + str(chr(ord(lugar[1])-2))] == '-':
        print("Captura Obrigatória")
        return True
    
    
    #PRETO
    
    #verificar se há peças na ESQUERDA que podem ser capturadas CIMA DAMA
    if tabuleiro[lugar] =='X' and lugar[0] not in '78' and lugar[1] not in 'ab' and tabuleiro[str(int(lugar[0])+1) + str(chr(ord(lugar[1])-1))] =='o' and  tabuleiro[str(int(lugar[0])+2) + str(chr(ord(lugar[1])-2))] == '-':
        print("Captura Obrigatória")
        return True
    #verificar se há peças na DIREITA que podem ser capturadas CIMA DAMA
    if tabuleiro[lugar] == 'X' and lugar[0] not in '78' and lugar[1] not in 'gh' and  tabuleiro[str(int(lugar[0])+1) + str(chr(ord(lugar[1])+1))] =='o' and  tabuleiro[str(int(lugar[0])+2) + str(chr(ord(lugar[1])+2))] == '-':
        print("Captura Obrigatória")
        return True

    #verificar se há peças na DIREITA que podem ser capturadas BAIXO DAMA
    if tabuleiro[lugar] == 'X' and lugar[0] not in '12' and lugar[1] not in 'gh' and tabuleiro[str(int(lugar[0])-1) + str(chr(ord(lugar[1])+1))] =='o' and  tabuleiro[str(int(lugar[0])-2) + str(chr(ord(lugar[1])+2))] == '-':
        print("Captura Obrigatória")
        return True
    #verificar se há peças na ESQUERDA que podem ser capturadas BAIXO DAMA
    if tabuleiro[lugar] == 'X' and lugar[0] not in '12' and lugar[1] not in 'ab' and tabuleiro[str(int(lugar[0])-1) + str(chr(ord(lugar[1])-1))] =='o' and  tabuleiro[str(int(lugar[0])-2) + str(chr(ord(lugar[1])-2))] == '-':
        print("Captura Obrigatória")
        return True
    

    return False
    



while True:

    #De quem é a vez
    if vez=='o':
        print("VEZ DAS PEÇAS BRANCAS (o)")
    elif vez=='x':
        print("VEZ DAS PEÇAS PRETAS (x)")
   
   
   
   
   
    #Entrada
    if p==0:
        movimento=input("Peça que será movida e para onde ela vai (ex: 3a4b) ")  
        movi=movimento[0]+movimento[1].lower()
        lugar=movimento[2]+movimento[3].lower()
        
           
        while restricaoFormato(movimento,movi,lugar)==False:
           
                movimento=input("Peça que será movida e para onde ela vai (ex: 3a4b) ")
                movi=movimento[0]+movimento[1].lower()
                lugar=movimento[2]+movimento[3].lower()
        if tabuleiro[movi] not in [damaPreta, damaBranca]:
            while capturaObrigatoria(tabuleiro, vez) and capturaPossivel(movi,lugar)==False:
                    movimento=input("Peça que será movida e para onde ela vai (ex: 3a4b) ")
                    movi=movimento[0]+movimento[1].lower()
                    lugar=movimento[2]+movimento[3].lower()
        
        
                
    #Verificação das restrições e caso alguma não seja cumprida, será necessário digitar novamente.
    while True:
        k=0
        if tabuleiro[movi]!=vez or tabuleiro[movi] not in [damaBranca, damaPreta] and restricaoLugarImpo(movi,lugar) == False:
             k = 1
        if tabuleiro[movi] not in [damaBranca,damaPreta]:
            if restricaoMoviPeca(movi)==False or restricaoMoviIne(movi) == False or restricaoMoviVez(movi) == False or restricaoLugarOcupado(lugar)==False or restricaoLugarPosicao(lugar) == False or restricaoLugarFrente(lugar) == False or k>0:
               

                movimento=input("Peça que será movida e para onde ela vai (ex: 3a4b) ")
                movi=movimento[0]+movimento[1].lower()
                lugar=movimento[2]+movimento[3].lower()  
                while restricaoFormato(movimento,movi,lugar)==False:  
                    movimento=input("Peça que será movida e para onde ela vai (ex: 3a4b) ")  
                movi=movimento[0]+movimento[1].lower()
                lugar=movimento[2]+movimento[3].lower()                
           
           
            else:
                break
        else:
            if restricaoMoviPeca(movi)==False or essadamapodevoarn(lugar,movi)== False or dancinhadadama(movi,lugar) == False or restricaoMoviIne(movi) == False  or restricaoLugarOcupado(lugar)==False or restricaoMoviDamaCor(movi)==False:
                movimento=input("Peça que será movida e para onde ela vai (ex: 3a4b) ")
                movi=movimento[0]+movimento[1].lower()
                lugar=movimento[2]+movimento[3].lower()  
                while restricaoFormato(movimento,movi,lugar)==False:
                    movimento=input("Peça que será movida e para onde ela vai (ex: 3a4b) ")
               
                movi=movimento[0]+movimento[1].lower()
                lugar=movimento[2]+movimento[3].lower()  
                 
            else:
                break
   

    #Se a jogada for possível, então será modificada no tabuleiro e ele será exibido.
   
    mover(movi,lugar)
    montarBulero()
   
    #Verificação de quem é a vez de jogar e se há a possibilidade de captura dupla .
    if cap==0:
        contador+=1
        if contador%2==0:
           vez=pecaBranca
        else:
            vez=pecaPreta
    elif cap>0 and capturaObrigatoriaSeguida(vez,lugar,tabuleiro)==True or capturaObrigatoriaSeguidaDama(lugar,tabuleiro)==True:
        print("Você ainda pode capturar mais uma peça.")
        
        

    
        print()
    else:
        contador+=1
        if contador%2==0:
           vez=pecaBranca
        else:
            vez=pecaPreta aq
