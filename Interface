import tkinter as tk
#declarações variáveis
janelaTabuleiro = tk.Tk()
janelaTabuleiro.title("Tabuleiro")
tamanhoTab = 8

#Função para definir cores das posições
def corQuadrado(l, c):
    if (l + c) % 2 == 0:
        return "white"
    else:
        return "black"
#Função para reconhecimento do clique no mouse
def clicarQuadrado(clique):
    col = clique.widget.coluna
    lin = clique.widget.linha
    print(f"Clique no quadrado ({lin}, {col})")
#Criar os quadrados
for linha in range(tamanhoTab,0,-1):
    for coluna in range(tamanhoTab):
        cor = corQuadrado(linha, coluna)
        quadrado = tk.Frame(janelaTabuleiro, width=70, height=70, background=cor)
        quadrado.grid(row=linha, column=coluna)
        quadrado.linha = linha
        quadrado.coluna = coluna
        quadrado.bind("<Button-1>", clicarQuadrado)

janelaTabuleiro.mainloop()
