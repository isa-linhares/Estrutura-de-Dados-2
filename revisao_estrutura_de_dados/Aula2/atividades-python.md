# 18. Atividades

## Atividade 1 — Listas

```python
numeros = []

for i in range(10):
    valor = int(input(f"Digite o {i + 1}º número: "))
    numeros.append(valor)

print("\nNúmeros digitados:", numeros)

soma = sum(numeros)
media = soma / len(numeros)

print(f"Soma: {soma}")
print(f"Média: {media:.2f}")

# Desafio
maior = max(numeros)
menor = min(numeros)
pares = [n for n in numeros if n % 2 == 0]

print(f"Maior valor: {maior}")
print(f"Menor valor: {menor}")
print(f"Quantidade de números pares: {len(pares)}")
```

---

## Atividade 2 — Matrizes

```python
matriz = []

print("Digite os valores da matriz 3x3:")
for i in range(3):
    linha = []
    for j in range(3):
        valor = int(input(f"Elemento [{i}][{j}]: "))
        linha.append(valor)
    matriz.append(linha)

print("\nMatriz:")
for linha in matriz:
    print(linha)

soma_total = sum(sum(linha) for linha in matriz)
soma_diagonal = sum(matriz[i][i] for i in range(3))
maior_elemento = max(max(linha) for linha in matriz)

print(f"\nSoma de todos os elementos: {soma_total}")
print(f"Soma da diagonal principal: {soma_diagonal}")
print(f"Maior elemento: {maior_elemento}")
```

---

## Atividade 3 — Dicionário

```python
livro = {}

livro["titulo"] = input("Título: ")
livro["autor"] = input("Autor: ")
livro["ano"] = int(input("Ano: "))
livro["preco"] = float(input("Preço: "))

print("\nDados do livro:")
for chave, valor in livro.items():
    print(f"{chave}: {valor}")

novo_preco = float(input("\nNovo preço: "))
livro["preco"] = novo_preco

livro["categoria"] = input("Categoria: ")

print("\nDados atualizados:")
for chave, valor in livro.items():
    print(f"{chave}: {valor}")
```

---

## Atividade 4 — Dataclass

```python
from dataclasses import dataclass


@dataclass
class Aluno:
    nome: str
    matricula: int
    nota1: float
    nota2: float

    def media(self):
        return (self.nota1 + self.nota2) / 2


aluno = Aluno("Maria", 12345, 8.0, 9.0)
print(aluno.media())
```

---

## Atividade 5 — Lista de objetos

```python
from dataclasses import dataclass


@dataclass
class Aluno:
    nome: str
    matricula: int
    nota1: float
    nota2: float

    def media(self):
        return (self.nota1 + self.nota2) / 2


alunos = [
    Aluno("Maria", 1, 8.0, 9.0),
    Aluno("João", 2, 5.0, 6.0),
    Aluno("Ana", 3, 7.0, 7.0),
    Aluno("Pedro", 4, 4.0, 5.0),
    Aluno("Carla", 5, 9.0, 10.0),
]

print("Médias dos alunos:")
for aluno in alunos:
    print(f"{aluno.nome}: {aluno.media():.2f}")

print("\nAlunos aprovados (média >= 7.0):")
for aluno in alunos:
    if aluno.media() >= 7.0:
        print(f"{aluno.nome} - Média: {aluno.media():.2f}")

melhor_aluno = max(alunos, key=lambda a: a.media())
print(f"\nAluno com maior média: {melhor_aluno.nome} ({melhor_aluno.media():.2f})")
```

---

## Desafio integrador — Sistema de estoque

```python
from dataclasses import dataclass


@dataclass
class Produto:
    codigo: int
    nome: str
    preco: float
    quantidade: int


produtos = []


def cadastrar_produto():
    codigo = int(input("Código: "))
    nome = input("Nome: ")
    preco = float(input("Preço: "))
    quantidade = int(input("Quantidade: "))
    produtos.append(Produto(codigo, nome, preco, quantidade))
    print("Produto cadastrado com sucesso!\n")


def listar_produtos():
    if not produtos:
        print("Nenhum produto cadastrado.\n")
        return
    print("\nLista de produtos:")
    for p in produtos:
        print(f"Código: {p.codigo} | Nome: {p.nome} | Preço: R${p.preco:.2f} | Quantidade: {p.quantidade}")
    print()


def buscar_produto():
    codigo = int(input("Digite o código do produto: "))
    for p in produtos:
        if p.codigo == codigo:
            print(f"Encontrado: {p.nome} | Preço: R${p.preco:.2f} | Quantidade: {p.quantidade}\n")
            return
    print("Produto não encontrado.\n")


def valor_total_estoque():
    total = sum(p.preco * p.quantidade for p in produtos)
    print(f"Valor total do estoque: R${total:.2f}\n")


def produto_mais_caro():
    if not produtos:
        print("Nenhum produto cadastrado.\n")
        return
    p = max(produtos, key=lambda p: p.preco)
    print(f"Produto mais caro: {p.nome} - R${p.preco:.2f}\n")


def menu():
    while True:
        print("===== SISTEMA DE ESTOQUE =====")
        print("1 - Cadastrar produto")
        print("2 - Listar produtos")
        print("3 - Buscar produto")
        print("4 - Valor total do estoque")
        print("5 - Produto mais caro")
        print("0 - Sair")

        opcao = input("Escolha: ")

        if opcao == "1":
            cadastrar_produto()
        elif opcao == "2":
            listar_produtos()
        elif opcao == "3":
            buscar_produto()
        elif opcao == "4":
            valor_total_estoque()
        elif opcao == "5":
            produto_mais_caro()
        elif opcao == "0":
            print("Encerrando o sistema...")
            break
        else:
            print("Opção inválida. Tente novamente.\n")


if __name__ == "__main__":
    menu()
```
